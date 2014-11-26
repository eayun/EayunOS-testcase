# 创建数据中心

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|25|主机的安装|安装主机(参照安装测试)|主机安装成功|||
|26|创建数据中心|<ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，点击System选择Data Centers</li><li>点击New，显示New Data Center对话框，输入名称及其描述，选择Type</li><li>点击OK，显示New Data Center-Guide me对话框，提示配置Cluster（可以在这部直接配置Cluster也可以之后再创建Cluster）</li></ol>|数据中心列表下显示创建的数据中心|||
|27|创建集群|<ol><li>若在配置数据中心完成的最后一步显示 New Data Center-Guide me可以直接点击 Configure Cluster，若不是则可以点击菜单 栏内的Guide me显示New Data Center me点 击Configure Cluster</li><li>在New Cluster下General项内输入名称及描述</li><li>CPU Name下选择能最好描述Host的CPU（注意 默认Cluster下不需要这步）</li><li>设置Optinization及Resilience Policy、 Cluster Policy根据实际需要选择</li><li>点击OK，在New Data Center-Guide me下可以继续添加Cluster也可以配置Host也可以选 择稍后再配置</li></ol>|创建的集群会显示在数据中心Cluster列表下|||
|28|创建Host|<ol><li>若在配置集群完成的最后一步显示 New Data Center-Guide me可以直接点击Configure Host，若不是则可以点击菜单栏内的Guide me,在对话框内点击Configure Host</li><li>在New Host对话框，进行配置，输入名称、 描述、Ip地址密码，SSH Fingerprint等，还可设置电源管理</li><li>点击OK，在Host列表下可以看到状态 installing-\>Reboot-\>Awaiting-\>Up</li></ol>|创建Host成功状态为Up可用|||
|29|配置网络（Cluster）|||||
|30|配置网络（Host）|||||
|31|配置存储（NFS） |<ul><li>前提：</li></ul><ol><li>已经存在一个NFS存储</li></ol><ol><li>在左侧树形面板下点击Expand All，在System下选择数据中心点击Storage，在详细面板菜单下点击New Domain</li><li>在New Domain对话框内输入名称、选择存储域类型、Export Path等信息</li><li>点击OK,创建的存储域显示在存储列表下状态由Locked-\>Active</li></ol>|存储列表下显示创建的存储域状态Active|||
|32|配置存储（iSCSI）|<ul><li>前提：</li></ul><ol><li>已经存在一个iSCSI存储</li></ol><ol><li>在左侧树形面板下点击Expand All，在System下选择数据中心点击Storage，在详细面板菜单下点击New Domain</li><li>在New Domain对话框内输入名称、选择存储域类型、Export Path等信息</li><li>点击OK，创建的存储域显示在存储列表下状态由Locked-\>Active<br/><br/>|存储列表下显示创建的存储域状态Active|||
|33|配置ISO Domain（创建一个存在的 ISO Domain）|<ol><li>在左侧树形面板下点击Expand All，在System下选择数据中心，在右侧的数据中心列表下选择该数据中心，显示详细面板</li><li>在详细面板下选择Storage，点击菜单栏内的 Attach ISO，选择ISO Domain，点击OK</li><li>ISO Domain显示在存储列表下状态由 Locked-\>Active</li></ol>|存储列表下显示ISO Domain状态Active|||
|34|配置ISO Domain（创建一个新的ISO Domain）||ISO Domain创建成功|||

