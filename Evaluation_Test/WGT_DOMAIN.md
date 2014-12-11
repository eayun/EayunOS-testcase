# WGT_DOMAIN

* 摘要
  * EayunOS Engine Appliance初始化配置完成后，会默认创建一个WGT_DOMAIN。
  * 
  * 需要对其进行初始化以后，才能正常使用WGT_DOMAIN。

## WGT_DOMAIN初始化

1. 以engineadm用户登录到EayunOS管理端，进入Engine Console界面。
1. 按下任意键进入主配置界面，在`Choose the advanced setting:`处输入【7】，并按下【Enter】键。
1. 进入高级配置界面，在`Choose the advanced setting:`处输入【4】，并按下【Enter】键。
1. 提示输入admin@internal的密码，则输入密码并按下【Enter】键。
1. 提示`WGT_DOMAIN initialization successfully.`则说明初始化成功。
1. 按下任意键退出初始化界面，回到主配置界面。

* 结果

  WGT_DOMAIN初始化成功。

## WGT_DOMAIN的使用

1. 登录到EayunOS虚拟化管理端，点击【存储】选项卡。
1. 在出现的存储列表中，看到WGT_DOMAIN处于Unattach状态，选择WGT_DOMAIN，并点击其下的【数据中心】子选项卡。
1. 点击【数据中心】子选项卡菜单中的【附加】按键。
1. 在弹出的【附加到数据中心】对话框中，勾选要附加到的数据中心，并点击【确定】。
1. WGT_DOMAIN处于激活中的状态，附加成功后，状态变为【Active】。
1. 点击【映像】子选项卡，看到默认包含`WGT-3.5_5.iso`。

* 结果

  WGT_DOMAIN附加成功，能够正常使用。

> #### 提示
> WGT_DOMAIN是一个ISO域，如果你想使用这个ISO域中的其他镜像，则使用ISO上传工具上传iso镜像到该域，即可使用。详情请参考【ISO上传工具】。
