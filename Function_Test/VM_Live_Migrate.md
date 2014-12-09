# 虚拟机动态迁移

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|134     |虚拟机动态迁移从一个Host到另一个Host|<ul><li>前提：</li></ul><ol><li>创建虚拟机时，设置Host-\>Migration Options设置为“允许手动和自动迁移”</li></ol><ul><li>操作：</li></ul><ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，选择一个数据中心下指定集群，点 击VMs</li><li>在虚拟机列表下选择一个或者多个虚拟机（运行状态），点击菜单上的Migrate</li><li>在“Migrate Virtual Machines”下选择“自动选择主机”或“选择目标主机”点击OK</li></ol>|虚拟机迁移成功（从一Host迁移到该集群下另一Host）|||
|135     |虚拟机动态迁移从一个Host到另一个Host|<ul><li>前提：</li></ul><ol><li>创建虚拟机时，设置Host-\>Migration Options设置为“仅允许手动迁移”</li></ol><ul><li>操作：</li></ul><ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，选择一个数据中心下指定集群，点击VMs</li><li>在虚拟机列表下选择一个或者多个虚拟机（运行状态），点击菜单上的Migrate</li><li>在“Migrate Virtual Machines”下选择“自动选择主机”或“选择目标主机”点击OK</li></ol>|虚拟机迁移成功（从一Host迁移到该集群下另一Host）|||
|136     |虚拟机动态迁移从一个Host到另一个Host|<ul><li>前提：</li></ul><ol><li>创建虚拟机时，设置Host-\>Migration Options设置为“不允许迁移”</li></ol><ul><li>操作：</li></ul><ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，选择一个数据中心下指定集群，点击VMs</li><li>在虚拟机列表下选择一个或者多个虚拟机（运行状态），点击菜单上的Migrate</li><li>在“Migrate Virtual Machines”下选择“自动选择主机”或“选择目标主机”点击OK</li></ol>|虚拟机没有迁移提示不能迁移|||
|137     |当Host变为维护模式时，虚拟机自动动态迁移到其他Host|<ul><li>前提：</li></ul><ol><li>创建虚拟机时，设置Host-\>Migration Options设置为“允许手动和自动迁移”</li></ol><ul><li>操作：</li></ul><ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，选择一个数据中心下指定集群下的Hosts</li><li>在Hosts列表下选择其中一个Host，点击菜单Maintenance，该Host变为维护模式</li><li>检查该集群下创建在该Host下的虚拟机是否自动迁移到该集群下其他Host上</li><li>|虚拟机自动迁移|||
|138     |当Host变为维护模式时，虚拟机自动动态迁移到其他Host|<ul><li>前提：</li></ul><ol><li>创建虚拟机时，设置Host-\>Migration Options设置为“仅允许手动迁移”</li></ol><ul><li>操作：</li></ul><ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，选择一个数据中心下指定集群下的Hosts</li><li>在Hosts列表下选择其中一个Host，点击菜单Maintenance，试图将该Host变为维护模式</li></ol>|Host不能变为维护模式，提示该Host上有不能迁移的虚拟机|||
|139     |当Host变为维护模式时，虚拟机自动动态迁移到其他Host|<ul><li>前提：</li></ul><ol><li>创建虚拟机时，设置Host-\>Migration Options设置为“不允许迁移”</li></ol><ul><li>操作：</li></ul><ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，选择一个数据中心下指定集群下的Hosts</li><li>在Hosts列表下选择其中一个Host，点击菜单Maintenance，试图将该Host变为维护模式</li></ol>|Host不能变为维护模式，提示该Host上有不能迁移的虚拟机|||
|140     ||<ol><li>定义Cluster power saving policy-\>Evenly\_Distributed 虚拟机动态迁移（CpuOverCommitDurationMinutes(0,10) 虚拟机动态迁移（HighUtilization[50,99]）</li><li>定义集群策略，CpuOverCommitDurationMinutes设置为2（0,10），HighUtilization 50[50,99]</li><li>在一台主机上同时启多台虚拟机（允许手动和自动迁移），同时虚拟机上运行消耗CPU的程序（如：echo "scale=100000;4\*a(1)"\|bc -l）</li><li>观察主机CPU使用情况达到50%([50,99])及以上时，时间为2([1,9])分钟，虚拟机作何反应</li></ol>|时间到达2分钟后，虚拟机开始自动迁移|||
|141     ||定义Cluster power saving policy-\>Evenly\_Distributed 虚拟机动态迁移（HighUtilization[50,99]）||||
|142     ||<ol><li>定义Cluster power saving policy-\>Power\_Saving虚拟机 动态迁移（CpuOverCommitDurationMinutes(0,10)）</li><li>选择集群，右键编辑集群，设置CpuOverCommitDurationMinutes为2</li><li>在node的vm上面跑程序，使得满足自动迁移的条件</li></ol>|2分钟之后开始迁移。|||
|143     ||<ol><li>定义Cluster power saving policy-\>Power\_Saving虚拟机 动态迁移（HighUtilization[50,99]）</li><li>选择集群，右键编辑集群，设置highUtilization80</li><li>在node2上面运行几个vm，总CPU占用率超过80%，单个vm占用率不超过。node1的CPU占用率大于20（下限），低于80%</li></ol>|一段时间后，部分虚拟机被迁移到node1。|||
|144     ||<ol><li>定义Cluster power saving policy-\>Power\_Saving虚拟机 动态迁移（LowUtilization[10,49]）</li><li>选择集群，右键编辑集群，设置lowUtilization为10</li><li>在集群中node1上任意虚拟机跑程序，使cpu占用率大于10%</li><li>将node2上关闭或者打开一些虚拟机，保证node2上存在虚拟机，且cpu占用率低于10%</li><li>如果node2上的虚拟机迁移到node1上面了，手动迁移回来</li></ol>|当node2的cpu占用率低于10%，虚拟机自动迁移到node1,如果手动移动回node2,需要一段时间后才会重新检测，然后再迁移||node1和node2的selinux应该配置一致，否则无法迁移|
|1       |虚拟机从一个集群迁移到另一个集群|<ul><li>前提：</li></ul><ol><li>环境中至少有一个可用集群</li><li>另一个集群中包含可用主机</li><li>虚拟机设置为可以迁移</li></ol><ul><li>操作：</li></ul><ol><li>登录到Engine管理端后，点击左侧树形面板中的【展开所有】按键，在默认数据中心下点击默认集群，点击【集群】下的【虚拟机】</li><li>在右侧虚拟机列表中显示所有可用的虚拟机，选择一台允许迁移的虚拟机，点击菜单中的【移植】按键或右键选择【移植】</li><li>弹出【移植虚拟机】的窗口，点击【高级参数】展开</li><li>在展开中选择目的集群，即要将虚拟机迁移到哪个集群中，点击【确定】</li></ol>|<ol><li>虚拟机迁移到另一个集群中</li><li>虚拟机状态变化为Migrating -> Up，在虚拟机的【迁移】属性中能够显示虚拟机迁移的进度</li></ol>|||


以上用例均为虚拟机磁盘为Internal 当虚拟机磁盘为External时进行虚拟机迁移，是否可以迁移成功（手动、自动）？？？

