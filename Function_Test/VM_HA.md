# 虚拟机高可用

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|145     ||<ul><li>前提：</li></ul><ol><li>配置电源管理禁用Cluster policy(设置为None)虚拟机配置High Availability（只有服务器版本的虚拟机可以配置）</li></ol><ul><li>操作：</li></ul><ol><li>登录系统在左侧树形面板选择Expand All-\>System，在右侧详细面板菜单中选择Virtual Mchines，点击Edit</li><li>在Edit Server Virtual Machine对话框 High Availability-\> Priority for Run/Migration queue 选中High，勾选中Highly Available项</li></ol>|设置成功。选择虚拟机，在详情面板下常规标签内“高度可 用的”显示为“是”|||
|146     |Host-Initated reboot|<ol><li>登录系统在树形面板下选择VMs，高可用的虚拟机显示在虚拟机详细列表下</li><li>在树形面板选择Hosts，可用的Hosts显示在Hosts的详细列表下，选择其中一台Host，点击 Power Management下拉菜单内选择Restart，在 Restart Host对话框内点击OK，主机状态变为 Reboot-\>Non-Responsive</li><li>Host正在重启中，观察运行在这个Host上的虚拟机，在树形面板下点击VMs,显示虚拟机列表，虚拟机在Host重启完成后shut down状态 最后虚拟机是在另一台host重启起来</li></ol>|高可用的虚拟机在另外的 Host 启动|||
|147     |Virtual Machine Interruption|<ol><li>在host上运行多个虚拟机，并把其中一些设置为高可用</li><li>在host上登录终端，使用vdsClient命令，查看 进程列表</li><li>根据虚拟机的进程id，使用“kill -9”杀掉虚拟机进程</li><li>观察虚拟机列表，其中高可用虚拟机会立刻重新启动，而非高可用虚拟机处于停止状态</li></ol>|高可用虚拟机在另外的 Host 启动，非高可用的则不会|||
|148     |Non-Operational Host(Host是SPM)|<ol><li>查看storage网络的名字和物理接口。在【主机】标签中选择要操作的host，点击 “Network Interfaces”子tab，可以看到其至少有一个rhevm网络和一个storage网络。在Tree面板中点击“ISCSI-share”，在“Storage”tab中选择“ISCSI-share”，点击“Edit”打开“Edit Domain”对话框，点击“+”显示iSCSI目标</li><li>通过ssh连接到host，使用ifconfig命令确认网络连接正常。根据storage网络的名字，用ifdown 命令关闭storage网络</li><li>由于host是SPM的，所以它会立刻自动重启。高可用虚拟机会在cluster中其他可用host上启动，非高可用虚拟机会暂停。而一旦这台host重新运行，原来运行在这条host上的虚拟机会重新迁移回这台host运行</li></ol>||||
|149     |Non-Operational Host（Host不是SPM）|<ol><li>操作步骤同host不是spm的情况</li><li>与SPM情况不同，host上的所有虚拟机都会迁移到其他host上运行</li></ol>|虚拟机自动在另一台主机上运行|||
|150     |Non-responsive host（连接破坏）|<ol><li>首先查看host的网络信息，然后使用ifdown命令关闭其rhevm网络（注意，上一个case是关闭 storage网络）</li><li>高可用虚拟机会在其他host上重新启动，非高可 用虚拟机不会</li></ol>|高可用虚拟机在另外的 Host 启动，非高可用的则不会。|||
|151     |Non-responsive host（不正确保护）|<ol><li>在Hosts tab中选择要操作的虚拟机，点击 “Power Management”下拉菜单中的“Restart”，来重启host</li><li>host重启完毕后，高可用虚拟机会立刻重新运行，在host重启过程中，高可用虚拟机会在其它host上运行。而非高可用虚拟机会始终处于关闭状态</li></ol>|高可用虚拟机在另外的 Host 启动，非高可用的则不会。|||
