# 备份及恢复EayunOS管理端数据库
**简要说明**：engine-backup是将备份和恢复统一到一起的程序，由于数据是一定不能丢的，因此，OVIRT开发此脚本程序帮助您实现这一目标 。

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|2000001       |备份数据库|<ol><li>使用命令<code> #engine-backup --help</code>查看engine-backup的用法。</li><li>在文件/etc/ovirt-engine/engine.conf.d/10-setup-database.conf下查看所要备份数据库的基本信息（包括数据库用户名称、数据库名称、数据库密码等）。</li><li>填写engine-backup所需参数。</li><li>按回车键开始备份文件。|生成一个包含数据库所有数据的文件|在当前目录下生成一个backup的压缩文件|可使用命令<code>#tar -jxvf backup</code>查看backup的具体信息。|
|2000002       |恢复数据库|<ol><li>使用<code>#su postgres</code>命令进入数据库操作环境,在使用命令<code>$dropdb engine;</code>删除原有数据库。</li><li>使用命令<code>#sudo -u postgres psql</code>进入数据库操作环境，再使用命令<code>postgres=# create role [user name] with login encrypted password '[password]';</code>创建数据库用户。</li><li>在命令行输入<code>sudo -u postgres -O engine engine</code>创建数据库。</li><li>编辑文件 /var/lib/pgsql/data/pg_hba.conf，并在紧接着以 Local 开头的那一行下面添加如下内容：<code>host [database name] [user name] 0.0.0.0/0 md5</code> / <code>host [database name] [user name] ::0/0 md5</code></li><li>执行命令<code>#service postgresql restart</code>重启数据库服务，在backup所在文件夹下执行执行命令engine-backup填写相关恢复参数之后回车即开始恢复数据库。|数据库恢复成功|数据库恢复成功，并且显示如下信息<code>You should now run engine-setup.</code>|执行<code>#engine-setup</code>重新配置好**ovirt-engine**服务即可。|
