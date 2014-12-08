# 登录/登出

|用例编号|测试目的|操作|预期结果|实际结果|备注|
|--------|--------|----|--------|--------|----|
|181     ||<ol><li>浏览器中输入engine地址，打开网页，点击User Portal</li><li>在弹出登录框中输入用户名、密码、在Domain下拉菜单上选择用户对应的正确的domain（如admin -\> ）</li><li>若该用户下只有一个虚拟机选中“Connect Automatically”</li><li>点击Login</li></ol>|弹出打开虚拟机的窗口，点击打开直接连接该虚拟机|||
|182     ||<ol><li>浏览器中输入engine地址，打开网页，点击User Portal</li><li>在弹出登录框中输入用户名、密码、在Domain下拉菜单上选择用户对应的正确的domain（如admin -\> ）</li><li>若该用户下有虚拟机数量大于1选中“Connect Automatically”</li><li>点击Login</li></ol>|进入系统，并没有直接连接某个虚拟机|||
|183     ||<ol><li>浏览器中输入engine地址，打开网页，点击User Portal</li><li>在弹出登录框中输入用户名、密码、在Domain下拉菜单上选择用户对应的正确的domain（如admin -\> ）</li><li>若该用户下有虚拟机数量大于1，不选中“Connect Automatically”</li><li>点击Login</li></ol>|进入系统，并没有直接连接某个虚拟机|||

