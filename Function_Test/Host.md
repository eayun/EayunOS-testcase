# 主机

|用例编号|操作|预期结果|实际结果|备注|
|--------|----|--------|--------|----|
|98|添加Host（管理系统注册方式）<br/><br/>1.  若在配置集群完成的最后一步显示 New Data Center-Guide me可以直接点击<br/>    Configure Host，若不是则可以点击菜单栏内的 Guide<br/>    me,在对话框内点击Configure Host<br/><br/>2.  在New Host对话框，进行配置，输入名称、描 述、Ip地址密码，SSH<br/>    Fingerprint等，还可设置 电源管理<br/><br/>3.  点击OK，在Host列表下可以看到状态 installing-\>Reboot-\>Awaiting-\>Up<br/><br/>|添加Host成功|||
|99|添加Host（Console注册方式）<br/><br/>1.  安装Host完成后在Console界面下配置Status、<br/>    Network、Security、oVirt-Engine（ip及端口号 设置80）保存设置<br/><br/>2.  在系统管理平台Host列表下，会显示该Host，点<br/>    击菜单Approve，可以设置电源管理等，点击OK, Host 列表下可以看到状态<br/>    installing-\>Reboot-\>Awaiting-\>Up<br/><br/>|添加Host成功|||
|100|配置Host电源管理<br/><br/>1.  在虚拟化管理系统左侧树形面板下选择 Expand All-\>System<br/>    在右侧详细面板中选择 Hosts，选择待配置电源管理的host，点击菜单内<br/>    的edit，在Edit Host界面下的 Power<br/>    Management,输IPMI的ip地址、用户名及密<br/>    码、Type，点击Test，提示success<br/><br/>|提示success，电源管理配置成功，可以通过电源管理对主 机进行重启关机等操作|||
|101|配置及更换主机SPM<br/><br/>1.  在虚拟化管理系统左侧树形面板下选择 Expand All-\>System<br/>    在右侧详细面板中选择 Hosts，选择待配置SPM的host，点击菜单内的<br/>    edit，在Edit Host界面下的SPM,分别设置优先级 （Low、Normal、High）<br/><br/>2.  观察实际使用<br/><br/>|SPM设置成功|||
|102|维护主机<br/><br/>1.  在虚拟化管理系统左侧树形面板下选择 Expand All-\>System<br/>    在右侧详细面板中选择 Hosts，选择待维护的host，点击菜单内的<br/>    Maintenance,弹出Maintenance Host(s)确认框， 点击OK<br/><br/>2.  列表下该Host状态 Preparing Maintenance-\>Maintenance<br/><br/>|主机进入维护模式|||
|103|激活主机<br/><br/>1.  在Host列表下，选择已被设置成Maintenance模式<br/>    的Host，点击菜单内的Active<br/><br/>2.  Host状态Unassigned-\>Up<br/><br/>|主机激活成功|||
|104|删除主机（前提主机不是non-responsive、没有磁盘卷、 主机本身不是存储域（本地数存储就属于这种情况）<br/><br/>1.  在Host列表下，选择待删除的Host，将其置成 Maintenance，点击Remove<br/><br/>|Host成功被删除|||
|105|强制删除主机（前提主机是non-responsive、没有磁盘 卷、主机本身不是存储域（本地数存储就属于这种情况） 中任意一种<br/><br/>1.  在Host列表下，选择待删除的Host，将其置成<br/>    Maintenance，点击Remove，再选中 Force Remove，点击OK<br/><br/>|Host成功被删除|||

