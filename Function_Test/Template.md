# 模板

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|115     |创建模板（Windows、Linux）|<ol><li>在虚拟机列表下，选择指定的虚拟机</li><li>确认虚拟机状态为Down</li><li>点击Make Template打开New Template窗口</li><li>输入名称，描述等信息</li><li>选择Host Cluster</li><li>默认选中 Allow all users to access this Template</li><li>点击OK，创建模板</li></ol>|虚拟机状态由Image Locke-\>Down 在Template列表下显示创建的模板状态由Locked-\>OK|||
|116     |删除模板（默认的Blank 模板不允许删除）|<ol><li>在模板列表下选中待删除的模板</li><li>点击Remove打开Remove Template窗口</li><li>点击OK</li></ol>|模板被删除|||
|117     |导出模板（前提：已创建好Export存储域）|<ol><li>在模板列表下，选中待导出模板</li><li>点击Export，打开Export Template窗口，选择 ForceOverride</li><li>点击OK</li></ol>|模板导出到Export存储域|||
|118     |导入模板（已存在Export域）|<ol><li>在左侧树形面板下找到Export存储域</li><li>在详细面板下选择Export存储域内的Template</li><li>选中模板，点击Import，在Import template窗口内选择Destination Cluster和Storage</li><li>清除 Clone All Templates</li><li>点击OK</li></ol>|模板成功导入到数据存储中|||
|119     |导出到另一数据中心后的模板，创建虚拟机||虚拟机创建成功，虚拟机可以正常使用|||
|120     |批量导入导出模板||可以批量导入导出模板，导出的模板可以正常使用||批量导出时只能成功一个，其它失败|

