---
title: 网络程序设计07-AWT事件模型
date: 2020-07-28 15:35:23
---

## 第一节 事件模型的概念

### 什么是事件

- 事件（event）：用户对界面操作在java语言上的描述，以类的形式出现
- 事件源（event source）：是一个事件产生者
- 事件处理者（event handler）：接收事件对象并对其进行处理的对象 

![什么是事件](./网络程序设计07-AWT事件模型/什么是事件.png)

### Java的事件模型

#### 层次模型——早期的事件模型

层次模型是Java早期的事件模型，在JDK1.0中采用

**工作原理**：当事件产生时，它先被送往产生该事件的组件，如事件在这里未被处理，它就会被自动送往该组件的Container，如Container也未对事件进行处理，则还会递交给该Container的上一层Container（如有的话）

![层次模型](./网络程序设计07-AWT事件模型/层次模型.png)

- 优点:简单，而且非常适合面向对象的编程环境
- 缺点：
  - 事件只能由产生这个事件的组件或包含这个组件的容器处理
  - 为了处理事件，必须定义接收这个事件的组件的子类，或者在基容器创建handleEvent()方法

**这种模型已被新的事件模型所取代。**

#### 委托代理模型

委托代理模型(Delegation model)，是JDK1.1之后采用的事件模型

- **工作原理**：一个组件如要响应某一事件，必须先登记(register)与该事件有关的一个或多个被称为listeners的类，这些类包含了相应的方法能接受事件并对事件进行处理。
- 操作步骤
  - 组件调用addXXXListener()方法来登记相应的Listener（XXX代表Listener类型）
  - 该方法的参数是一个实施了相应Listener的类的实例，在实例中定义了相应的事件处理方法。
  - 当组件产生事件时，特定的事件处理方法会被自动执行。

---

- 在委托代理模型中，事件的产生者和事件的处理者分离开来了，它们可以是不同的对象。事件的产生者是这个组件；事件的处理者则是那些listener，它们是一些实施了Listener接口的类。当事件传到登记的listener时，该listener中必须有相应的方法来接受这种类型的事件并对它进行处理。
- 一个组件如没有登记的listeners，则它产生的事件就不会被传递。
- 委托代理模型较好地解决了层次模型中的问题，并提供了对Java Bean的支持。

**注：虽然JDK的新版本也支持旧的层次模型，但层次模型和委托代理模型不能在程序中混用。**

![委托代理模型](./网络程序设计07-AWT事件模型/委托代理模型.png)

##### 委托代理模型——TestButton.java

```java
import java.awt.*;
import java.awt.event.*; 
     public class TestButton {	
        public static void main(String args[]){
	Frame f = new Frame("Test");
	Button b = new Button("Press Me!");
	b.addActionListener(new ButtonHandler());//添加事件监听器
                    f.setLayout(new FlowLayout()); //设置布局管理器
                    f.add(b);
                    f.setSize(200,100);
	f.setVisible(true);}
     }
     class ButtonHandler implements ActionListener {
          public void actionPerformed(ActionEvent e){
	System.out.println("Action occurred"); 
	System.out.println("Button's label is:"+e.getActionCommand()); 
      //本接口只有一个方法，因此事件发生时，系统会自动调用本方法，需要做的操作就把代码写在则个方法里。
         }
     }
```

- 浅析
  - Button 类有一个addActionListner(ActionListener)方法
  - AddActionListner 接口定义了一个方法actionPerformed，用来接收一个ActionEvent
  - 创建一个Button 对象时，这个对象可以通过使用addActionListener 方法注册为ActionEvents 的监听者。调用这个方法时带有一个实现了ActionListener 接口的类的参数
  - 在Button 对象上用鼠标进行点击时，将发送一个ActionEvent 事件。这个ActionEvent 事件会被使用addActionListener()方法进行注册的所有ActionListener 的actionPerformed()方法接收。
  - ActionEvent 类的getActionCommand()方法返回与动作相关联的命令名称。以按钮的点击动作为例，将返回Button 的标签。
- 优点：
  - 事件不会被意外地处理
  - 有可能创建并使用适配器 (adapter)类对事件动作进行分类
  - 委托模型有利于把工作分布到各个类中
- 缺点：不容易将JDK1.0 代码移植到JDK1.1 上

## 第二节 事件的分类和处理


## 第三节 事件适配器



![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)

![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)
![通用计算机分类](./网络程序设计07-AWT事件模型/通用计算机分类.png)