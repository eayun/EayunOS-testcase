# 数据中心

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|87      |创建数据中心|<ol><li>登录虚拟化系统，在左侧树形面板下点击Expand All，点击System选择Data Centers</li><li>点击New，显示New Data Center对话框，输入名称及其描述，选择Type（必须与该数据中心的存 储类型一致）</li><li>点击OK，显示New Data Center-Guide me对话框，提示配置Cluster（可以在这部直接配置Cluster也可以之后再创建Cluster）</li></ol>|数据中心创建成功|||
|88      |编辑数据中心|<ol><li>登录虚拟化系统，在左侧树形面板下点击Expand All，点击System选择Data Centers</li><li>在右侧详细面板下选择待编辑的的数据中心（激活状态），点击edit（Type项不可编辑）编辑其它选项</li><li>点击OK</li></ol>|Type类型不可编辑刷新界面可以看到数据中心修改成功|||
|89      |编辑数据中心|<ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，点击System选择Data Centers</li><li>在右侧详细面板下选择待编辑的数据中心（未初始化状态），点击edit（Type项可编辑）编辑其它选项</li><li>点击OK</li></ol>|Type类型可以编辑，刷新界面可以看到数据中心修改成功|||
|90      |编辑数据中心|<ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，点击System选择Data Centers</li><li>在右侧详细面板下选择待编辑的数据中心（无响应状态），点击edit（Type项不可编辑）编辑其 它选项</li><li>点击OK</li></ol>|Type类型不可编辑，刷新界面可以看到数据中心修改成功|||
|91      |删除数据中心|<ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，点击System选择Data Centers</li><li>在右侧详细面板下选择待编辑的数据中心（未初始化状态），无存储或存储域为maintenace,点击remove</li><li>点击OK</li></ol>|数据中心被删除|||
|92      |强制删除数据中心|<ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，点击System选择Data Centers</li><li>在右侧详细面板下选择待编辑的数据中心（无响应状态），同时该数据中心下有Host，点击 Force Remove</li><li>点击OK</li></ol>|数据中心被删除|||
|93      |强制删除数据中心|<ol><li>登录虚拟化系统，在左侧树形面板下点击 Expand All，点击System选择Data Centers</li><li>在右侧详细面板下选择待编辑的数据中心（无响应状态），同时该数据中心没有Host但有存储，点击Force Remove</li><li>点击OK</li></ol>|数据中心不能被删除提示无Host|||

