# 事件通知

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|173|添加事件通知功能|<ul><li>前提：</li></ul><ol><li>已经安装了MTA agent</li></ol><ul><li>操作：</li></ul><ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，点击System，在右侧详细面板菜单内点击Users</li><li>选中用户列表下的用户</li><li>在该用户详细面板下点击Event Notifier，点击 Manage Events，打开Add Event Notification窗口</li><li>选择需要通知的事项，填充邮件地址</li><li>点击OK</li><li>ssh登录到manager节点，开启服务<code>chkconfig --add ovirt-engine-notifier</code>、<code>chkconfig ovirt-engine-notifier on</code>、<code>service ovirt-engine-notifier restart</code></li></ol>|当系统出现问题会自动发到填写的邮箱内|||
|174|取消事件通知|<ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，点击System，在右侧详细面板菜单内 点击Users</li><li>选中用户列表下的用户</li><li>在该用户详细面板下点击Event Notifier，点击 Manage Events，打开Add Event Notification窗口</li><li>清除所有所选的事件（删除通知）</li><li>点击OK</li></ol>|邮件将不再自动发送通知|||

**Note**<br/>><br/>> 其他注意事项：

