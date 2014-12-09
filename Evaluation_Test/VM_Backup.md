# VM Backup 

* 摘要
  * 本功能能够以一定的策略自动执行虚拟机的快照，以及虚拟机的导出操作。
  * 虚拟机备份的功能需要初始化后才能使用。

## 初始化虚拟机备份

1. SSH到EayunOS虚拟化管理端。
1. 执行命令`vm-backup-setup`，进行初始化。
1. 此时会进行一些数据库的创建操作，需要用户输入admin@internal的密码。
1. 初始化过程中，会重启engine服务、dwh&reports服务和postgresql服务，初始化完毕后，重启httpd服务，并启动vm backup服务。

  输出如下：

      stopping engine
      停止oVirt Engine:                                          [确定]
      stopping dwh&reports
      停止oVirt Engine Reports:                                  [确定]
      停止oVirt Engine Dataware House:                           [确定]
      restarting postgresql
      停止 postgresql 服务：                                     [确定]
      启动 postgresql 服务：                                     [确定]
      starting engine
      启动oVirt Engine:                                          [确定]
      starting dwh&reports
      启动oVirt Engine Reports:                                  [确定]
      启动oVirt Engine Dataware House:                           [确定]
      Restarting httpd
      停止 httpd：                                               [确定]
      正在启动 httpd：                                           [确定]
      Staring engine-vm-backup service...
      启动engine vm backup service:                 [  OK  ]
      Setup proccess completed.

  > #### 提示
  > 由于初始化会重启engine服务，如果你不希望Hosted Engine中的HA服务将EayunOS管理端虚拟机重启，请事先启用全局维护模式。

## 使用虚拟机备份

1. 点击【虚拟机】标签，选中其中一台虚拟机，点击该虚拟机下的【Vm Backup】子标签。
1. 选择【备份策略】，勾选【启用】。
1. 设置【时间计划】，并设置备份的时间。
1. 设置【备份限制】，可以是【保留备份数】或【保留备份天数】。
1. 点击【保存更改】按钮。

* 结果

  

## 虚拟机备份的选项解释

  设置虚拟机备份，需要设置备份策略、时间计划和备份限制。三者缺一不可。

  * 备份策略：备份的方式
    * 增量备份（快照）：备份操作为创建虚拟机快照，备份出来的快照的描述信息为 “Auto Backup”。
    * 完全备份：备份操作为将虚拟机导出至导出域，该虚拟机的名称为 “[原虚拟机名称]_Backup_[当前时间]”。

  * 时间计划：备份的周期
    * 按周：选择后，下方会列出一周七天的选择，选中的那一天才会在指定时间内执行相应备份策略的操作。
    * 按天：选择后，仅选择一天中执行备份的时间，且每天会执行一次。

  * 备份限制：备份保留的策略

    根据配置的保存备份数的策略，定时进行备份是否需要清理的检查。

    * 保留备份数：定时检查从所对应的备份策略（增量备份/完全备份）里创建出来的备份（快照/导出域里的虚拟机）数量是否超过保留备份数的设置，如果超过，一次删除一个日期最早的备份。
    * 保留备份天数：定时检查从所对应的备份策略（增量备份/完全备份）里创建出来的备份（快照/导出域里的虚拟机）中最老的备份的备份时间是否比设置的保留备份天数之前的时间还早，如果是的，删除该日期最早的备份。

    > #### 注意
    > 如果选择的是“增量备份（快照）”，那么根据其备份限制，需要在虚拟机处于 down 的状态下才会被删除。

