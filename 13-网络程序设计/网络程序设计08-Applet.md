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

- 要创建一个Applet, 该Applet对应的类必须是java.applet.Applet类的子类。如： 
    ```java
    import java.applet.*;
    public class HelloWorldB extends Applet {
    //  ……
    }
    ```
- 继承java.applet.Applet类不仅可以使Applet能在浏览器内运行，还可以让Applet具有一般Java Appliaction不具有的能力，如播放音乐。
- Applet对应的类必须说明是public。

![Applet的层次结构](./ 网络程序设计08-Applet.md/Applet的层次结构.png)

从层次图中可看出，Applet是Panel的子类，所以它就是一个Container，可作为AWT布局的起始点。

## 第三节 Applet的生命周期和主要方法

### Applet的生命周期

- Applet从开始载入、运行到停止、消亡的整个过程称为Applet的生命期。
- 小应用程序的生命周期相对于Application而言较为复杂。在其生命周期中涉及到Applet类的四个方法（也被JApplet类继承）：
  - init()
  - start()
  - stop()
  - destroy()

![Applet的生命周期](./ 网络程序设计08-Applet.md/Applet的生命周期.png)

### Applet的主要方法

- Applet在生命期的不同阶段，分别执行不同的方法。
- Applet的主要方法包括： init(), start(), stop(), destroy()和paint()。 
- 在Applet的生命期中，没有一个方法是被自始至终地执行的。

#### init()

init()方法是在Applet被第一次载入或重新载入时运行，并且在调用start()之前执行完成。

在Java Appliaction中，程序是从main()方法开始执行的。

Applet则不同。浏览器在运行Applet时，首先执行Applet的构造方法，然后调用Applet中的init()方法进行一些基本的初始化工作，如创建所需的对象、设置初始状态和参数，以及装载图象或字体等。 

#### start()

start()方法在init()方法执行完后被执行

- 系统在调用完init()方法之后，将自动调用start()方法。当浏览器从图标恢复成窗口，或者或者用户离开包含该小应用程序的主页后又再返回时，系统都会再执行一遍start()方法。
- 该方法在小应用程序的生命周期中被调用多次，以启动小应用程序的执行，这一点与init()方法不同。
- 该方法是小应用程序的主体，在其中可以执行一些需要重复执行的任务或者重新激活一个线程，例如开始动画或播放声音等。
- init()和start()方法的任务是激活Applet (make live)

#### stop() 

- 可多次执行,当浏览器变成图标时,或者是离开主页时执行，主要功能是停止一些耗用系统资源的工作。
- stop()方法通常是在Applet变得不可见时被调用的
    ```java
    // 如用户离开当前运行Applet的画面转向另一个画面时，或者浏览器窗口被图标化时。
    // Applet常用该方法来停止动画，关闭声音，或挂起正在运行的线程。如： 
    public void stop() {
    MusicClip.stop();
    }
    ```
- stop()方法常用来关闭start()方法中启动的应用。

#### destroy()

Applet的destroy()方法可在Applet结束时（如用户关闭浏览器）做一些清除工作，如停止所有仍在运行的线程，释放Applet 所占据的资源等，在stop()之后执行。

与析构方法finalize()方法相比，destroy()只可用在Applet上，而finalize()是一个通用的析构方法。由于Java能自动回收内存垃圾，所以除非有特殊的资源需要释放，一般不需要重写destroy()方法。

### Applet的AWT绘制

![Applet的AWT绘制](./ 网络程序设计08-Applet.md/Applet的AWT绘制.png)

- paint(Graphics)方法
- update(Graphics)方法
- repaint()方法 

#### paint (Graphics g)

Applet的paint()方法可以使Applet在屏幕上显示文字和图象。

由于Applet本质上是图形化的，所以通常不用System.out.println()方法来输出（该方法的输出将定向到标准输出），而需在图形环境中建立输出，paint()方法就可在Applet对应的Panel面板上显示文字和画图。

#### paint (Graphics g)

paint()用来定义绘图的具体操作，所以必须被重写

paint()方法是由浏览器调用的。每当Applet需要刷新的时候都会自动调用该方法。

如浏览器窗口被图标化后又恢复到原来的大小时就会调用该方法。

##### 使用paint()方法的例子

在Applet中通过重写paint()方法可以输出需要输出的内容。如： 

```java
import java.awt.*;
import java.applet.*;
public class HelloWorld extends Applet {
   public void paint(Graphics g) {
	  g.drawString("Hello World!",25,25);
   }
}
```

##### 程序浅析

从上例中可看出，paint()方法的参数是一个java.awt.Graphics类的对象，该对象是由浏览器创建并把它传给paint()方法。

使用该对象的方法（如drawString()）可在Applet 对应的Panel内显示文字或画图。

Graphics类的drawString()方法，其第一个参数给出要显示的字符串，第二和第三个参数对应该字符串第一个字符的基准线(baseline)的x,y坐标，该坐标系统的原点(0,0)对应Applet显示区域的左上角，单位是像素。

#### update()方法 & repaint()方法

- Update (Graphics g)：用于更新图形，先清除背景、前景，再调用paint()
- repaint( )：用于重绘图形，在组件外形发生变化，即大小改变或位置移动时，repaint( )方法立即被系统自动调用，而实际上repaint()方法是自动调用update()方法

## 第四节 Applet的开发和运行步骤 

### 开发Applet程序的步骤

- 编辑Applet对应的源程序。 
- 编译该源程序，生成对应的class文件。 
- 编写包含Applet的HTML文本
- 该文本通过\<applet>标签将Applet的class文件嵌入在内。 
- 用浏览器或JDK自带的applerviewer程序来运行Applet。

**前二个步骤与Java Application相同，不再作介绍**

### 包含Applet的HTML文件（例）

```java
<html>
<head>
<title>This page has a Applet on it</title>
</head>
<body>
<h1>Simple Applet</h1>
    <applet code="Simple.class" width=500 height=20>
    </applet>
</body>
</html>
```

### \<APPLET>标记的常用属性

- Applet不能直接在命令行运行，需要编写一个HTML文件，并使用\<applet>标记将Applet嵌入在内，然后才可由浏览器来运行。
- \<applet>标记用于从HTML文本中启动Applet，可带一些属性：
  - archive指出同一个codebase中需预先下载的文件
  - code指出Applet对应class文件的URL
  - 如与HTML文件在同一目录下，则给出Applet类的文件名即可
  - width和height用来指出Applet显示区的宽度和高度，单位为像素
- 前面的例子在HTML文件中包含了一个类名为Simple的Applet，Applet区域的宽度为500像素，高度为20像素。

### \<APPLET>标记的其他属性

- CODEBASE（可选）:如果Applet的类文件与包含Applet的HTML文件不在同一目录下，需要使用CODEBASE属性来指明Applet类所在的目录
- ALT （可选）:当浏览器无法显示Applet时，会显示该属性的字符串
- NAME （可选）:描述Applet的字符串，将显示在浏览器的状态栏
- ALIGN（可选）:指出Applet的对齐方式，取值可为LEFT，RIGHT等

### 向Applet传递参数

使用PARAM可从HTML页向Applet传递参数

要传递的参数由两部分组成： name属性对应参数名，value属性对应参数值。如：

```java
<APPLET CODE="AppletTest.class" WIDTH=200 HEIGHT=100>
		<PARAM NAME= "fontsize" VALUE="24">
</APPLET>
```

在Applet中可用getParameter()方法得到指定参数名对应的参数值。如：

`String theFontSize = getParameter("fontsize"); `

注意，getParameter()方法返回的是字符串类型的参数。