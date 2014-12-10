# Host USB

* 摘要
  * ...
  * Host USB使用的条件为：
    * 虚拟机设置为不允许迁移
    * 虚拟机处于运行状态

## Host USB的使用

1. 点击【虚拟机】选项卡，在右侧的虚拟机列表中，选择一台设置为**不允许迁移**的虚拟机。
1. 点击该虚拟机的【Host Usb】子选项卡，列出可用的usb列表。
1. 选择要使用的usb设备，点击Action列中的【Attach】按钮，附加一个usb设备。
1. 附加成功后，Action列中的【Attach】按钮变为【Dettach】；VM列中显示使用该usb设备的虚拟机的名称。

> #### 提示
> 在没有Dettach USB设备的情况下关闭虚拟机，USB设备会被自动Dettach。

> #### 提示
> 一个USB设备只能被一台虚拟机使用。当USB设备被其他虚拟机使用时，Action列中的按钮会变为【Disable】。

