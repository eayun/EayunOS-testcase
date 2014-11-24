# 主机的Fence

启用了Fence功能以后，当主机发生故障，Engine会选择数据中心里的另一台主机作为代理，测试这台主机的状态，如果主机确实故障，则通过Fence将该主机隔离，尽量不影响业务

* 在本集群中的Fence，需要的前提条件为：
  * 启用集群的隔离策略：【集群 -> 编辑 -> 隔离策略】，勾选Enable Fence
  * 本数据中心或本集群中至少有另一台主机（以作为代理）
  * 主机配置了电源管理

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|1|非SPM主机网络异常（断开）时的Fence|<ol><li>通过电源管理打开其中一台主机A（或ssh到主机上，但由于网络会断开，不推荐），这台主机不能是运行着HostedEngine虚拟机的主机</li><li>在主机A上，运行<code>service network stop<code>，模拟网络异常的情况</li><li>回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态|执行Fence成功，主机由于被代理执行重启命令而重新启动<br /><br /><ol><li>主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待60sec</li><li>由于Engine连接不上主机A，主机A状态变为Non Resposive</li><li>本集群或数据中心里的另一台主机B被Engine选为代理，测试主机A的状态</li><li>主机B作为Engine的代理，首先执行SSH，发现连接超时，则向主机A发出执行Restart的命令，重启主机A</li><li>主机A被重启，状态变化为Reboot -> Up</li></ol>|||
|2|非SPM主机VDSM崩溃时的Fence|<ol><li>ssh到其中一台主机A上，这台主机不能是运行着HostedEngine虚拟机的主机</li><li>在主机A上，运行命令<code>service vdsmd stop</code>，模拟vdsmd服务崩溃的情况</li><li>回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态|执行Fence成功，主机由于被代理执行了重启命令而重新启动<br /><br /><ol><li>主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待60sec</li><li>由于Engine连接不上主机A，主机A状态变为Non Resposive</li><li>本集群或数据中心里的另一台主机B被Engine选为代理，测试主机A的状态</li><li>主机B作为Engine的代理，执行SSH，发现能够连接，则尝试重启VDSM，重启主机A的vdsmd服务</li><li>主机A的vdsmd服务被重启，主机状态变化为Connecting -> Non Responsive -> Up，主机恢复正常</li></ol>|||
|3|SPM主机网络异常时的Fence|<ol><li>>通过电源管理打开其中的SPM主机A（或ssh到主机上，但由于网络会断开，不推荐），这台主机不能是运行着HostedEngine虚拟机的主机</li><li>在主机A上，运行<code>service network stop<code>，模拟网络异常的情况</li><li>回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态|执行Fence成功，主机由于被代理执行重启命令而重新启动<br /><br /><ol><li>主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待80sec</li><li>由于Engine连接不上主机A，主机A状态变为Non Resposive</li><li>本集群或数据中心里的另一台主机B被Engine选为代理，测试主机A的状态</li><li>主机B作为Engine的代理，首先执行SSH，发现连接超时，则向主机A发出执行Restart的命令，重启主机A</li><li>集群中的其他主机立刻被选为SPM，重新激活存储，存储域状态变为Active</li><li>主机A被重启，状态变化为Reboot -> Up</li></ol>|<ul><li>与预期结果不完全一致：</li></ul><br /><ol><li>主机重启前，集群中的其他主机没有被选为SPM，存储域中的主存储处于Unknow的状态</li><li>主机重启后，集群里的另一台主机被选为SPM</li></ol>||
|4|SPM主机VDSM崩溃时的Fence|<ol><li>>ssh到其中一台主机A上，这台主机不能是运行着HostedEngine虚拟机的主机</li><li>在主机A上，运行命令<code>service vdsmd stop</code>，模拟vdsmd服务崩溃的情况</li><li>回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态|执行Fence成功，主机由于被代理执行了重启命令而重新启动<br /><br /><ol><li>主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待60sec</li><li>由于Engine连接不上主机A，主机A状态变为Non Resposive</li><li>本集群或数据中心里的另一台主机B被Engine选为代理，测试主机A的状态</li><li>集群里的另一台主机立即被选为SPM，重新激活存储域，存储域状态为Active</li><li>主机B作为Engine的代理，执行SSH，发现能够连接，则尝试重启VDSM，重启主机A的vdsmd服务</li><li>主机A的vdsmd服务被重启，主机状态变化为Connecting -> Non Responsive -> Up，主机恢复正常</li></ol>|||
