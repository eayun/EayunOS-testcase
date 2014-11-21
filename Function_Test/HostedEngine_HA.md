# Hosted Engine的高可用

Hosted Engine中，Engine虚拟机是高可用的，它的高可用被主机管理，而不是被Engine管理，所以Engine虚拟机的高可用是不依赖于电源管理的

Engine虚拟机应该能在它所管理的任意一台安装了hosted-engine插件的主机上启动

* 本次测试至少有一台可用的Hosted Engine HA主机，为了方便测试，需要进行一些配置：
  * 关闭电源管理：【主机 -> 编辑 -> 电源管理】，取消勾选启用电源管理
  * 取消集群的隔离策略：【集群 -> 编辑 -> 隔离策略】，取消勾选Enable Fence


|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|1|测试HostedEngine虚拟机在网络故障情况下的高可用情况|<ol><li>为打开HostedEngine虚拟机的控制台，在本机运行命令：<code>/bin/remote-viewer vnc://host_ip:5900</code></li><li>同时ssh到HostedEngine的HA主机上</li><li>在HostedEngine虚拟机的控制台中，运行命令：<code>service network stop</code>，停止网络，模拟网络故障发生</li><li>在HostedEngine的HA主机上运行命令<code>hosted-engine --vm-status</code>，以观察HostedEngine虚拟机和Engine的状态变化</li></ol>|HA成功执行，虚拟机在另一台主机上重启<br /><br /><ul><li>在HA主机上，运行命令<code>hosted-engine --vm-status</code>，可以看到：</li></ul><ol><li>Engine的状态显示为：Engine status : {"reason": "failed liveliness check", "health": "bad", "vm": "up", "detail": "powering down"}</li><li>HA服务开始重启虚拟机，看到虚拟机在另一台主机上重启，虚拟机的状态变化为：Powering Down -> Powering Up -> Up</li><li>虚拟机重启完毕后，HA服务不断去检查engine服务的状态，直到engine服务启动，能够通过浏览器访问为止，最终在运行了HostedEngine虚拟机上的主机状态显示为：Engine status : {"health": "good", "vm": "up", "detail": "up"}</li></ol><br /><ul><li>在HostedEngine虚拟机的控制台中，可以看到</li></ul><ol><li>弹出关机提示，说明HA服务要重启虚拟机</li></ol>|与预期结果一致|另一台可用主机的分数不能为0，也不能处于本地维护（maintenance mode=local），HostedEngine虚拟机不会在以上两种情况下的主机上重启|
|2|测试HostedEngine虚拟机在Engine服务崩溃情况下的高可用情况|<ol><li>ssh到HostedEngine虚拟机上，运行命令：<code>service ovirt-engine stop</code> 或 <code>/etc/init.d/ovirt-engine stop</code>，停止engine服务，模拟engine服务崩溃</li><li>ssh到HostedEngine的HA主机上，运行命令<code>hosted-engine --vm-status</code>，以观察HostedEngine虚拟机和Engine的状态变化</li></ol>|HA成功执行，虚拟机在另一台主机上重启<br /><br /><ul><li>在HA主机上，运行命令<code>hosted-engine --vm-status</code>，可以看到：</li></ul><ol><li>Engine的状态显示为：Engine status : {"reason": "failed liveliness check", "health": "bad", "vm": "up", "detail": "powering down"}</li><li>HA服务开始重启虚拟机，看到虚拟机在另一台主机上重启，虚拟机的状态变化为：Powering Down -> Powering Up -> Up</li><li>虚拟机重启完毕后，HA服务不断去检查engine服务的状态，直到engine服务启动，能够通过浏览器访问为止，最终在运行了HostedEngine虚拟机上的主机状态显示为：Engine status : {"health": "good", "vm": "up", "detail": "up"}</li></ol><br /><ul><li>在HostedEngine虚拟机的中，可以看到</li></ul><ol><li>弹出关机提示，说明HA服务要重启虚拟机</li></ol>|与预期结果一致|<ol><li>另一台可用主机的分数不能为0，也不能处于本地维护（maintenance mode=local），HostedEngine虚拟机不会在以上两种情况下的主机上重启</li><li>目前，当engine服务停止时，只实现了重启虚拟机的情况，将来可能实现仅仅重启engine服务而不重启虚拟机</li></ol>|
|3|HostedEngine虚拟机异常崩溃情况下的高可用|<ol><li>ssh到运行了HostedEngine虚拟机的主机上，运行命令<code>ps aux\|grep qemu</code>，查看运行HostedEngine虚拟机的进程号</li><li>运行命令：<code>kill [qemu进程号]</code>，模拟虚拟机的异常崩溃</li><li>在HostedEngine的HA主机上运行命令<code>hosted-engine --vm-status</code>，以观察虚拟机和engine服务的状态变化</li><ol>|HA成功执行，虚拟机在本地主机上重启；如果本地重启失败，则尝试在另一台主机上重启<br /><br /><ul><li>在HA主机上，运行命令<code>hosted-engine --vm-status</code>，可以看到：</li></ul><ol><li>Engine的状态显示为：Engine status : {"reason": "failed liveliness check", "health": "bad", "vm": "up", "detail": "powering down"}</li><li>HA服务开始重启虚拟机，看到虚拟机在另一台主机上重启，虚拟机的状态变化为：Powering Down -> Powering Up -> Up</li><li>虚拟机重启完毕后，HA服务不断去检查engine服务的状态，直到engine服务启动，能够通过浏览器访问为止，最终在运行了HostedEngine虚拟机上的主机状态显示为：Engine status : {"health": "good", "vm": "up", "detail": "up"}</li></ol>|与预期结果不完全一致：<ol><li>HostedEngine虚拟机没有尝试在本地主机上重启，而是直接在另一台主机上重启</li></ol>|由于HostedEngine虚拟机异常崩溃后，本地主机的分数为0，而HostedEngine虚拟机无法在分数为0的主机上启动，因此，虚拟机直接在另一台可用的主机上启动|
|4|HostedEngine虚拟机在HA主机网络故障情况下的高可用|<ol><li>ssh到运行了HostedEngine虚拟机的主机上，运行命令<code>service network stop</code>，模拟HA主机网络故障的情况</li><li>ssh到另一台主机上，运行命令<code>hosted-engine --vm-status</code>，以观察HostedEngine虚拟机和Engine服务的状态变化</li></ol>|HA成功执行，虚拟机在本地主机上重启；如果本地重启失败，则尝试在另一台主机上重启<br /><br /><ul><li>在HA主机上，运行命令<code>hosted-engine --vm-status</code>，可以看到：</li></ul><ol><li>Engine的状态显示为：Engine status : {"reason": "failed liveliness check", "health": "bad", "vm": "up", "detail": "powering down"}</li><li>HA服务开始重启虚拟机，看到虚拟机在另一台主机上重启，虚拟机的状态变化为：Powering Down -> Powering Up -> Up</li><li>虚拟机重启完毕后，HA服务不断去检查engine服务的状态，直到engine服务启动，能够通过浏览器访问为止，最终在运行了HostedEngine虚拟机上的主机状态显示为：Engine status : {"health": "good", "vm": "up", "detail": "up"}</li></ol>|与预期结果一致||
|5|HostedEngine虚拟机在存储故障情况下的高可用（本实验以NFS存储为例）|<ol><li>ssh到运行了HostedEngine虚拟机的HA主机上，运行命令<code>mount</code>，找到当前HostedEngine虚拟机所使用的存储的路径</li><li>运行命令<code>umount -l [存储路径]</code>，模拟主机挂载存储故障的情况</li><li>在主机上运行命令<code>hosted-engine --vm-status</code>，观察HostedEngine虚拟机和Engine服务的状态变化</li></ol>|HA成功执行，存储被重新挂载，不重启HostedEngine虚拟机，期间Engine业务没有中断<br /><br /><ul><li>在HA主机上，可以看到：</li></ul><ol><li>HostedEngine虚拟机状态良好，期间Engine业务没有中断</li><li>运行命令<code>mount</code>，观察到HostedEngine虚拟机所使用的存储被重新挂载</li><li>如果本地重新挂载存储失败，HostedEngine虚拟机应该能在另一台可用的HA主机上重启</li></ol>|与预期结果一致||
|6|HostedEngine虚拟机在主机崩溃情况下的高可用|<ol><li>通过电源管理打开运行了HostedEngine虚拟机的主机，将主机关机，模拟主机崩溃的情况</li><li>ssh到另一台可用的HA主机上，运行命令<code>hosted-engine --vm-status</code>，以观察HostedEngine虚拟机和Engine服务的状态变化</li></ol>|HA成功执行，虚拟机在本地主机上重启；如果本地重启失败，则尝试在另一台主机上重启<br /><br /><ul><li>在HA主机上，运行命令<code>hosted-engine --vm-status</code>，可以看到：</li></ul><ol><li>Engine的状态显示为：Engine status : {"reason": "failed liveliness check", "health": "bad", "vm": "up", "detail": "powering down"}</li><li>HA服务开始重启虚拟机，看到虚拟机在另一台主机上重启，虚拟机的状态变化为：Powering Down -> Powering Up -> Up</li><li>虚拟机重启完毕后，HA服务不断去检查engine服务的状态，直到engine服务启动，能够通过浏览器访问为止，最终在运行了HostedEngine虚拟机上的主机状态显示为：Engine status : {"health": "good", "vm": "up", "detail": "up"}</li></ol>|与预期结果一致||
|7|HostedEngine虚拟机在VDSM崩溃情况下的高可用||||HA服务不允许停止vdsmd服务，运行命令<code>service vdsmd stop</code>，会提示：Job for vdsmd.service canceled.|
|8|当所有主机（网络）故障时HostedEngine虚拟机的表现||||如果所有的主机网络出现了故障，那么，所有的HA主机的分数都会变成0，没有可运行虚拟机的主机，因此不会运行虚拟机，虚拟机无法重启|