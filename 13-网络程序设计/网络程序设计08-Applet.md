---
title:  网络程序设计08-Applet.md
date: 2020-07-28 16:36:52
---

## 第一节 Java Applet的概念

### 什么是Applet?

Applet是这样一类Java程序，其对应的class文件可嵌入在HTML页中，并可由浏览器下载和执行。

Applet的执行过程与Java Application不同

Java Application中均有一个main()方法，执行时从该方法开始执行。

而Applet的执行过程较为复杂，一般由浏览器来执行。

### Applet的载入和运行

Applet不能在命令行直接运行，它的运行环境是用户的浏览器。

必须建立一个包含Applet对应class文件的HTML文档，并指示浏览器去访问该HTML文档对应的URL，这时，浏览器除了下载HTML文档外，还会下载Applet的class文件并运行它。

浏览器载入和运行Applet的步骤如下:

- 浏览器与指定的URL建立连接。 
- 浏览器下载HTML文档。 
- 浏览器下载Applet class。 
- 浏览器运行Applet。

### Applet的安全性限制

“沙箱”机制：Java虚拟机为Applet提供能够良好运行的沙箱，一旦它们试图离开沙箱则会被禁止。

由于小应用程序是通过网络传递的，这就不可避免地使人想到会发生安全问题。例如有人编写恶意程序通过小应用程序读取用户密码并散播到网络上，这将会是一件非常可怕的事情。所以，必须对小应用程序进行限制。

Applet的安全性是由运行Applet的浏览器来控制的，大多数浏览器都对Applet作如下限制：

1. 运行时执行另一程序
2. 任何文件的输入/输出
3. 调用任何本地方法
4. 尝试打开除提供Applet 的主机之外的任何系统的Socket

**安全性限制通过限制Applet的行为来防止下载Applet的用户系统遭到破坏。**

## 第二节 Applet的层次结构

## 第三节 Applet的生命周期和主要方法

## 第四节 Applet的开发和运行步骤 


![通用计算机分类](./ 网络程序设计08-Applet.md/通用计算机分类.png)