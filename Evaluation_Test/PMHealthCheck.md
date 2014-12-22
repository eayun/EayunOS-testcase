# 电源管理健康检查
* 摘要
  对于配置了电源管理的主机进行电源管理健康检查的配置，定期报告主机的状况，在发生失败操作时可以发出警报。

1. SSH到Engine中，执行如下命令，启用电源管理健康检查的功能（默认情况下是False，即不启用）`engine-config -s PMHealthCheckEnabled=True`。
1. 设置电源管理健康检查的周期（默认是3600秒，即1小时），运行命令`engine-config -s PMHealthCheckIntervalInSec=60`（设置为1分钟一次）。
1. 重启Engine，使配置生效，运行命令`service ovirt-engine restart`或`/etc/init.d/ovirt-engine restart`。
1. 登录到Engine管理端中，等待，每分钟能够看到事件中提示：`Host Host1 from cluster Default was chosen as a proxy to execute Status command on Host Host2.`。
