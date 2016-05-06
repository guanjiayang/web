---
layout: post
title: ER3260:多VLAN划分的实现
categories: VLAN
excerpt: ER3260 多VLAN
comments: true
---

**H3C ER3260支持最多划分16个VLAN，但是此路由器只有3个LAN口，就需要LAN端口配置为trunk，允许通过相应的VLAN或者所有VLAN，这样的话能通过所配置的多个vlan。同时需要下面连接的交换机（可网管，支持vlan划分）的端口也同样配置为trunk，允许通过所有VLAN。**
### 操作步骤
- 在ER3260上，建立VLAN50、VLAN51、VLAN52和透传VLAN100，如下图设置

![er32601.jpg](/images/ER3260/er32601.jpg)

---

![er32602.jpg](/images/ER3260/er32602.jpg)

---

- 在S2100上，选定一可用端口做TRUNK口用，比如端口15，建立VLAN50（添加端口，比如端口16，可多个）、VLAN51（添加端口，比如端口17，可多个）和VLAN52(添加端口，比如端口18，可多个），新建TRUNK口(端口15，PVID 100，允许通过的VLAN 50-52)，如下图操作

![s2100-1.jpg](/images/ER3260/s2100-1.jpg)

---
![s2100-2.jpg](/images/ER3260/s2100-2.jpg)

---
![s2100-3.jpg](/images/ER3260/s2100-3.jpg)

---
![s2100-4.jpg](/images/ER3260/s2100-4.jpg)

---

- ER3260 LAN3与S2100 端口15直连即可，至此完成。
