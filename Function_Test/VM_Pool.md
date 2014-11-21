# 虚拟机池

|用例编号|操作|预期结果|实际结果|备注|
|--------|----|--------|--------|----|
|152|创建虚拟机池（前提：已有模板）<br/><br/>1.  在管理系统平台详细面板下点击Pools，打开 New Pool窗口<br/><br/>2.  设置Host Cluster、Template、操作系统、 optimized for、VMs的数量、<br/>    Maximum number of VMs per user及名称描述等 信息<br/><br/>3.  点击Show Advanced Options，填充每项内的信息 等<br/><br/>4.  完成全部设置后，点击OK，创建虚拟机池<br/><br/>|虚拟机列表下显示创建的虚拟机，数量为虚拟机池设置的 数量，同时显示特殊标识，区别于单独的虚拟机|||
|153|Prestarting Virtual Machines in a Pool<br/><br/>1.  点击Pools，在虚拟机池列表下，选定虚拟机池<br/><br/>2.  点击Edit ，打开Edit Pool窗口<br/><br/>3.  Prestarted VMs这项输入启动虚拟机的数量<br/><br/>4.  pool 项下的Pool Type确保设置为Automatic<br/><br/>5.  点击OK<br/><br/>|虚拟机列表下显示启动的虚拟机池内的指定数量的虚拟机 状态为UP|||
|154|添加虚拟机到虚拟机池<br/><br/>1.  点击Pools，在虚拟机池列表下，选定虚拟机池<br/><br/>2.  点击Edit ，打开Edit Pool窗口<br/><br/>3.  Increase number of VMs in pool by这项输入增 加的虚拟机的数量<br/><br/>4.  点击OK<br/><br/>|虚拟机列表显示创建增加的虚拟机|||
|155|从虚拟机池中分离虚拟机<br/><br/>1.  点击Pools，在虚拟机池列表下，选定虚拟机池<br/><br/>2.  确保待分离的虚拟机为关闭状态，状态为Down<br/><br/>3.  在虚拟机池详细面板下，点击 Virtual Machines，选中列表下的虚拟机，点<br/>    击Detach<br/><br/>4.  在Detach Virtual Machine（s）对话框，点击OK<br/><br/>|从虚拟机池分离出来，虚拟机图标显示为正常独立的虚拟机|||
|156|删除虚拟机池<br/><br/>1.  点击Pools,在虚拟机池列表下，选定虚拟机池<br/><br/>2.  点击Remove ，打开Remove Pool（s）<br/><br/>3.  点击OK<br/><br/>|虚拟机池被删除|||
|157|UserRole用户在用户门户下，使用虚拟机池分配虚拟机|分配虚拟机成功同时虚拟机开启|||
|158|UserRole用户在用户门户下，虚拟机释放回虚拟机池|关闭虚拟机，虚拟机在用户门户界面下消失，虚拟机释放回虚拟机池。|||

