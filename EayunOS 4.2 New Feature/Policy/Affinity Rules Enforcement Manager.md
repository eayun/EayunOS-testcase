# Affinity Rules Enforcement Manager

* 概述

该篇将要介绍的是一个给运行的虚拟机强制添加关联规则的管理器。该管理器将会定期检查每个集群是否存在关联规则冲突的问题，如果发现相关问题，会采取迁移问题虚拟机的方式解决关联冲突的问题。

* 测试

1. 集群被创建，管理器即被创建
   * 启动时创建管理器
     1. 开启 engine
     2. 从日志信息中检查 ARES 是否为默认集群创建了 PerCluster 对象。
 
   * 在新的集群上创建管理器
     1. 创建新的集群
     2. 从日志信息中检查 ARES 是否为新的集群创建了 PerCluster 对象。

   * 被删除集群的管理器删除
     1. 删除集群
     2. 从日志信息中检查 ARES 是否为已被删除的集群删除。
  
2. 管理器时间间隔检查
   * 检查规律的时间间隔
   * 检查长时间的时间间隔

3. 管理器强制关联规则

4. 候选关联规则检查

5. 平衡竞争的管理器

=======
 
= Affinity Rules Enforcement Manager =

== Summary ==
A new manager that will enforce affinity rules for running VMs.
The manager will periodically check each cluster for affinity rule conflicts and will try to resolve those conflicts by migrating problematic VMs. Each interval only one VM will be migrated by the manager for each cluster(As long as there are conflicts).

The following picture, explains AR (Affinity Rules),  before enforcement and after enforcement 
<br />
(The green boxes represent VMs belonging to positive affinity groups and the red ones are VMs belonging to negative affinity groups.
<br />
See VM-Affinity page for more details http://www.ovirt.org/Features/VM-Affinity). 
[[File:Affinity_Rule_Enforcement.png]]

== Procedure ==
<br />
[[File:ARES_Life_Cycle.png]]
<br />
[1][2]
<br />
[The following method identify broken affinity rule,  designate vm that breaks the rule and migrates the vm.]
<br />
''' Manager interval reached: Enforce affinity rules using migration '''
#Find migration free clusters
#for each migration free cluster:
##'''choose next VM to migrate''' and add to VM candidates.
#for each vm candidate for migrations:
##migrate VM.

== Related methods ==
''' Choose next vm to migrate(cluster) '''
# Get all hard affinity groups.
# Get unified affinity groups().
: The following picture explains UAG (Unified Affinity Group) algorithm
: [[File:UAG_Algorithm.png]]
# Loop over all unified affinity groups(order by size and than by lowest VM id[4]):
##if affinity group positive:
###find VM violating positive affinity group
##Else:
###find VM violating negative affinity group
##if found candidate VM check if can migrate VM:
###If can migrate VM then return VM.
<br />

== Footnotes ==
[1]Methods are written in the section “related methods”.
<br />
[2] If no class is written(As for most methods/fields) assume it’s in the manager itself.
<br />
[3] The migration command will be done automatically to let the scheduler decide where to migrate the VM based on  other policies as well.
<br />
[4] It’s important to keep getting the same groups in the same order each time. The order is kept because affinity group are assumed not to change very often during enforcement.
<br />

== Testing ==
# Manager creation when cluster is created:
## Manager creation on startup.
### Start engine
### Check log to see that ARES has created PerCluster object for the default cluster.
## Manager creation on new cluster.
### Create new cluster
### Check log to see that ARES has created PerCluster object for the new cluster.
## Manager deletion of deleted cluster(pre-condition = test 1b):
### Delete cluster
### Check log to see that ARES has deleted PerCluster object for the deleted cluster.
# Manager interval check:
## Check regular interval:
### Create new cluster. 
### Check log to see that ARES has created PerCluster object for cluster. (Make sure cluster has affinity rules).
### Add 2 VMs on the same host
### Add negative affinity rule for the 2 VMs.
### wait for “regular interval”
### check that ARES interval reached.
## Check long interval: (Preconditions = one datacenter is up, affinity rules enforced).
### Create new cluster. 
### Check log to see that ARES has created PerCluster object for cluster. (Make sure cluster has no affinity rules).
### Wait for long interval
### Check logs to see that long interval reached.
# Manager Affinity Rules enforcement:
## Enforcement for positive affinity rule: (Precondition load balancer if off, All vms can run together on the same hypervisor)
### Start engine
### Add 2 hosts.
### For host A add 3 Vms
### For host B add 1 Vm
### Add positive affinity rule for all VMs.
### Wait for regular interval.
### See that the Vm from Host B migrated to host A.
## Enforcement for negative affinity rule: (Preconditions: load balancer if off, All vms can run together on the each hypervisor)
### Start engine
### Add 2 hosts.
### For host A add 2 Vms
### For host B no Vms should be running on it.
### Add negative affinity rule for the two VMs.
### Wait for regular interval.
### See that one Vm migrated from host A to host B.
## Enforcement for balanced hypervisors:(Precondition: All Vms should be able to run on the same hypervisor at once)
### Start engine
### Add 2 hosts
### For host A add 3 Vms
### For host B add 3 Vms
### Add positive affinity rule for all Vms.
### Wait for 6 regular intervals(6 * regular interval)
### See that all Vms migrated from one of the hosts to the other one.
# Affinity Rule contradictions check:
## Check two opposite conditions:
### Start engine
### Add 2 hosts
### Add 2 Vms
### Add positive affinity rule for both VMs.
### Add negative affinity rule for both VMs.
### Wait for regular interval.
### Check logs to see a new exception was thrown saying: “Affinity group contradiction detected” (With associated groups).
# Balancer competing managers:
## Check power saving and colliding affinity:
### Start engine
### Add 2 hosts
### Add 6 Vms(Each host should have 3 VMs).
### Add positive affinity rule for 3 VMs
### Put balancer on power saving.
### Wait for a 4 regular intervals(4 * regular interval).
### Check in the logs that the manager has been shutdown because of contradicting migrations.

== Benefit to oVirt ==
Affinity groups will be enforced also for VMs which are already running.  

== Dependencies / Related Features ==
#SchedulerUtilQuartzImpl - scheduleAFixedDelayJob, scheduleAOneTimeJob.
#VmAffinityFilterPolicyUnit - getAcceptableHosts, filter. 
#MigrateVmCommand.
#AddAffinityGroupCommand.

== Intervals and values used in the system ==
#Regular interval - 1 minute.
<br />

== Release Notes ==
This feature is a manager that checks if hard affinity rules are broken and migrates VMs in order to enforce them. 
<br />
This manager includes:
# Manager only starts migrations when no other migrations are active in the cluster.
# Manager uses scheduler's automatic migration command to comply with filter and weight policies.
# Manager has a new and improved algorithm for finding affinity rule contradictions called "Unified Affinity Group Algorithm".
# Manager will enforce affinity rules one by one, starting with the violated affinity rule which consists of most VMs.
# Manager's strategy to enforce affinity rules in case of positive groups is to migrate VMs from the hypervisor that has the minimum number of VMs from the same affinity group to the one that has the most VMs(Taking into account the Scheduler policies. Sometimes VMs might be migrated to a different host if the scheduler thinks it's better).
# Affinity rules only work for clusters with version >= 3.5.

== Phase 2 (not included in 3.6.0) ==
# Using UAG algorithm to tell the user where there are conflicting affinity rules and also if the affinity rules can be optimized by uniting positive intersecting groups.
# Taking into consideration the host's RAM, CPU type, Network interfaces etc in order choose only hosts that can run the entire affinity group(In case of enforcing positive affinity group).

== Comments and Discussion ==
For more information see the following BugZilla link:
<br />
https://bugzilla.redhat.com/show_bug.cgi?id=1112332

* Refer to [[Talk:Affinity_Group_Enforcement_Manager]]  <!-- This adds a link to the "discussion" tab associated with your page.  This provides the ability to have ongoing comments or conversation without bogging down the main feature page -->

[[Category:Feature|Affinity Group Enforcement Manager]]
[[Category:oVirt 3.6 Proposed Feature|Affinity Group Enforcement Manager]]
[[Category:OVirt 3.6 Feature|Affinity Group Enforcement Manager]]
[[Category:SLA]]

