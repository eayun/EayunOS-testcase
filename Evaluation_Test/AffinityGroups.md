# Affinity组

## 策略描述

* Positive Affinity (Run Together) - 一个能够设置一同运行affinity的策略，以决定确认哪些虚拟机需要运行在同一个管理主机上。
* Anti (Negative) Affinity (Run Independently) - 一个能够设置独立运行的affinity策略，以决定确认哪些虚拟机要分开运行在不同的管理主机上。
* Must Condition (enforce = hard) - 这是个硬性条件，意味着两台或更多的虚拟机要运行在同一台管理主机上或者是独立的主机上，无视外部条件。
* Should Condition (enforce = soft) - 这是个软式条件，意味着有优先权，两台或更多的虚拟机会运行在同一个管理主机或在单独的主机上，但它不是硬性要求的。

## 测试

* 强制执行Positive策略

  1. 点击【集群】选项卡，选择要设置Affinity组的集群，点击【Affinity组】子选项卡。
  1. 点击【Affinity组】子选项卡的【新建】按键。
  1. 在弹出的【新建Affinity组】窗口中，输入名称、描述，勾选Positive和Enforcing。
  1. 选择虚拟机（两台以上），点击【确定】。
  1. 运行虚拟机vm1，该虚拟机运行在主机Host1上。
  1. 运行虚拟机vm2，该虚拟机也运行在主机Host1上。

  > #### 注意
  > 如果虚拟机vm2设置为可迁移，虚拟机vm2无法迁移到其他主机上，提示<code>Migration failed, No available host found</code>。

* 选择执行Positive策略

  1. 点击【集群】选项卡，选择要设置Affinity组的集群，点击【Affinity组】子选项卡。
  1. 点击【Affinity组】子选项卡的【新建】按键。
  1. 在弹出的【新建Affinity组】窗口中，输入名称、描述，勾选Positive，取消勾选Enforcing。
  1. 选择虚拟机（两台以上），点击【确定】。
  1. 运行虚拟机vm1，该虚拟机运行在主机Host1上。
  1. 运行虚拟机vm2，该虚拟机也运行在主机Host1上。

  > #### 注意
  > * 如果虚拟机vm2设置为专属于其他主机，则vm2运行在其他主机上。
  > * 如果虚拟机vm2设置为可迁移，虚拟机vm2可以迁移到其他主机上。

* 强制执行Negative策略

  1. 点击【集群】选项卡，选择要设置Affinity组的集群，点击【Affinity组】子选项卡。
  1. 点击【Affinity组】子选项卡的【新建】按键。
  1. 在弹出的【新建Affinity组】窗口中，输入名称、描述，取消勾选Positive，勾选Enforcing。
  1. 选择虚拟机（两台以上），点击【确定】。
  1. 运行虚拟机vm1，该虚拟机运行在主机Host1上。
  1. 运行虚拟机vm2，该虚拟机运行在除主机Host1之外的其他主机上。

> #### 注意
> * 如果除Host1外没有其他可用主机，则虚拟机vm2无法运行。
> * 如果虚拟机vm2设置为可迁移，虚拟机vm2不能迁移到主机Host1上，但可以迁移到其他主机上。

* 选择执行Negative策略

  1. 点击【集群】选项卡，选择要设置Affinity组的集群，点击【Affinity组】子选项卡。
  1. 点击【Affinity组】子选项卡的【新建】按键。
  1. 在弹出的【新建Affinity组】窗口中，输入名称、描述，取消勾选Positive和Enforcing。
  1. 选择虚拟机（两台以上），点击【确定】。
  1. 运行虚拟机vm1，该虚拟机运行在主机Host1上。
  1. 运行虚拟机vm2，该虚拟机运行在其他可用主机上。

> #### 注意
> * 如果虚拟机vm2设置为专属于主机Host1，则vm2可以运行在Host1上。
> * 如果虚拟机vm2没有其他可运行的主机，则vm2启动时运行在主机Host1上。
> * 如果虚拟机vm2设置为可迁移，虚拟机vm2可以迁移到主机Host1上。
