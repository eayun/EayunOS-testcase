# 电源管理的健康检查

对于配置了电源管理的主机进行电源管理健康检查的配置，定期报告主机的状况，在发生失败操作时可以发出警报。

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|1|配置电源管理的健康检查，并观察报告内容|前提条件：由于操作过程需要重启engine服务，要在Engine上启用全局维护模式<br /><br /><ol><li>SSH到Engine中，执行命令<code>engine-config -s PMHealthCheckEnabled=True</code>，启用电源管理健康检查功能（默认情况下是False，即不启用）</li><li>设置电源管理健康检查的周期，运行命令<code>engine-config -s PMHealthCheckIntervalInSec=60</code>，设置为每1分钟检查一次（默认时间间隔是3600，即1小时）</li><li>重启engine服务，运行命令<code>service ovirt-engine restart</code> 或 <code>/etc/init.d/ovirt-engine restart</code>，使配置生效</li><li>通过浏览器登录到Engine中，等待，观察事件中提示的报告</li></ol>|电源管理健康检查配置成功，每过1分钟，可以看到事件中有如下提示：<br />Host Host1 from cluster Default was chosen as a proxy to execute Status command on Host Host2.||
