# 集群

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|94|创建集群|<ol><li>若在配置数据中心完成的最后一步显示 New Data Center-Guide me可以直接点击 Configure Cluster，若不是则可以点击菜单栏内 的Guide me显示New Data Center - Guide me点击 Configure Cluster</li><li>在New Cluster下General项内输入名称及描述</li><li>CPU Name下选择能最好描述Host的CPU（注 意默认Cluster下不需要这步）</li><li>设置Optimization及Resilience Policy、Cluster Policy根据实际需要</li><li>点击OK，在New Data Center-Guide me下可以继续添加Cluster也可以配置Host也可以选择稍后再配置</li></ol>|创建集群成功|||
|95|编辑集群|<ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All,点击System，在右侧详细面板点击Clusters,选择待编辑的集群</li><li>点击edit，编辑选项</li><li>点击OK</li></ol>|集群修改成功|||
|96|添加一个存在的集群|<ol><li>删除某一数据中心</li><li>在左侧树形面板下点击Expand All ，点击System，在右侧详细面板点击Clusters ,选中被删除数据中心遗留下的Cluster，点击 edit 重新设置，选择数据中心等</li><li>点击OK</li></ol>|集群被成功添加进其它数据中心|||
|97|删除集群|<ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，点击System，在右侧详细面板点击Clusters，选择待删除的集群</li><li>点击Remove</li><li>点击OK</li></ol>|集群被成功删除|||

