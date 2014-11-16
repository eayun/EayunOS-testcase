# 创建数据中心

|用例编号|操作|预期结果|实际结果|备注|
|--------|----|--------|--------|----|
|25|安装主机(参照安装测试)|主机安装成功|||
|26|创建数据中心<br/><br/>1.  登录虚拟化系统，在左侧树形面板下点击 Expand All,点击System选择Data<br/>    Centers<br/><br/>2.  点击New，显示New Data Center对话框，输<br/>    入名称及其描述，选择Type（必须与该数据 中心的存储类型一致）<br/><br/>3.  点击OK，显示New Data Center-Guide me对<br/>    话框，提示配置Cluster（可以在这部直接配<br/>    置Cluster也可以之后再创建Cluster）<br/><br/>|数据中心列表下显示创建的数据中心|||
|27|创建集群<br/><br/>1.  若在配置数据中心完成的最后一步显示 New Data Center-Guide<br/>    me可以直接点击 Configure Cluster，若不是则可以点击菜单 栏内的Guide<br/>    me显示New Data Center me点 击Configure Cluster<br/><br/>2.  在New Cluster下General项内输入名称及描 述<br/><br/>3.  CPU Name下选择能最好描述Host的CPU（注意 默认Cluster下不需要这步）<br/><br/>4.  设置Optinization及Resilience Policy、 Cluster Policy根据实际需要<br/><br/>5.  点击OK，在New Data Center-Guide me下可<br/>    以继续添加Cluster也可以配置Host也可以选 择稍后再配置<br/><br/>|创建的集群会显示在数据中心Cluster列表下|||
|28|创建Host<br/><br/>1.  若在配置集群完成的最后一步显示 New Data Center-Guide me可以直接点击<br/>    Configure Host，若不是则可以点击菜单栏 内的Guide me,在对话框内点击<br/>    Configure Host<br/><br/>2.  在New Host对话框，进行配置，输入名称、 描述、Ip地址密码，SSH<br/>    Fingerprint等，还 可设置电源管理<br/><br/>3.  点击OK，在Host列表下可以看到状态 installing-\>Reboot-\>Awaiting-\>Up<br/><br/>|创建Host成功状态为Up可用|||
|29|配置网络（Cluster）<br/><br/>1.  2.  3.  ||||
|30|配置网络（Host）<br/><br/>1.  2.  3.  ||||
|31|配置存储（NFS） 前提已经存在一个NFS存储<br/><br/>1.  在左侧树形面板下点击Expand All，在<br/>    System下选择数据中心点击Storage，在详细 面板菜单下点击New Domain<br/><br/>2.  在New Domain对话框内输入名称、选择存储 域类型、Export Path等信息<br/><br/>3.  点击OK,创建的存储域显示在存储列表下状态 由Locked-\>Active<br/><br/>|存储列表下显示创建的存储域状态Active|||
|32|配置存储（ISCSI） 前提已经存在一个ISCSI存储<br/><br/>1.  在左侧树形面板下点击Expand All，在<br/>    System下选择数据中心点击Storage，在详细 面板菜单下点击New Domain<br/><br/>2.  在New Domain对话框内输入名称、选择存储 域类型、Export Path等信息<br/><br/>3.  点击OK，创建的存储域显示在存储列表下状 态由Locked-\>Active<br/><br/>|存储列表下显示创建的存储域状态Active|||
|33|配置ISO Domain（创建一个存在的 ISO Domain）<br/><br/>1.  在左侧树形面板下点击Expand All，在<br/>    System下选择数据中心，在右侧的数据中心<br/>    列表下选择该数据中心，显示详细面板<br/><br/>2.  在详细面板下选择Storage，点击菜单栏内的 Attach ISO，选择ISO<br/>    Domain，点击OK<br/><br/>3.  ISO Domain显示在存储列表下状态由 Locked-\>Active<br/><br/>|存储列表下显示ISO Domain状态Active|||
|34|配置ISO Domain（创建一个新的ISO Domain）|ISO Domain创建成功|||

