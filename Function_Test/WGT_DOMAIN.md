# WGT_DOMAIN

* 摘要
  * EayunOS Engine Appliance初始化配置完成后，会默认创建一个WGT_DOMAIN。
  * 需要对其进行初始化以后，才能正常使用WGT_DOMAIN。


|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|1       |WGT_DOMAIN的初始化|<ol><li>以engineadm用户登录到EayunOS管理端，进入Engine Console界面</li><li>按下任意键进入主配置界面，在`Choose the advanced setting:`处输入【7】，并按下【Enter】键</li><li>进入高级配置界面，在`Choose the advanced setting:`处输入【4】，并按下【Enter】键</li><li>提示输入admin@internal的密码，则输入密码并按下【Enter】键</li></ol>|<ol><li>提示`WGT_DOMAIN initialization successfully.`，说明初始化成功</li><li>按下任意键退出初始化界面，回到主配置界面</li><li>WGT_DOMAIN初始化成功，可以被附加到数据中心</li></ol>|与预期结果一致||
|2       |WGT_DOMAIN的使用|<ol><li>登录到EayunOS虚拟化管理端，点击【存储】标签</li><li>在出现的存储列表中，看到WGT_DOMAIN处于Unattach状态，选择WGT_DOMAIN，并点击其下的【数据中心】子标签</li><li>点击【数据中心】子标签菜单中的【附加】按键</li><li>在弹出的【附加到数据中心】对话框中，勾选要附加到的数据中心，并点击【确定】</li></ol>|<ol><li>WGT_DOMAIN附加成功，状态变化为Activing（Initializing?） -> Active</li><li>点击【映像】子标签，看到默认包含`WGT-3.5_5.iso`</li><li>WGT_DOMAIN中的映像可以使用</li></ol>|与预期结果一致|WGT_DOMAIN是一个ISO域，如果你想使用这个ISO域中的其他镜像，则使用ISO上传工具上传iso镜像到该域，即可使用。详情请参考【ISO上传工具】|

> #### 提示
> 由于WGT_DOMAIN是一个ISO域，该域的其他测试用例域普通ISO域相同，在这里不再重复。
