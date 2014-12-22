# 主机的Fence
* 摘要
  启用了Fence功能以后，当主机发生故障，Engine会选择数据中心里的另一台主机作为代理，测试这台主机的状态，如果主机确实故障，则通过Fence将该主机隔离，尽量不影响业务。

## 在同一个数据中心里的Fence
* 需要的前提条件为：
  * 启用集群的隔离策略：【集群 -> 编辑 -> 隔离策略】，勾选Enable Fence。
  * 本数据中心或本集群中至少有另一台主机（以作为代理）。
  * 主机配置了电源管理。

### 非SPM主机网络异常（断开）时的Fence

1. 通过电源管理打开其中一台主机A（或ssh到主机上，但由于网络会断开，不推荐），这台主机不能是运行着HostedEngine虚拟机的主机。
1. 在主机A上，运行<code>service network stop</code>，模拟网络异常的情况。
1. 回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态，看到如下过程：
  1. 由于Engine连接不上主机A，主机A状态变为Non Resposive。
  1. 本集群或数据中心里的另一台主机B被Engine选为代理，测试主机A的状态，事件中有相关的提示。
  1. 主机B作为Engine的代理，首先执行SSH，发现连接超时，则向主机A发出执行Restart的命令，重启主机A，事件中有相关的提示。
  1. 主机A被重启，状态变化为Reboot -> Up。
1. 执行Fence成功，主机由于被代理执行重启命令而重新启动。

### 非SPM主机VDSM崩溃时的Fence

1. ssh到其中一台主机A上，这台主机不能是运行着HostedEngine虚拟机的主机。
1. 在主机A上，运行命令<code>service vdsmd stop</code>，模拟vdsmd服务崩溃的情况。
1. 回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态，看到如下过程：
  1. 主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待60sec，事件中有相关的提示。
  1. 由于Engine连接不上主机A，主机A状态变为Non Resposive。
  1. 本集群或数据中心里的另一台主机B被Engine选为代理，测试主机A的状态，事件中有相关的提示。
  1. 主机B作为Engine的代理，执行SSH，发现能够连接，则尝试重启VDSM，重启主机A的vdsmd服务。
  1. 主机A的vdsmd服务被重启，主机状态变化为Connecting -> Non Responsive -> Up，主机恢复正常。
1. 执行Fence成功，主机由于代理执行了vdsmd服务的重启，重启了vdsmd服务，主机A重新连接到环境中。

### 非SPM主机崩溃时的Fence

1. 通过电源管理打开其中一台主机A（或ssh到主机上，但由于网络会断开，不推荐），这台主机不能是运行着HostedEngine虚拟机的主机。
1. 在主机A上，运行<code>poweroff</code> 或直接通过电源管理关机，模拟主机异常崩溃的情况。
1. 回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态，看到如下过程：
  1. 主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待60sec，事件中有相关的提示。
  1. 由于Engine连接不上主机A，主机A状态变为Non Resposive，事件中有相关提示。
  1. 本集群或数据中心里的另一台主机B被Engine选为代理，测试主机A的状态，事件中有相关的提示。
  1. 主机B作为Engine的代理，首先执行SSH，发现连接超时，则向主机A发出执行Restart的命令，重启主机A，事件中有相关的提示。
  1. 主机A被重启，状态变化为Reboot -> Up。
1. 执行Fence成功，主机由于被代理执行启动命令而开机。

### SPM主机网络异常时的Fence

1. 通过电源管理打开其中的SPM主机A（或ssh到主机上，但由于网络会断开，不推荐），这台主机不能是运行着HostedEngine虚拟机的主机。
1. 在主机A上，运行<code>service network stop</code>，模拟网络异常的情况。
1. 回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态，看到如下过程：
  1. 主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待80sec，事件中有相关的提示。
  1. 由于Engine连接不上主机A，主机A状态变为Non Resposive。
  1. 本集群或数据中心里的另一台主机B被Engine选为代理，测试主机A的状态，事件中有相关的提示。
  1. 主机B作为Engine的代理，首先执行SSH，发现连接超时，则向主机A发出执行Restart的命令，重启主机A，事件中有相关的提示。
  1. 集群中的其他主机立刻被选为SPM，重新激活存储，存储域状态变为Active。
  1. 主机A被重启，状态变化为Reboot -> Up。
1. 执行Fence成功，主机由于被代理执行重启命令而重新启动。

### SPM主机VDSM崩溃时的Fence

1. 通过电源管理打开其中一台主机A（或ssh到主机上，但由于主机会关机，不推荐），这台主机不能是运行着HostedEngine虚拟机的主机。
1. 在主机A上，运行<code>poweroff</code> 或直接通过电源管理关机，模拟主机异常崩溃的情况。
1. 回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态，看到如下过程：
  1. 主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待80sec，事件中有相关的提示。
  1. 由于Engine连接不上主机A，主机A状态变为Non Resposive，事件中有相关提示。
  1. 本集群或数据中心里的另一台主机B被Engine选为代理，测试主机A的状态，事件中有相关的提示。
  1. 集群里的另一台主机立即被选为SPM，重新激活存储域，存储域状态未Active。
  1. 主机B作为Engine的代理，首先执行SSH，发现连接超时，则向主机A发出执行Restart的命令，重启主机A，事件中有相关的提示。
  1. 主机A被重启，状态变化为Reboot -> Up。
1. 执行Fence成功，主机由于被代理执行启动命令而开机。

## 在另一个数据中心里执行的Fence
* 需要的条件为： 
  * 被测数据中心的集群里只有一台主机（这样才会选择另一个数据中心里的主机作为Fence代理）。
  * 环境中有另一个数据中心，这个数据中心里至少有一台可以作为Fence代理的主机。
  * 启用集群的隔离策略：【集群 -> 编辑 -> 隔离策略】，勾选Enable Fence。
  * 主机配置了电源管理。

  * 在Engine上，执行以下命令，添加other_dc选项，使其可以通过另一个数据中心执行Fence

```
  curl -X PUT -H "Accept: application/xml" -H "Content-type: application/xml" -u [Username:Password] --insecure -d '<host><power_management type="ipmilan"><pm_proxies><pm_proxy><type>dc</type></pm_proxy><pm_proxy><type>cluster</type></pm_proxy><pm_proxy><type>other_dc</type></pm_proxy></pm_proxies><agents><agent type="ipmilan"><address>192.168.3.160</address><username>ADMIN</username><options/><order>1</order></agent></agents></power_management></host>' https://[engine_ip]/api/hosts/[host_id]
```

  配置完成后，点击选择主机，点击菜单中的【编辑 -> 电源管理】，可以看到电源管理中的【源】选项中，多了一个选项为【other_dc】。


### 主机网络异常（断开）时通过另一个数据中心执行的Fence

1. 通过电源管理打开环境A的一台主机A（或ssh到主机上，但由于网络会断开，不推荐），这台主机不能是运行着HostedEngine虚拟机的主机。
1. 在主机A上，运行</code>service network stop</code>，模拟网络异常的情况。
1. 回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态，看到如下过程：
  1. 主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待80sec，事件中有相关的提示。
  1. 由于Engine连接不上主机A，主机A状态变为Non Resposive，数据中心也处于Non Responsive的状态，事件中有相关提示。
  1. 另一个数据中心B里的一台主机B被Engine选为代理，测试主机A的状态，事件中有相关的提示。
  1. 主机B作为Engine的代理，首先执行SSH，发现连接超时，则向主机A发出执行Restart的命令，重启主机A，事件中有相关的提示。
  1. 主机A被重启，状态变化为Reboot -> Up。
  1. 数据中心A恢复正常。
1. 执行Fence成功，主机由于被代理执行重启命令而重新启动。

### 主机VDSM崩溃时通过另一个数据中心执行的Fence

1. ssh到数据中心A的一台主机A上，这台主机不能是运行着HostedEngine虚拟机的主机。
1. 在主机A上，运行命令<code>service vdsmd stop</code>，模拟vdsmd服务崩溃的情况。
1. 回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态，看到如下过程：
  1. 主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待80sec，事件中有相关的提示。
  1. 由于Engine连接不上主机A，主机A状态变为Non Resposive，数据中心A也处于Non Responsive的状态。
  1. 另一个数据中心B一台主机B被Engine选为代理，测试主机A的状态，事件中有相关的提示。
  1. 主机B作为Engine的代理，执行SSH，发现能够连接，则尝试重启VDSM，重启主机A的vdsmd服务。
  1. 主机A的vdsmd服务被重启，主机状态变化为Connecting -> Non Responsive -> Up，主机恢复正常。
  1. 数据中心A恢复正常。
1. 执行Fence成功，主机由于代理执行了vdsmd服务的重启，重启了vdsmd服务，主机A重新连接到环境中。

###  主机崩溃时的通过另一个数据中心执行的Fence

1. 通过电源管理打开其中一台主机A（或ssh到主机上，但由于主机会关机，不推荐），这台主机不能是运行着HostedEngine虚拟机的主机。
1. 在主机A上，运行<code>poweroff</code> 或直接通过电源管理关机，模拟主机异常崩溃的情况。
1. 回到浏览器，点击左侧树形面板，选择【主机】，观察该主机和存储的状态，看到如下过程：
  1. 主机A与Engine失去联系，不响应，Engine尝试连接主机A，主机A状态为Connecting，等待80sec，事件中有相关的提示。
  1. 由于Engine连接不上主机A，主机A状态变为Non Resposive，事件中有相关提示。
  1. 本集群或数据中心里的另一台主机B被Engine选为代理，测试主机A的状态，事件中有相关的提示。
  1. 主机B作为Engine的代理，首先执行SSH，发现连接超时，则向主机A发出执行Restart的命令，重启主机A，事件中有相关的提示。
  1. 主机A被重启，状态变化为Reboot -> Up。
  1. 数据中心A恢复正常，主机重新连接到数据中心A中。
1. 执行Fence成功，主机由于被代理执行启动命令而开机。

