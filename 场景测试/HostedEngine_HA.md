# Hosted Engine的高可用

Hosted Engine中，Engine虚拟机是高可用的，它的高可用被主机管理，而不是被Engine管理，所以Engine虚拟机的高可用是不依赖于电源管理的

Engine虚拟机应该能在它所管理的任意一台安装了hosted-engine插件的主机上启动

* 本次测试至少有一台可用的Hosted Engine HA主机，为了方便测试，需要进行一些配置：
  * 关闭电源管理：【主机 -> 编辑 -> 电源管理】，取消勾选启用电源管理
  * 取消集群的隔离策略：【集群 -> 编辑 -> 隔离策略】，取消勾选Enable Fence

* Engine网络故障

  |用例编号|操作|预期结果|实际结果|备注|
  |--------|----|--------|--------|----|
  |1|<ol><li>打开HostedEngine虚拟机的控制台，在本机运行命令：<code>/bin/remote-viewer vnc://host_ip:5900</code></li><li>同时ssh到HostedEngine的HA主机上</li><li>在HostedEngine虚拟机的控制台上，运行命令：<code>service network stop</code>，停止网络，模拟网络故障发生</li><li>在HostedEngine的HA主机上运行命令<code>hosted-engine --vm-status</code>，以观察HostedEngine虚拟机的状态变化，和Engine的状态变化</li></ol>|HA成功执行，虚拟机在另一台主机上重启</br></br><ul><li>在HA主机上，运行命令<code>hosted-engine --vm-status</code>，可以看到：</li></ul><ol><li>Engine的状态显示为：Engine status : {"reason": "failed liveliness check", "health": "bad", "vm": "up", "detail": "powering down"}</li><li>HA服务开始重启虚拟机，看到虚拟机在另一台主机上重启，虚拟机的状态变化为：Powering Down -> Powering Up -> Up</li><li>虚拟机重启完毕后，HA服务不断去检查engine服务的状态，直到engine服务启动，能够通过浏览器访问为止，最终在运行了HostedEngine虚拟机上的主机状态显示为：Engine status : {"health": "good", "vm": "up", "detail": "up"}</li></ol></br><ul><li>在HostedEngine虚拟机的控制台中，可以看到</li></ul><ol><li>弹出关机提示，说明HA服务要重启虚拟机</li></ol>|与预期结果一致|另一台可用主机的分数不能为0，也不能处于本地维护（maintenance mode=local），HostedEngine虚拟机不会在以上两种情况下的主机上重启|
