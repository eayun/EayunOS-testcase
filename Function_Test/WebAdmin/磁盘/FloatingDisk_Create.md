#创建一个浮动磁盘
<table width="700px">
<thead>
<tr>
  <th width="10%">用例编号</th>
 <th width="45%">操作</th>
 <th width="15%">预期结果</th>
 <th width="15%">实际结果</th>
 <th width="15%">备注</th>
</tr>
</thead>
<tbody>
<tr>
 <td>313</td>
 <td>
     <ol style="list-style-type:decimal">
         <li>在左侧的树形面板中点击【系统】，在右侧的详细列表中点击选择【磁盘】标签</li>
         <br/>
         <li>点击菜单中的【添加】按键，在弹出的【添加虚拟磁盘】窗口中，输入如下配置：
         <br/>
         <ol style="list-style-type:square">
            <li>大小：20（本实验设置大小为20G）</li>
            <li>别名（必填）</li>
            <li>描述（可不填）</li>
            <li>选择数据中心</li>
         </ol>
         </li><br/> 
         <li>其他配置保持默认配置，点击【确定】
         </li><br/>
     </ol>
 </td>
 <td>浮动磁盘创建成功,在磁盘列表中显示了添加的浮动磁盘</td>
 <td>ok</td>
 <td>创建浮动磁盘</td>
</tr>
<tr>
 <td>314</td>
 <td>
     <ol style="list-style-type:decimal">
         <li>在左侧树形面板中点击【系统】，在右侧的详细列表中点击选择【虚拟机】标签              </li><br/>
         <li>从显示的虚拟机列表中选择要分配浮动磁盘的虚拟机(浮动磁盘所在的数据中心下的虚              拟机)，点击虚拟机的【磁盘】子标签，点击菜单中的【添加】按键 
         </li><br/> 
         <li>在弹出的【添加虚拟机磁盘】窗口中，勾选【附加磁盘】，此时会列出所有可用的浮              动磁盘 
         </li><br/>
         <li> 勾选要分配的浮动磁盘，点击【确定】 </li><br/>
     </ol>
 </td>
 <td>虚拟机分配浮动磁盘成功，在虚拟机的【磁盘】子标签中显示该浮动磁盘的信息 </td>
 <td>ok</td>
 <td>给虚拟机分配浮动磁盘</td>
</tr>
</tbody>
</table>

