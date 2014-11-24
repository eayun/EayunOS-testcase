# 超级用户门户#

<table>
<thead>
<tr>
 <th width="11%">用例编号</th>
 <th width="45%">操作</th>
 <th width="15%">预期结果</th>
 <th width="15%">实际结果</th>
 <th width="15%">备注</th>
</tr>
</thead>
<tbody>
<tr>
 <td>304</td>
 <td>
     前提条件：已经部署好有一个IPA服务器(本实验IPA地址：192.168.3.200)<br/>
     <br/>
     <ol style="list-style-type:decimal">
         <li>登录Engine控制台，使用ssh连接到Engine控制台中,</br>
         将IPA服务器的Ip地址添加到/etc/resolv.conf文件中：<br/>
         #vi /etc/resolv.conf<br/>
添加nameserver ip（本实验nameserver 192.168.3.200）。 </li>
         <br/>
         <li>运行以下命令:<br/>
         engine-manage-domains add --domain=zhaochao.eayunos.eayun.com --provider=ipa            --user=eayunos
         </li><br/> 
         <li>重启服务：<br/>
         #service ovirt-engine  restart 
         </li><br/>
     </ol>
 </td>
 <td>重启后IdM域被添加到EayunOS虚拟化管理系统。</td>
 <td>ok</td>
 <td>添加IdM域（IPA）</td>
</tr>
<tr>
 <td>305</td>
 <td>
     前提条件：已经部署好有一个IPA服务器并添加了IdM域 <br/>
     <br/>
     <ol style="list-style-type:decimal">
         <li>打开IPA所在的主机上的服务器管理器（这里是192.168.3.200）</li>
         <br/>
         <li>在【Identity】下的【用户】的详细面板中点击【Add】
         </li><br/> 
         <li>在弹出的【Add用户】窗口中填入：<br/>
             <ol style="list-style-type:square">
                <li>用户登录名</li>
                <li>名</li>
                <li>姓</li>
                <li>New Password</li>
                <li>Verify Password</li>
             </ol>
             然后点击【Add】按钮。在"用户"的详细面板中显示了新添加的用户（本实验xyy）
         </li><br/>
         <li>登录EayunOS虚拟化管理服务控制台</li><br/>
              <ol style="list-style-type:square">
                 <li>将密码添加到/var/tmp/password(可以指定其它路径，本实验采用该路径)
                 </li>
                 <li>输入以下命令：<br/>
                 engine-manage-domains edit --domain=zhaochao.eayunos.eayun.com                          --provider=ipa --user=xyy --password-file=/var/tmp/password                             --add-permissions
                 </li>
                 <li>重启ovirt engine使得修改生效：<br/>
                 #service ovirt-engine restart</li>
                 <li>登录管理系统，可以在用户列表下看到新添加的用户，该用户权限为
                 SuperUser</li><br/>
              </ol>
        
     </ol>
 </td>
 <td>EayunOS虚拟化系统中，用户列表中显示添加的用户，该用户可以通过用户门户登录系统
 </td>
 <td>ok</td>
 <td>添加用户并为其分配权限</td>
</tr>
<tr>
 <td>306</td>
 <td>
     <ol style="list-style-type:decimal">
         <li>登录到Engine管理端，点击左侧树形面板中的【展开所有】按键，在默认数据中心下              点击选择【Default】数据中心 </li>
         <br/>
         <li> 在右侧的详细列表中，点击Default数据中心的【权限】子标签，点击菜单中的【添               加】按键 
         </li><br/> 
         <li>弹出的【为用户添加权限】窗口，在【搜索】下拉菜单中选择域，在【命名空间】              下拉菜单中选择【*】，点击【执行】 <br/>
         </li><br/>
         <li>执行结果会列出这个域下所包含的用户，勾选要分配权限的用户，在窗口下方的
          【要分配的角色】下拉列表中，选择PowerUserRole角色，点击【确定】 
         </li><br/>
     </ol>
 </td>
 <td>分配权限成功，在权限子标签中看到新分配的用户及其权限，为用户分配了数据中心的PowerUserRole权限</td>
 <td>ok</td>
 <td>PowerUserRole权限分配</td>
</tr>
<tr>
 <td>307</td>
 <td>
     <ol style="list-style-type:decimal">
         <li>登录到Engine管理端，点击左侧树形面板中的【展开所有】按键，在默认数据中心的              默认集群下，选择虚拟机 </li>
         <br/>
         <li> 在右侧的虚拟机列表中，选择一台虚拟机（HostedEngine虚拟机除外），点击虚拟机               的【权限】子标签，点击菜单中的【添加】按键 
         </li><br/> 
         <li>弹出的【为用户添加权限】窗口，在【搜索】下拉菜单中选择                     域，在【命名空间下拉菜单中选择【*】，点击【执行】  <br/>
         </li><br/>
         <li>执行结果会列出这个域下所包含的用户，勾选要分配权限的用户，在窗口下方的【要分配的角色】下拉列表中，选择PowerUserRole角色，点击【确定】 </li><br/>
         <li>分配权限成功，在权限子标签中看到新分配的用户及其权限，为用户分配了这台虚拟机的PowerUserRole权限,用此用户通过用户门户登录虚拟化系统后显示这台虚拟机的信息</li><br/>
     </ol>
 </td>
 <td> 分配权限成功</td>
 <td>ok</td>
 <td>在现有的虚拟机上分配PowerUserRole权限</td>
</tr>
<tr>
 <td>308</td>
 <td>
     前提条件：至少有一个已分配了权限，可登录的用户 <br/>
     <br/>
     <ol style="list-style-type:decimal">
         <li> 打开浏览器，输入http://[FQDN] （如：http://engine.test.com）  </li>
         <br/>
         <li> 在门户标题下，选择【用户门户】
         </li><br/> 
         <li>页面跳转到用户门户的登录界面，选择域，输入用户名和密码，点击【登录】</li>
         <br/>
     </ol>
 </td>
 <td> 成功登录到用户门户  </td>
 <td>ok</td>
 <td>登录超级用户门户</td>
</tr>
</table>

