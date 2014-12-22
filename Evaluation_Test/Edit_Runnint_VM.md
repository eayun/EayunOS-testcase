# 编辑运行中的虚拟机
* 摘要
  可以通过EayunOS4.1虚拟化管理中心编辑正在运行的虚拟机。
    * 某些修改是可以立即生效的，如名称、注释、勾选高可用等；
    * 某些修改是不能立即生效的，需要下次运行时生效，如内存、引导序列等；
    * 某些修改是可以立即生效的，但是对虚拟机有一定的影响，会询问用户是否确定修改，确定则立即生效，取消则下次运行时生效。

## 编辑虚拟机名称，注释等

1. 选择一台运行中的虚拟机（HostedEngine虚拟机除外），点击菜单中的【编辑】按键或右键选择【编辑】。
1. 在弹出的【编辑虚拟机】窗口中，修改虚拟机的名称、描述、注释，点击【确定】。
1. 看到虚拟机的名称、描述、注释被修改，虚拟机正常运行。

## 编辑虚拟机内存等

1. 选择一台运行中的虚拟机（HostedEngine虚拟机除外），点击菜单中的【编辑】按键或右键选择【编辑】。
1. 在左侧选择系统标签，修改虚拟机的内存大小，点击【确定】。
1. 弹出【下个重启配置】的确认窗口，提示：“一些改变在下一次重启后才有效”。
1. 点击【确定】，虚拟机的内存没有被修改。
1. 虚拟机名称前的图标右上角多了个标记，将鼠标放在标记上，有提示信息：“服务器在下次运行时使用新的配置”。
1. 关闭该虚拟机，虚拟机状态为Down以后，再次运行该虚拟机，看到虚拟机内存大小被修改，使用新的内存运行。

  > #### 注意
  > 此处提示的“一些改变在下一次重启后才有效”，需要将虚拟机关闭，再次运行虚拟机，而不仅仅时在虚拟机中执行reboot的操作。

## 热插入虚拟机CPU

1. 选择一台运行中的虚拟机（HostedEngine虚拟机除外），点击菜单中的【编辑】按键或右键选择【编辑】。
1. 在左侧选择系统标签，增加虚拟CPU的总数（如由2改为4），点击【确定】。
1. 弹出【下个重启配置】确认窗口，提示：“以下值可以马上被应用：-cpu”。
1. 可以点击【确定】，马上生效；也可以勾选【稍后应用】，点击【确定】后，在下次重启生效（本实验直接点击确定，使其立即生效）。
1. 编辑虚拟机成功，看到该虚拟机的【常规】子标签中的CPU内核的数量增加，说明热插入了CPU。

  > #### 注意
  > 目前仅支持CPU的热插入操作，还不支持热拔出操作，因此如果修改虚拟机CPU的总数为减少，则修改不会生效。

> #### 注意
> **编辑运行中的虚拟机**是针对单台虚拟机而言的，不能编辑虚拟机池中的虚拟机。