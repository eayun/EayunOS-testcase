# Detailed Features Testing

|用例编号|操作|预期结果|实际结果|备注|
|--------|----|--------|--------|----|
|243|最低硬件要求验证 运行engine-setup-2 在一个小于4GB内存的系统|验证警告：在这Host上是内存不足|||
|244|推荐硬件需求验证 运行engine-setup-2 在一个小于16GB内存的系统|验证警告：系统运行的内存没有达到推荐使用的内存|||
|245|生成answer文件 运行engine-setup-2 --generate-answer=filename或 运行engine-setup-2 --generate-answer=filename|执行命令后，文件生成|||
|246|使用answer文件 在之前执行的生成一个answer文件下运行 engine-setup-2 --config-append=filename 或 engine-cleanup-2 --config-append=filename|engine-setup-2正常运行|||
|247|日志 运行 engine-setup-2 或 engine-cleanup-2|检查在/tmp下创建了一个文件 检查记录的配置摘要|||
|248|日志 运行 engine-setup-2 --log=filename或 engine-cleanup-2 --log=filename|检查在指定路径下创建log|||
|249|防火墙管理配置 在一个干净的系统下运行engine-setup-2|1.  检查如果只有安装firewalld系统才会提示你<br/>    是否要配置它<br/><br/>2.  检查如果只有安装iptables系统才会提示你是 否要配置它<br/><br/>3.  检查如果安装了firewalld和iptables系统会<br/>    首先提示你firewalld，如果你回答no系统会 提示iptables<br/><br/>4.  检查执行结束后仅选择正在运行的firewall 管理<br/><br/>5.  如果没有firewall管理被选择，用户可以手动 配置<br/><br/>|||
|250|密码隐藏 运行engine-setup-2|1.  检查当输入密码时屏幕上没有任何显示<br/><br/>2.  检查输入的密码在日志中是不可见的<br/><br/>|||
|251|输出信息 运行engine-setup-2|1.  check that there is a message<br/>    telling where to find the log file<br/><br/>2.  check that a summary of the configuration is presented when running<br/>    without an answer file before applying changes to the system<br/>    allowing the user to abort the procedure<br/><br/>3.  check that there is an info message finalizing the successful<br/>    install<br/><br/>|||
|252|输出信息 运行engine-cleanup-2|1.  check that there is a message<br/>    telling where to find the log file<br/><br/>2.  check that there is an info message finalizing the successful<br/>    cleanup<br/><br/>|||
|253|数据库配置 在干净系统上运行engine-setup-2 选择本地数据库 选择自动的postgresql配置|检查数据库是不是正确的配置和创建|||
|254|数据库配置 在干净系统上运行engine-setup-2 选择本地数据库 选择手动配置postgresql 根据屏幕提示，填充所需的连接参数|1.  检查设置成功完成<br/><br/>2.  检查设置结束engine正常运行<br/><br/>|||
|255|远程数据库配置 在干净系统下运行engine-setup-2 选择远程数据库，按照屏幕提示，填充所需的连接参数|1.  检查设置成功完成<br/><br/>2.  检查设置结束engine正常运行<br/><br/>|||
|256|Apache配置 在干净系统上运行engine-setup-2|1.  check that if selinux<br/>    is enabled httpd\_can\_network\_connect flag is enabled on http and<br/>    https ports<br/><br/>2.  check that existing httpd configuration were backed up<br/><br/>3.  check that mod\_ssl was configured for using engine apache keys<br/><br/>4.  check that Apache was configured as proxy for the requests to the<br/>    jboss service<br/><br/>|||
|257|工具配置 在一干经系统下运行engine-setup-2|检查ovirt-log-collector、ovirt-iso-uploader和 ovirt-image-uploader是否配置|||
|258|验证AIO插件硬件需求 安装ovirt-engine-setup-plugins-allinone 运行 engine-setup-2|1.  检查如果启用了对虚拟化的CPU硬件支持那么<br/>    可以配置VDSM<br/><br/>2.  如果bios禁用了或者CPU不支持对虚拟化CPU硬 件支持那么不可以配置VDSM<br/><br/>|||
|259|||||
|260|||||
|261|||||
|262|||||
|263|||||
|264|||||

> **Note**
>
> 其他注意事项：

