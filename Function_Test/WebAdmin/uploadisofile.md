# 上传iso文件到iso存储域
**简要说明**：上传iso文件到易云虚拟化管理平台中的iso存储域，可以使用户自定义安装管理平台中虚拟机的操作系统。

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|0120000	|上传iso文件到ISO存储域|<ol><li>以root身份登录到EayuOS管理平台。</li><li>下载所需的iso文件到管理平台的临时目录下。</li><li>使用<code>engine-iso-uploader</code>查看存在的ISO存储域的名字，命令行为<code># engine-iso-uploader list</code>，该命令会提示用户输入REST API的密码，输入密码即可。</li><li>使用<code>engine-iso-uploader</code>命令上传iso文件到ISO存储域，命令行为<code> # engine-iso-uploader --iso-domain=ISO-DOMAIN upload /tmp/ovirt-node-iso-3.1.0-0.999.456.el6.iso</code>其中ISO-DOMAIN为之前所查看已存在存储域的名称，/tmp/ovirt-node-iso-3.1.0-0.999.456.el6.iso为所下载iso文件的临时目录及文件名称，同时命令行仍然提示需要输入REST API密码，输入密码即可。</li><li>命令行提示文件正在上传中，耐心等待即可，等待时间会因文件大小而不同，上传完毕之后命令行会有上传成功提示。|iso文件上传完成并出现在命令中指定的 ISO 存储域中。|ISO 上传完成并出现在命令中指定的 ISO 存储域中。同时也将出现在创建该 ISO 存储域所附加到的数据中心中的虚拟机时可用的启动媒介列表中。|可在【虚拟机】->【新建虚拟机】->【引导选项】->【附加CD】的下拉列表中查看上传的iso文件。|
