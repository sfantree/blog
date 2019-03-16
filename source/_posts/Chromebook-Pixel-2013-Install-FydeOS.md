---
title: Chromebook Pixel 2013 安装 FydeOS
date: 2019-03-16 18:57:26
tags: [Chromebook]
categories: 技术控
---

首先是拆机壳儿，去除硬件写保护，不得不吐槽这个Chromebook后盖比较难打开，四个底座是用胶水封上的。

接着是启用开发者模式

进入开发者模式：`电源键+esc+刷新键` (第1排左到右第4个键) 
系统重启后
忽略系统警告：`ctrl+d` 
关闭系统验证：`ENTER键` 

跳过系统警告：`ctrl+d` (可能需多按几次) 
系统开始部署开发者模式环境，大概需要5-10分钟左右完成 
自动重启后，如果能用`ctrl+alt+后退键`（第1排第2个键）和 `ctrl+alt+前进键`（第1排第3个键）来回切换终端与桌面，表示开启成功。

进入终端，按`ctrl+alt+f2`进入linux界面后，登陆管理员账户，chronos，正常输入一次即可

<!-- more -->

关闭软件写保护：`flashrom --wp-disable`
进入BIOS保存目录：`cd ~/Downloads/`
备份原BIOS：`sudo flashrom -r bios.bin`

刷入第三方BOIS

johnlewis.ie 刷入 BIOS 

`cd;bash <(curl https://johnlewis.ie/flash_cb_fw.sh)` 选择 `5`

![](https://ww1.sinaimg.cn/large/006uCcPzgy1g14us8vkcdj31z41b811g.jpg)


使用感受：
首先说优点，使用免费，第三方Chrome OS适配的兼容性和稳定性还比较好，重点是能运行Android APP。
缺点就很显而易见了，登陆要注册手机号，内置插件监控用户所有行为，完全阉割谷歌服务，无法进行同步。
受不了大部分国产软件不收集用户隐私誓不罢休的行为，使用了几个小时卸载了，还是重装了原版的Chrome OS。

1. https://blog.csdn.net/woodenrobot/article/details/53931220
2. https://jingyan.baidu.com/article/359911f558086f57ff03067e.html
3. http://tieba.baidu.com/p/6055206763
4. http://johnlewis.ie
