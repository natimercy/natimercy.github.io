---
title: windows 命令行下用netsh 实现端口转发(端口映射)
copyright: true
date: 2021-04-30 11:00:00
updated: 2021-04-30 11:20:00
tags: 
	- netsh 
categories: 
	- window
	- netsh
comments: true

---

## 前言

> 微软Windows的netsh是一个命令行脚本实用工具。使用netsh工具 ，可以查看或更改本地计算机或远程计算机的网络配置。不仅可以在本地计算机上运行这些命令，而且可以在网络上的远程计算机上运行。可以手动运行Netsh命令，或创建批处理文件或脚本实现过程的自动化。netsh提供了脚本功能，让您在批处理模式下针对指定的计算机，运行一组命令。利用netsh ，可以将配置脚本保存为文本文件，便于存档或用于配置其他的计算机。

<!--more-->

## 配置方法

- 假定需要通过127.0.0.1的8003端口转发到192.168.0.20的8003端口,则需要在本机的命令行上输入以下命令(添加转发):


  ```cmd
netsh interface portproxy add v4tov4 listenport=8003 listenaddress=127.0.0.1 connectport=8003 connectaddress=192.168.0.20
  ```

  - 删除指定转发


  ```cmd
  netsh interface portproxy delete v4tov4 listenport=8003 listenaddress=127.0.0.1
  ```

  - 查看存在的转发


  ```cmd
  netsh interface portproxy show all
  ```

  - 查看端口(8003)是否处于被侦听状态

    **`findstr` 后有一个空格**

  ```cmd
  netstat -ano | findstr :8003
  ```

- 禁用系统防火墙


  ```
  netsh firewall set opmode disable
  ```

  - 启用系统防火墙


  ```cmd
  netsh firewall set opmode enable
  ```

  - [微软官方 netsh 文档](https://support.microsoft.com/zh-cn/help/947709/how-to-use-the-netsh-advfirewall-firewall-context-instead-of-the-netsh)



