# Engine的高可用
* 摘要
  Hosted Engine中，Engine虚拟机是高可用的，它的高可用被主机管理，而不是被Engine管理，所以Engine虚拟机的高可用是不依赖于电源管理的。

  Engine虚拟机应该能在它所管理的任意一台安装了hosted-engine插件的主机上启动。

* 本次测试至少有一台可用的Hosted Engine HA主机，为了方便测试，需要进行一些配置：
  * 关闭电源管理：【主机 -> 编辑 -> 电源管理】，取消勾选启用电源管理。
  * 取消集群的隔离策略：【集群 -> 编辑 -> 隔离策略】，取消勾选Enable Fence。

## Engine网络故障

1. 使用vnc控制台打开HostedEngine虚拟机，ssh到HostedEngine虚拟机的HA主机上
1. 在HostedEngine控制台上，运行命令<code>service network stop</code>，停止网络，模拟网络故障的情况
1. 在HostedEngine的HA主机上，运行命令<code>hosted-engine --vm-status</code>，查看HostedEngine虚拟机的状态
1. 在HA主机上，可以看到：
  1. Engine的状态变为
  1. HA服务开始重启Engine虚拟机，运行命令`hosted-engine --vm-status`可以看到HostedEngine虚拟机在另一台主机上重启，状态变化为Powering Down -> Powering Up -> Up。
  1. HostedEngine虚拟机重启后，HA服务不断去检查engine服务的状态，直到engine服务启动成功，健康状态为good。
  1. 在HostedEngine虚拟机上可以看到系统发出了关机提示。

## Engine服务崩溃

1. ssh到HostedEngine虚拟机上，运行命令<code>service ovirt-engine stop</code> 或 <code>/etc/init.d/ovirt-engine stop</code>
1. ssh到HostedEngine的HA主机上，运行命令<code>hosted-engine --vm-status</code>，查看HostedEngine虚拟机的状态
1. 在HA主机上，可以看到：
  1. Engine的状态变为
  1. HA服务开始尝试重启HostedEngine虚拟机，运行命令<code>hosted-engine --vm-status</code>可以看到HostedEngine在另一台主机上重启，状态变化为Powering Down -> Powering Up -> Up。
  1. HostedEngine虚拟机重启后，HA服务不断去检查engine服务的状态，直到engine服务启动成功，健康状态为good。
  1. 在HostedEngine虚拟机上可以看到系统发出了关机提示。

## Engine虚拟机崩溃

1. ssh到运行了HostedEngine虚拟机的HA主机上，运行命令<code>ps aux | grep qemu</code>，查看运行HostedEngine虚拟机的qemu进程。
1. 运行命令<code>kill [qemu进程号]</code>，模拟HostedEngine虚拟机崩溃的情况。
1. 在该主机上运行命令<code>hosted-engine --vm-status</code>，看到虚拟机的状态是Down，该主机的分数为0。
1. 原本当HostedEngine虚拟机崩溃时，虚拟机应该首先尝试在本地主机上重启，重启失败后再去另一台主机上重启，但是由于虚拟机崩溃后，本地主机的分数为0，虚拟机无法在分数为0的主机上启动。
1. 看到虚拟机直接在另一台主机上重启，运行命令<code>hosted-engine --vm-status</code>可以看到HostedEngine虚拟机状态变化为Powering Down -> Powering Up -> Up。
1. Engine虚拟机重启后，HA服务不断去检查Engine服务的状态，直到engine服务启动成功，健康状态为good。

## 主机网络崩溃

1. ssh到运行了HostedEngine虚拟机的主机上，运行命令<code>service network stop</code>，模拟主机网络崩溃的情况。
1. ssh到另一台可用的HA主机上，运行命令<code>hosted-engine --vm-status</code>，查看虚拟机的状态。
1. 看到虚拟机在另一台分数不为0的主机上重启，如果当时没有分数不为0的主机，ha服务则等待，直到找到分数不为0的主机来重启HostedEngine虚拟机为止。

## 存储故障

1. 在运行了HostedEngine的HA主机上，运行命令<code>mount</code>，找到当前HostedEngine虚拟机所使用的存储。
1. 运行命令<code>umount -l [存储路径]</code>，模拟主机挂载存储故障的情况。
1. 运行命令<code>hosted-engine --vm-status</code>，查看虚拟机的状态，看到虚拟机状态良好。
1. 运行命令<code>mount</code>，看到HostedEngine虚拟机所使用的存储被重新挂载，而期间Engine业务没有中断，能够正常使用。
1. 如果在本地主机上重新挂载存储，失败了，则在另一台HA主机上重启HostedEngine虚拟机。

## VDSM崩溃
* HA服务不允许停止vdsmd服务，运行<code>service vdsmd stop</code>会提示：`Job for vdsmd.service canceled.`。

## 主机崩溃

1. 使用电源管理打开运行了HostedEngine的主机，ssh到另一台可用的HA主机上。
1. 关闭运行了HostedEngine的主机，在另一台HA主机上运行命令<code>hosted-engine --vm-status</code>。
1. 看到虚拟机的状态为Down，此时，虚拟机会在这台可用的HA主机上重启，可以看到HostedEngine虚拟机状态变化为Powering Down -> Powering Up -> Up。
1. Engine虚拟机重启后，HA服务不断去检查Engine服务的状态，直到engine服务启动成功，健康状态为good。

## 所有主机网络故障
* 如果所有的主机网络出现了故障，那么，所有的HA主机的分数都会变成0，不会运行虚拟机，虚拟机无法重启。

