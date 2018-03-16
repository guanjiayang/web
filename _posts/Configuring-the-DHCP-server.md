
## 问题描述

#### 华为交换机如何配置DHCP服务器？

## 解决方案

交换机设备作为DHCP服务器为客户端设备分配IP地址有两种配置方式：
配置基于全局地址池的DHCP服务器
DHCP服务器在全局视图下创建IP地址池，在接口视图下配置服务器采用全局地址池来为客户端分配IP地址、网关、DNS 服务器地址等信息。
配置基于接口地址池的DHCP服务器
DHCP服务器在接口视图下配置服务器采用接口地址池来为客户端分配IP地址、网关、DNS 服务器地址等信息。

```
说明：
      以上两种配置方式中提到的接口包括VLANIF接口和切换成三层模式的物理接口。其中，切换成三层模式的物理接口自V200R005C00版本开始支持上述配置。
```
根据创建方式的不同，地址池可以分为基于接口方式的地址池和基于全局方式的地址池：
基于接口方式的地址池
在服务器与客户端相连的接口上配置IP地址，地址池是跟此接口地址所属同一网段的IP地址，且地址池中地址只能分配给此接口下的客户端。这种配置方式简单，仅适用于DHCP客户端与DHCP服务器在同一个网段时，即不存在中继的场景。例如，设备做DHCP服务器时仅给一个接口下的客户端分配IP地址或者给多个接口下的客户端分别分配不同网段的IP地址。
基于全局方式的地址池
在服务器系统视图下创建的指定网段的地址池，且地址池中地址可以分配给设备所有接口下的客户端。这种配置方式适用于：
− 客户端与DHCP服务器在不同网段，即存在中继的场景。
− DHCP服务器与客户端在同一网段，且需要给一个接口下的客户端分配IP地址或者给多个接口下的客户端分别分配不同网段的IP地址。

如图所示，交换机作为DHCP服务器为PC分配IP地址和DNS服务器的IP地址时，可以采用全局地址池和接口地址池两种配置方式。

![mahua](http://oltn18dzj.bkt.clouddn.com/image/png/dhcp.png)

基于全局地址池的DHCP服务器的配置示例如下：

- 创建IP地址池

```javascript
<HUAWEI> system-view
[HUAWEI] ip pool 1 //创建IP地址池
[HUAWEI-ip-pool-1] network 10.10.10.0 mask 255.255.255.0 //配置网段
[HUAWEI-ip-pool-1] gateway-list 10.10.10.1 //配置网关
[HUAWEI-ip-pool-1] excluded-ip-address 10.10.10.10 10.10.10.50  //配置保留地址
[HUAWEI-ip-pool-1] dns-list 10.8.8.8 //配置DNS服务器的IP地址
[HUAWEI-ip-pool-1] lease day 0 hour 8 minute 0 //配置租期
[HUAWEI-ip-pool-1] quit
```
- 使能DHCP功能

```javascript
[HUAWEI] dhcp enable //全局模式下开启DHCP功能

```

- 使能VLANIF10接口采用全局地址池的DHCP服务器功能

```javascript
[HUAWEI] interface vlanif10 //进入到vlan的逻辑接口
[HUAWEI-Vlanif10] ip address 10.10.10.1 255.255.255.0 //配置IP地址
[HUAWEI-Vlanif10] dhcp select global //配置基于全局地址池的DHCP服务器功能
```

基于接口地址池的DHCP服务器的配置示例如下：

1.使能DHCP功能

```javascript

<HUAWEI> system-view
[HUAWEI] dhcp enable

```

2.使能接口VLANIF10接口采用接口地址池的DHCP服务器功能

```
注意：执行命令dhcp select interface前,需要配置VLANIF接口的IP地址。
````

```javascript
[HUAWEI] interface vlanif 10
[HUAWEI-Vlanif10] ip address 10.10.10.1 255.255.255.0 //配置网段
[HUAWEI-Vlanif10] dhcp select interface //配置基于接口地址池的DHCP服务器功能
[HUAWEI-Vlanif10] dhcp server dns-list 10.8.8.8 //配置DNS服务器的IP地址
[HUAWEI-Vlanif10] dhcp server excluded-ip-address 10.10.10.10 10.10.10.50  //配置保留地址
[HUAWEI-Vlanif10] dhcp server lease day 0 hour 8 minute 0 //配置租期
[HUAWEI-Vlanif10] quit
```
