#创建一个 Windows 虚拟机来为创建模板做准备
| 编号 | 测试项 | 测试目的 | 测试步骤 | 预期结果 | 实际结果 |
|--------- | ---------- | ------------ | ------------ | ------------ | ------------ |
|**0070502**|封装一个win7虚拟机|为创建win7模板做准备|  1.在作为模板使用的虚拟机上，打开一个命令行终端，并输入 **regedit**.<br/>2.Registry Editor 窗口会被打开。在左面的框中，展开 **HKEY_LOCAL_MACHINE → SYSTEM → SETUP**。<br/>3.在主窗口中，点鼠标右键，使用 **New → String Value** 来添加一个新的字符串, **Value name** 写为 **UnattendFile**，点鼠标右键，选择修改打开编辑字符串窗口，修改**Value data** 为 **a:\sysprep.inf**。<br/>4.通过**C:\Windows\System32\sysprep\sysprep.exe** 运行 Sysprep。<br/>5.在 Sysprep 中的 **System Cleanup Action** 下，选择 **Enter System Out-of-Box-Experience (OOBE)**。如需修改系统的 ID（SID），勾选 **Generalize** 选择框。在 **Shutdown Options** 下，选择 **Shutdown**。<br/>6.点 **OK** 完成封装的过程，在封装完成后，虚拟机会被自动关闭。 |封装模板成功||
