# 存储

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|106|配置存储（NFS类型的DataDomain）|<ul><li>前提：</li></ul><ol><li>已经存在一个NFS 存储</li></ol><ul><li>操作：</li></ul><ol><li>在左侧树形面板下点击Expand All，在System下选择数据中心点击Storage，在详细面板菜单下点 击New Domain</li><li>在New Domain对话框内输入名称、选择存储域类型、Export Path等信息</li><li>点击OK，创建的存储域显示在存储列表下状态由 Locked-\>Active</li></ol>|创建NFS类型的Data Domain成功|||
|107|配置存储（iSCSI类型的Data Domain）|<ul><li>前提：</li></ul><ol><li>已经存在一个iSCSI存储</li></ol><ul><li>操作：</li></ul><ol><li>在左侧树形面板下点击Expand All，在System下选择数据中心点击Storage，在详细面板菜单下点击New Domain</li><li>在New Domain对话框内输入名称、选择存储域类型、Export Path等信息</li><li>点击OK，创建的存储域显示在存储列表下状态由 Locked-\>Active</li></ol>|创建ISCSI类型的Data Domain成功|||
|108|配置ISO Domain（创建一个存在的ISO Domain）|<ol><li>在左侧树形面板下点击Expand All，在System下选择数据中心，在右侧的数据中心列表下选择该数据中心，显示详细面板</li><li>在详细面板下选择Storage，点击菜单栏内的Attach ISO，选择ISO Domain，点击OK</li><li>ISO Domain显示在存储列表下状态由 Locked-\>Active</li></ol>|ISO Domain创建成功|||
|109|配置Export Domain|<ol><li>在左侧树形面板下点击Expand All，在System下选择数据中心，在右侧的数据中心列表下选择该数据中心，显示详细面板</li><li>在详细面板下选择Storage，点击菜单栏内的Attach Export，选择Export Domain，点击OK</li><li>Export Domain显示在存储列表下状态由 Locked-\>Active</li></ol>|Export Domain创建成功|||
|110|分离(Export Domain、ISO Domain、DataDomain）|<ol><li>在Storage列表下，选择指定的存储域</li><li>在Storage的详细面板下选择Data Center，将要脱离的数据中心修改为Maintenance模式</li><li>点击Detach</li></ol>|存储域分离出数据中心|||
|111|维护存储域|<ol><li>在Storage列表下，选择指定的存储域</li><li>关闭并且移走运行在该存储域下的所有的虚拟机</li><li>在Storage详细面板下点击Data Center</li><li>点击Maintenance</li></ol>|存储域设置为Maintenance模式|||
|112|激活存储域|<ol><li>在Storage列表下，选择指定的存储域</li><li>在Storage详细面板下点击Data Center</li><li>点击Active</li></ol>|存储域被激活|||
|113|Destroy存储域|<ol><li>在Storage列表下，选择指定的存储域</li><li>右键该存储域选择Destroy，在弹出的 Destroy Storage Domain选择 Approve operation</li><li>点击OK</li></ol>|存储域被Destroy|||
|114|删除存储域|<ol><li>在Storage列表下，选择指定的存储域</li><li>将该存储域变为Maintenance模式</li><li>将该存储域与数据中心Detach</li><li>点击Remove，在Remove Storage确认框选择一个 host从列表下</li><li>点击OK</li></ol>|存储域被删除|||

