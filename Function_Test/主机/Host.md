# 主机

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|1|添加Host（管理系统注册方式）|<ol><li>若在配置集群完成的最后一步显示 New Data Center-Guide me可以直接点击Configure Host，若不是则可以点击菜单栏内的Guide me，在对话框内点击Configure Host</li><li>在New Host对话框，进行配置，输入名称、描述、Ip地址密码，点击高级参数获取SSH Fingerprint等，还可设置电源管理</li><li>点击OK，在Host列表下可以看到状态Installing -> Initializing -> Up</li></ol>|添加Host成功|Ok||
|2|添加Host（Console注册方式）|<ol><li>安装Host完成后在Console界面下配置Status、Network、Security、oVirt-Engine（ip及端口号 设置80）保存设置</li><li>在系统管理平台Host列表下，会显示该Host，点击菜单Approve，可以设置电源管理等，点击OK, Host 列表下可以看到状态Installing -> Initializing -> Up</li></ol>|添加Host成功|Ok||
|3|配置Host电源管理|<ol><li>在虚拟化管理系统左侧树形面板下选择Expand All-\>System在右侧详细面板中选择 Hosts，选择待配置电源管理的host，点击菜单内的edit，在Edit Host界面下的Powerx Management,输IPMI的ip地址、用户名及密码、Type，点击Test，提示success</li></ol>|提示success，电源管理配置成功，可以通过电源管理对主 机进行重启关机等操作|||
|4|配置及更换主机SPM|<ol><li>在虚拟化管理系统左侧树形面板下选择Expand All-\>System在右侧详细面板中选择Hosts，选择待配置SPM的host，点击菜单内的edit，在Edit Host界面下的SPM,分别设置优先级（Low、Normal、High）</li><li>观察实际使用</li></ol>|SPM设置成功|||
|5|维护主机|<ol><li>在虚拟化管理系统左侧树形面板下选择 Expand All-\>System在右侧详细面板中选择 Hosts，选择待维护的host，点击菜单内的Maintenance,弹出Maintenance Host(s)确认框， 点击OK</li><li>列表下该Host状态 Preparing Maintenance-\>Maintenance</li></ol>|主机进入维护模式|||
|6|激活主机|<ol><li>在Host列表下，选择已被设置成Maintenance模式的Host，点击菜单内的Active</li><li>Host状态Unassigned-\>Up</li></ol>|主机激活成功|||
|7|删除主机|<ul><li>前提：</li></ul><ol><li>主机不是non-responsive、没有磁盘卷、主机本身不是存储域（本地数存储就属于这种情况）</li><ol><ul><li>操作：</li></ul><ol><li>在Host列表下，选择待删除的Host，将其置成 Maintenance，点击Remove</li></ol>|Host成功被删除|||
|8|强制删除主机|<ul><li>前提：</li></ul><ol><li>主机是non-responsive、没有磁盘卷、主机本身不是存储域（本地数存储就属于这种情况） 中任意一种</li></ol><ul><li>操作：</li></ul><ol><li>在Host列表下，选择待删除的Host，将其置成Maintenance，点击Remove，再选中Force Remove，点击OK</li></ol>|Host成功被删除|||

