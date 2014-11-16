# 事件通知

|用例编号|操作|预期结果|实际结果|备注|
|--------|----|--------|--------|----|
|173|添加事件通知功能（前提：已经安装了MTA agent）<br/><br/>1.  登录虚拟化系统，在左侧树形面板下点击 Expand<br/>    All,点击System，在右侧详细面板菜单内 点击Users<br/><br/>2.  选中用户列表下的用户<br/><br/>3.  在该用户详细面板下点击Event Notifier，点击 Manage Events，打开Add<br/>    Event Notification 窗口<br/><br/>4.  选择需要通知的事项，填充邮件地址<br/><br/>5.  点击OK<br/><br/>6.  ssh登录到manager节点，开启服务<br/><br/>        # chkconfig --add ovirt-engine-notifier<br/>        # chkconfig ovirt-engine-notifier on<br/>        # service ovirt-engine-notifier restart<br/>                                            <br/><br/>|当系统出现问题会自动发到填写的邮箱内|||
|174|取消事件通知<br/><br/>1.  登录虚拟化系统，在左侧树形面板下点击 Expand<br/>    All,点击System，在右侧详细面板菜单内 点击Users<br/><br/>2.  选中用户列表下的用户<br/><br/>3.  在该用户详细面板下点击Event Notifier，点击 Manage Events，打开Add<br/>    Event Notification窗 口<br/><br/>4.  清除所有所选的事件（删除通知）<br/><br/>5.  点击OK<br/><br/>|邮件将不再自动发送通知|||<br/>||1.  2.  3.  4.  5.  6.  ||||<br/>|...|...<br/><br/>...|...|||<br/><br/>> **Note**<br/>><br/>> 其他注意事项：

