#使用Gluster管理主机和磁盘

这个功能可以控制主机上的磁盘和存储设备，在Gluster集群中，可以识别bricks。配置包括
<ol><li> 确定磁盘和存储设备不存在文件系统</li><li>使用这些brick设备通过新的逻辑卷创建新的brick或者通过扩大逻辑卷来扩大存在的brick</li><li>如果有必要可以选择xfs或其他文件系统格式对逻辑卷</li><li>更新这个条目的逻>辑卷</li><li>挂载这个逻辑卷</li></ol>

##测试用例0110001
* 测试步骤

  1.进入管理平台管理员门户如下图所示：

   ![界面图](../images/admin.png)

  2.点**系统**的**数据中心**里的**集群**的**编辑**项，会弹出编辑集群窗口，如图所示：
   ![集群编辑](../images/gluster_cluster_setting.png)

  3.选择启用Gluster服务，默认不启动，点击确定，可以看到选择改变的集群出现一个G图案，如图所示：

   ![G](../images/G.png)

  4.向该集群内添加 EayunOS 宿主机，如果在设置集群为 gluster 集群之前，该集群已经有 EayunOS 宿主机，则进入**主机**选项卡，选择已有宿主机，点击**维护**，之后点击**重新安装**等待完成，并且主机处于up状态。

  5.此时点击**主机**选项卡，在详细列表里出现**存储设备**选项。如图所示：

    ![storageDevice](../images/storageDevice.png)

  6.点击**存储设备**选项，将会给你列出主机存在的所有存储，未被使用的存储放到类表上面，使用的存储则出项一个象征锁，放到列表下，如图所示：

    ![storgeList](../images/storageList.png)

  7.选择未被使用的存储设备，这时可以未存储创建Brick，点击**创建Brick**，弹出创建窗口，如图所示：

    ![creatBrick](../images/creatBrick.png)

  8.根据添加的brick的名字，系统自动挂载到/gluster-bricks下.

  9.再次点击**卷**的**add Brick**可以看到存在的brick方便你的使用。如图所示：

    ![changeBrick](../images/changeBrick.png)


