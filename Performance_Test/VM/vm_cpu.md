# 虚拟机 CPU 性能

## 模型一：一对一
* **测试环境**：EayunOS 4.1.1 精简版
   * 一台宿主机：
     <table>
        <tr>
           <td><b>IP</b></td>
           <td>192.168.9.168</td>
        </tr>
        <tr>
           <td><b>物理 CPU 个数：</b></td>
           <td>
              [root@test ~]# cat /proc/cpuinfo | grep 'physical id' | sort | uniq | wc -l <br/>
              1
           </td>
        </tr>
        <tr>
           <td><b>逻辑 CPU 个数（<font color="red">未</font>开启 Hyper-Threading 的情况下）：</b></td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'processor' | wc -l <br/>
           4
           </td>
        </tr>
        <tr>
           <td><b>CPU 内核数（<font color="red">未</font>开启 Hyper-Threading 的情况下）：</b></td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'core id' | sort | uniq | wc -l <br/>
           4
           </td>
        </tr>
        <tr>
           <td><b>逻辑 CPU 个数（开启 Hyper-Threading 的情况下）：</b></td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'processor' | wc -l <br/>
           8
           </td>
        </tr>
        <tr>
           <td><b>CPU 内核数（开启 Hyper-Threading 的情况下）：</b></td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'core id' | sort | uniq | wc -l <br/>
           8
           </td>
        </tr>
     </table>

   * 两台虚拟机：
     <table>
        <tr>
           <td><b>IP</b></td>
           <td>192.168.9.80</td>
           <td>192.168.9.85</td>
        </tr>
        <tr>
           <td><b>物理 CPU 个数：</b></td>
           <td>
              [root@test ~]# cat /proc/cpuinfo | grep 'physical id' | sort | uniq | wc -l <br/>
              1
           </td>
           <td>
              [root@test ~]# cat /proc/cpuinfo | grep 'physical id' | sort | uniq | wc -l <br/>
              1
           </td>
        </tr>
        <tr>
           <td><b>逻辑 CPU 个数（<font color="red">未</font>开启 Hyper-Threading 的情况下）：</b></td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'processor' | wc -l <br/>
           4
           </td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'processor' | wc -l <br/>
           4
           </td>
        </tr>
        <tr>
           <td><b>CPU 内核数（<font color="red">未</font>开启 Hyper-Threading 的情况下）：</b></td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'core id' | sort | uniq | wc -l <br/>
           4
           </td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'core id' | sort | uniq | wc -l <br/>
           4
           </td>
        </tr>
        <tr>
           <td><b>逻辑 CPU 个数（开启 Hyper-Threading 的情况下）：</b></td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'processor' | wc -l <br/>
           4
           </td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'processor' | wc -l <br/>
           4
           </td>
        </tr>
        <tr>
           <td><b>CPU 内核数（开启 Hyper-Threading 的情况下）：</b></td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'core id' | sort | uniq | wc -l <br/>
           4
           </td>
           <td>
           [root@test ~]# cat /proc/cpuinfo | grep 'core id' | sort | uniq | wc -l <br/>
           4
           </td>
        </tr>
     </table>

* **测试工具**：
   * sysbench

* **测试方法**：
   * 将虚拟机的 cpu 设置为主机一样的配置，包括物理 cpu 的个数，逻辑 cpu 的个数，cpu 的核数。
   * 未开启超线程的情况下：在主机的每个 cpu core 和 虚拟机的每个 cpu core 下运行相同的程序，比较运行完成的时间。
   * 开启超线程的情况下：同上。

* **测试结果**：
   
  <table>
     <tr>
        <td><b>测试前提</b></td>
        <td><b>宿主机运行的平均时间(单位：秒)</b></td>
        <td><b>基于本地存储的虚拟机运行的平均时间(单位：秒)</b></td>
        <td><b>基于 NFS 存储的虚拟机运行的平均时间(单位：秒)</b></td>
        <td><b>基于本地存储虚拟机的 CPU 利用率</b></td>
        <td><b>基于 NFS 存储虚拟机的 CPU 利用率</b></td>
     </tr>
     <tr>
        <td>未开启超线程</td>
        <td>22.7371142857s</td>
        <td></td>
        <td>22.88082142855s</td>
        <td>99.371%</td>
        <td></td>
     </tr>
     <tr>
        <td>开启超线程</td>
        <td>22.7516133333s</td>
        <td></td>
        <td>22.9193533333s</td>
        <td>99.268%</td>
        <td></td>
     </tr>
  </table>


## 模型二：一对多
* 一台宿主机：
* 三台虚拟机：

## 模型三：多对多
* 三台宿主机：
* 七台虚拟机：
