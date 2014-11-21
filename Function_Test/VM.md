# 虚拟机

|用例编号|操作|预期结果|实际结果|备注|
|--------|----|--------|--------|----|
|121|前提：虚拟化平台至少有一个Host及ISO domain 创建Red Hat Enterprise Linux server<br/><br/>1.  登录虚拟化系统，在左侧树形面板下点击 Expand<br/>    All,选择Default数据中心下Default集群 下点击VMs ,<br/>    在右侧虚拟机列表下点击菜单栏内 的New<br/>    VM,输入名称、内存大小、选择操作系统为 RedHat Enterprise Linux6.X<br/>    X64、其他项保持 默认设置，点击OK<br/><br/>2.  弹出“New Virtual Machine-Guide Me”窗口，提<br/>    示配置虚拟机磁盘，设置磁盘大小，网络接口默<br/>    认VirtIO，点击OK（根据需要可以再添加磁盘） 点击configure<br/>    Later，创建的虚拟机显示在虚拟 机列表下,安装操作系统（若采用run<br/>    once方式安 装添加CD则不需要changeCD）<br/><br/>|创建的虚拟机成功，虚拟机可以正常使用|||
|122|前提：虚拟化平台至少有一个Host及ISO domain 创建Windows虚拟机（win7 64）<br/><br/>1.  登录虚拟化系统，在左侧树形面板下点击 Expand<br/>    All,选择Default数据中心下Default集群 下点击VMs ,<br/>    在右侧虚拟机列表下点击菜单栏内 的New<br/>    VM,输入名称、内存大小、选择操作系统为 windows7 X64、Optimized<br/>    for项选择Desktop其 他项保持默认设置，点击OK<br/><br/>2.  弹出“New Virtual Machine-Guide Me”窗口，提<br/>    示配置虚拟机磁盘，设置磁盘大小，网络接口默<br/>    认VirtIO，点击OK（根据需要可以再添加磁盘） 点击configure<br/>    Later，创建的虚拟机显示在虚拟<br/>    机列表下,安装操作系统（安装到选择自定义项时<br/>    在管理平台上changeCD添加驱动，回到安装界面<br/>    刷新界面可以看到安装的磁盘，再到管理平台<br/>    changeCD加载系统安装盘，开始正常安装操作系<br/>    统）（安装完系统后changeCD）（若采用 run<br/>    once方式安装添加CD则不需要changeCD）<br/><br/>|创建的虚拟机成功，虚拟机可以正常使用|||
|123|登录虚拟机（前提：已安装SPICE）<br/><br/>1.  在虚拟机列表下选择运行的虚拟机，点击 console按钮（绿色电脑图标）<br/><br/>|登录虚拟机|||
|124|shut down 虚拟机<br/><br/>1.  在虚拟机列表下选择运行的虚拟机，点击菜单内 的shut<br/>    down或者右键菜单中选择shut down<br/><br/>|虚拟机状态变为Down|||
|125|power off虚拟机<br/><br/>1.  1 在虚拟机列表下选择运行的虚拟机，右键菜单 中选择power off<br/><br/>|虚拟机关机Down|||
|126|删除虚拟机<br/><br/>1.  在虚拟机列表下选择状态为Down的虚拟机（或将 要删除的虚拟机关机）<br/><br/>2.  点击Remove，弹出Remove Virtual Machine（s） 窗口<br/><br/>3.  点击OK<br/><br/>|虚拟机被删除|||
|127|暂停虚拟机<br/><br/>1.  在虚拟机列表下选择运行的虚拟机，点击菜单内<br/>    的suspend或者右键菜单中选择suspend<br/><br/>2.  虚拟机暂停状态Paused<br/><br/>|虚拟机被暂停|||
|128|运行状态的虚拟机创建快照<br/><br/>1.  在虚拟机列表下选中运行的虚拟机<br/><br/>2.  在虚拟机详细面板菜单Snapshots下点击Create,<br/>    在弹出的界面输入描述，保存，点击OK<br/><br/>|快照创建成功，快照可以正常使用。||Tasks列表下显示创建快照失败，但实际上快照创建完成并可以正常工作|
|129|关闭状态虚拟机创建快照<br/><br/>1.  在虚拟机列表下选中关闭状态的虚拟机<br/><br/>2.  在虚拟机详细面板菜单Snapshots下点击Create,在弹出的界面输入描述，保存，点击OK<br/><br/>|快照创建成功，快照可以正常使用|||
|130|使用快照恢复虚拟机<br/><br/>1.  在虚拟机列表里选择指定虚拟机<br/><br/>2.  将虚拟机关机状态powered down<br/><br/>3.  在虚拟机详细面板中点击菜单内的Snapshots，选 择待恢复的快照<br/><br/>4.  点击Preview,虚拟机状态由Image Locked-\>Down<br/><br/>5.  点击Commit,虚拟机状态由Image Locked-\>Down<br/><br/>|虚拟机恢复到快照|||
|131|导出虚拟机（已创建Export存储域）<br/><br/>1.  在虚拟机列表下，选中待导出的虚拟机，关闭这 些虚拟机<br/><br/>2.  点击Export，打开Export Virtual Machine(s)窗口，选择 ForceOverride<br/><br/>3.  点击OK<br/><br/>|虚拟机被导出到Export存储域|||
|132|导入虚拟机（已创建Export存储域）<br/><br/>1.  在左侧树形面板下找到Export存储域<br/><br/>2.  在详细面板下选择Export存储域内的虚拟机导入 列表<br/><br/>3.  选中这些虚拟机，点击Import，在 Import virtual machine（s）窗口内选择<br/>    Destination Cluster和Storage<br/><br/>4.  选择Collapse All Snapshots<br/><br/>5.  点击OK<br/><br/>|虚拟机被导入到数据存储域中|||
|133|批量导入导出虚拟机|可以批量导入导出虚拟机，虚拟机可以正常使用||批量导出虚拟机时，只能成功一个，其它的虚拟机都失败|

