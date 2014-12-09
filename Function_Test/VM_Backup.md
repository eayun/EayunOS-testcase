# VM Backup 

* 摘要
  * 本功能能够以一定的策略自动执行虚拟机的快照，以及虚拟机的导出操作。
  * 虚拟机备份的功能需要初始化后才能使用。


|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|1       |初始化虚拟机备份|<ol><li>SSH到EayunOS虚拟化管理端</li><li>执行命令`vm-backup-setup`，进行初始化</li><li>当出现输入admin@internal密码的提示时，输入密码，并按下【Enter】键</li></li>等待初始化完成</li></ol>|<ol><li>进行一些数据库的创建操作</li><li>会重启engine服务、dwh&reports服务和postgresql服务，初始化完毕后，重启httpd服务，并启动vm backup服务</li></ol>|||
|2       |使用虚拟机备份（增量备份）|点击【虚拟机】标签，选中其中一台虚拟机，点击该虚拟机下的【Vm Backup】子标签</li><li>选择【备份策略】为增量备份，勾选【启用】</li><li>设置【时间计划】，并设置备份的时间</li><li>设置【备份限制】，可以是【保留备份数】或【保留备份天数】</li><li>点击【保存更改】按钮</li></ol>|</ol><li>备份设置保存成功，弹出saved的提示，点击【确定】</li><li>当虚拟机发生一次备份后，会创建一份快照，可以在【快照】子标签中看到备份的快照，描述为`Auto Backup`</ol>||如果选择的时间计划为【按周】，则需要勾选星期|
|3       |使用虚拟机备份（完全备份）|点击【虚拟机】标签，选中其中一台虚拟机，点击该虚拟机下的【Vm Backup】子标签</li><li>选择【备份策略】为完全备份，勾选【启用】</li><li>设置【时间计划】，并设置备份的时间</li><li>设置【备份限制】，可以是【保留备份数】或【保留备份天数】</li><li>点击【保存更改】按钮</li></ol>|</ol><li>备份设置保存成功，弹出saved的提示，点击【确定】</li></ol>||如果选择的时间计划为【按周】，则需要勾选星期|