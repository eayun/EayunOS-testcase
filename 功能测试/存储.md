# 存储

|用例编号|操作|预期结果|实际结果|备注|
|--------|----|--------|--------|----|
|106|配置存储（NFS类型的DataDomain）前提已经存在一个NFS 存储<br/><br/>1.  在左侧树形面板下点击Expand All，在System下<br/>    选择数据中心点击Storage，在详细面板菜单下点 击New Domain<br/><br/>2.  在New Domain对话框内输入名称、选择存储域类 型、Export Path等信息<br/><br/>3.  点击OK,创建的存储域显示在存储列表下状态由 Locked-\>Active<br/><br/>|创建NFS类型的Data Domain成功|||
|107|配置存储（ISCSI类型的Data Domain） 前提已经存在一个ISCSI存储<br/><br/>1.  在左侧树形面板下点击Expand All，在System下<br/>    选择数据中心点击Storage，在详细面板菜单下点 击New Domain<br/><br/>2.  在New Domain对话框内输入名称、选择存储域类 型、Export Path等信息<br/><br/>3.  点击OK，创建的存储域显示在存储列表下状态由 Locked-\>Active<br/><br/>|创建ISCSI类型的Data Domain成功|||
|108|配置ISO Domain（创建一个存在的ISO Domain）<br/><br/>1.  在左侧树形面板下点击Expand All，在System下<br/>    选择数据中心，在右侧的数据中心列表下选择该 数据中心，显示详细面板<br/><br/>2.  在详细面板下选择Storage，点击菜单栏内的 Attach ISO，选择ISO<br/>    Domain，点击OK<br/><br/>3.  ISO Domain显示在存储列表下状态由 Locked-\>Active<br/><br/>|ISO Domain创建成功|||
|109|配置Export Domain<br/><br/>1.  在左侧树形面板下点击Expand All，在System下<br/>    选择数据中心，在右侧的数据中心列表下选择该 数据中心，显示详细面板<br/><br/>2.  在详细面板下选择Storage，点击菜单栏内的 Attach Export，选择Export<br/>    Domain，点击OK<br/><br/>3.  Export Domain显示在存储列表下状态由 Locked-\>Active<br/><br/>|Export Domain创建成功|||
|110|分离(Export Domain、ISO Domain、DataDomain）<br/><br/>1.  在Storage列表下，选择指定的存储域<br/><br/>2.  在Storage的详细面板下选择Data Center，将要<br/>    脱离的数据中心修改为Maintenance模式<br/><br/>3.  点击Detach<br/><br/>|存储域分离出数据中心|||
|111|维护存储域<br/><br/>1.  在Storage列表下，选择指定的存储域<br/><br/>2.  关闭并且移走运行在该存储域下的所有的虚拟机<br/><br/>3.  在Storage详细面板下点击Data Center<br/><br/>4.  点击Maintenance<br/><br/>|存储域设置为Maintenance模式|||
|112|激活存储域<br/><br/>1.  在Storage列表下，选择指定的存储域<br/><br/>2.  在Storage详细面板下点击Data Center<br/><br/>3.  点击Active<br/><br/>|存储域被激活|||
|113|Destroy存储域<br/><br/>1.  在Storage列表下，选择指定的存储域<br/><br/>2.  右键该存储域选择Destroy，在弹出的 Destroy Storage Domain选择 Approve<br/>    operation<br/><br/>3.  点击OK<br/><br/>|存储域被Destroy|||
|114|删除存储域<br/><br/>1.  在Storage列表下，选择指定的存储域<br/><br/>2.  将该存储域变为Maintenance模式<br/><br/>3.  将该存储域与数据中心Detach<br/><br/>4.  点击Remove，在Remove Storage确认框选择一个 host从列表下<br/><br/>5.  点击OK<br/><br/>|存储域被删除|||

