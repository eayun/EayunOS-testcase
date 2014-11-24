nux桌面版虚拟机 
<table>
<thead>
<tr>
 <th width="10%">用例编号</th>
 <th width="45%">操作</th>
 <th width="15%">预期结果</th>
 <th width="15%">实际结果</th>
 <th width="15%">备注</th>
</tr>
</thead>
<tbody><tr>
 <td>300</td>
 <td>前提条件：虚拟化平台至少有一个Host及ISO domain ,ISO domain中有Red Hat Enterprise Linux 7.x x64的iso镜像。以及一个可登录用户门户创建虚拟机的用户
     <br/>
     <br/>
     <ol style="list-style-type:decimal">
         <li>确保登录到用户门户，点击左侧的【虚拟机】选项，点击【新建虚拟机】按键</li>
         <br/>
         <li>在弹出的【新建虚拟机】窗口中，选择操作系统类型为Red Hat Enterprise Linux                7.x x64，优化选择为【桌面】，输入名称（必填）、描述和注释（选填），其他保持              默认配置，点击【确定】
         </li><br/> 
         <li>创建虚拟机成功，该虚拟机为桌面虚拟机 </li><br/>
         <li>此时还没有为虚拟机添加磁盘，需要选择该虚拟机，点击虚拟机的【磁盘】子菜单，              点击【添加】按键，输入磁盘大小，点击【确定】，为虚拟机添加一个磁盘 
         </li><br/>
         <li>点击菜单中的【只运行一次】或右键选择【只运行一次】，为虚拟机附加Red Hat                 Enterprise Linux 7.xx64的安装镜像，选择CD-ROM，点击【上移】，点击【确定】
         </li><br/>
         <li>虚拟机启动并运行 </li>
     </ol>
 </td>
 <td>虚拟机正常启动并运行</td>
 <td>ok</td>
 <td>在用户门户创建Linux桌面虚拟机</td>
</tr>
<tr>
 <td>301</td>
 <td>
     前提条件：客户端安装了virt-viewer(本实验使用spice) <br/> 
     <br/>
     <ol style="list-style-type:decimal">
        <li> 在扩展视图下，选择要打开的虚拟机（该虚拟机是运行的），点击虚拟机中的console              图标，可以打开虚拟机控制台 
        </li><br/>
        <li> 或在基本视图下，双击要打开控制台的虚拟机，以打开控制台 
        </li><br/>
        <li> 或在基本视图下，点击右侧窗口中控制台的【连接】，以连接并打开控制台
        </li><br/>
     </ol>
</td>
<td>打开控制台成功</td>
 <td>弹出对话框：<br/>
 无法连接到客户上
 的代理，它没有响应或者未安装。
因此，某些功能可能无法实现。但点击【确定】就正常打开控制台了
 </td>
 <td>打开用户门户的虚拟机控制台</td>
 </tr>
<tr>
 <td>302</td>
 <td>前提条件：虚拟化系统中存在一台EL7虚拟机
      <br/>
     <br/>
     <ol style="list-style-type:decimal">
        <li> 在用户门户选择一台EL7的虚拟机，点击菜单中的关闭图标或右键选择【关闭】，关闭该虚拟机 
        </li><br/>
        <li> 选择这台虚拟机，点击菜单中的【创建模板】按键 
        </li><br/>
        <li> 在弹出的【新建模板】窗口中，输入模板的名称（必填，本实验中名称为EL7）、描述             和注释（选填），勾选【复制虚拟机权限】，其他保持默认配置，点击【确定】（ok）
        </li><br/>
        <li> 虚拟机的模板创建成功，在模板列表中能够看到该模板 
        </li><br/>
        <li> 该磁盘状态变化为Locked -> Up 
        </li><br/>
     </ol>
</td>
<td>虚拟机的模板创建成功，在模板列表中能够看到该模板</td>
 <td>ok</td>
 <td>虚拟机制作模板</td>
 </tr>
 <tr>
 <td>303</td>
 <td>
     前提条件：已经在用户门户中完成了创建虚拟机和创建虚拟机模板的操作，
     也已经能够成功使用虚拟机<br/>
     <br/>
     <ol style="list-style-type:decimal">
        <li> 点击右上角的用户选择【登出】后，重新输入http://ip         （或直接删除URL中/userportal/#login部分），回到门户标题下，选择【管理门户】  
        </li><br/>
        <li> 跳转到管理门户的登录页面，输入用户名、密码，选择域，点击【登录】 
        </li><br/>
        <li> 成功登录，验证如下内容： 
           <ol style="list-style-type:none">
               <li> 虚拟机: </li>
                   <ol style="list-style-type:square">
                       <li>选择虚拟机列表，验证之前创建的虚拟机是否显示在虚拟机的列表中
                       </li>
                       <li>点击选择该虚拟机，在该虚拟机的【权限】子标签中，核对用户是否                            已经继承了对该虚拟机的UserVm Manager权限 
                       </li>
                   </ol>
                   <li>模板: </li>
                   <ol style="list-style-type:square">
                       <li>选择模板列表，验证之前创建的模板是否显示在模板列表中       
                       </li>
                       <li>点击选择该模板，在该模板的【权限】子标签中，核对用户是否已经                            继承了对该虚拟机的PowerUserRole权限，同时admin管理员对该模
                           板继承了SuperUser的权限，除此之外没有其他人能够使用该模板 
                       </li>
                       <li>相比之下，点击其他模板，在该模板的【权限】子标签中，显示已经                            分配给Everyone用户UserTemplateBasedVm权限，意味着该系统中的
                           所有用户都能使用该模板 
                       </li>
                   </ol>
           </ol>
        </li><br/>
     </ol>
</td>
<td>验证成功，之前创建的虚拟机显示在虚拟机列表当中，之前创建的模板显示在模板列表当中</td>
 <td>ok</td>
 <td>验证虚拟机及模板权限</td>
 </tr>
</tbody></table>
