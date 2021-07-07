# Java 桌面端GUI编程

## 概述

**java.awt** 包提供抽象窗口工具包。早期的 java GUI 开发主要使用 java.awt 包，它提供一些类例如 Button、TextField、List 等。**javax.swing** 包是 JDK 1.2 之后推出的一个功能更加强大的 GUI 设计工具包。GUI 开发主要用到两个概念：**容器类（Container） **和 **组件类（Component）**。

### Swing 中的组件

Swing 组件按功能可分为如下几类:

1. 顶层容器：JFrame, JApplet, JDialog和JWindow。
2. 中间容器：JPanel, JScrollPane, JSplitPane, JTooIBar 等。
3. 特殊容器：在用户界面上具有特殊作用的中间容器，如 JlnternalFrame、JRootPane、JLayeredPane 和 JDestopPane 等。
4. 基本组件：实现人机交互的组件，如JButton、 JComboBox、Just, Menu、Mider 等。
5. 不可编辑信息的显示组件：向用户显示不可编辑信息的组件，如 JLabel、JProgressBar和JTooITip 等。
6. 可编辑信息的显示组件：向用户显示能被编辑的格式化信息的组件，如 JTable、JTextArea 和 JTextField 等。
7. 特殊对话框组件：可以直接产生特殊对话框的组件，如 JColorChoosor 和 JFileChooser 等。

Swing 的4个顶层容器类直接继承了 AWT 组件，而不是从 JComponent 派生出来的，它们分别是：JFrame、JDialog、JApplet和 JWindow 。

![image-20201215173136533](C:\Users\HZN\Desktop\笔记\Java 桌面端GUI编程.assets\image-20201215173136533.png)

## 常用组件

### JFrame 窗口基本容器

- JFarme() 创建一个无标题窗口。

- JFarme(String s) 创建一个标题为 s 的窗口。

- public void setBounds(int a,int b,int width,int height) 设置窗口的初始位置是(a,b)，即距屏幕左面a个像素，距屏幕上方b个像素，窗口的宽是width，高是height。

- public void setSize(int width,int height) 设置窗口的大小。

- public void setLocation(int x,int y) 设置窗口的位置，默认位置是(0,0)。

- public void set Visible(boolean b)设置窗口是否可见，窗口默认是不可见的。
  
- public void setResizable(boolean b )设置窗口是否可调整大小，默认可调整大小。

- public void setVisible(boolean b) 设置窗口是否可见，窗口默认是不可见的。
  
- public void dispose() 撤销当前窗口，并释放当前窗口所使用的资源。
  
- public void setExtendedState(int state) 设置窗口的扩展状态，其中参数 state取.JFrame类中的下列类常量：
  
  MAXIMIZED_HORIZ（水平方向最大化），
  
  MAXIMIZED_VERT（垂直方向最大化），
  
  MAXIMIZED_BOTH（水平、垂直方向都最大化）。
  
- public void setDefaultCloseOperation(int operation) 该方法用来设置单击窗体右上角的关闭图标后，程序会做出怎样的处理。其中的参数 operation 取 JFrame 类中的下列 int 型 static 常量，程序根据参数 operation 取值做出不同的处理：

   DO_NOTHING_ON_CLOSE（什么也不做），

   HIDE_ON_CLOSE（隐藏当前窗口），

   DISPOSE_ON_CLOSE（隐藏当前窗口，并释放窗体占有的其他资源)，

   EXIT_ON_CLOSE（结束窗口所在的应用程序）。


### JMenubar 菜单条

JMenubar 负责创建菜单条，JMenubar 的一个实例就是一个菜单条。JFrame 类有一个方法将 JMenubar 加入其中：

``` java
setJMenuBar(JMenuBar bar);
```

### JMenu 菜单

JMenu 的一个实例就是一个菜单。

JMenu 本身也可以是一个菜单项，因此可以嵌套使用。

### JMenuItem 菜单项

负责创建菜单项，一个 JMenuItem 实例本身就是一个菜单项。

### JTextField 输入框

允许用户输入单行文本的组件

### JTextArea 文本域

允许用户输入多行文本的组件

### JButton 按钮

接收用户点击事件的按钮组件

### JLabel 标签

用来显示提示信息的组件

### JCheckBox 复选框

为用户提供多项选择功能，有两种状态，一种是选中，另一种是未选中

### JRadioButton 单选按钮

提供单项选择的功能

### JComboBox 下拉列表

提供下拉列表，可供用户单项选择

### JPasswordField

提供密码输入的功能

## 常用容器

### JPanel 面板

可以向面板添加组件，然后把它加入到其它容器中。**JPanle 面板的默认布局是 FlowLayout 布局**。

### JTabbedPane 选项卡窗格

可以使用 JTabbedPane 容器作为中间容器。当用户向 JTabbedPane 容器添加一个组件时，JTabbedPane 容器就会自动为该组件指定一个对应的选项卡，即让一个选项卡对应一个组件。各个选项卡对应的组件层叠式放入 JTabbedPane 容器，当用户单击选项卡时，JTabbedPane 容器将显示该选项卡对应的组件。选项卡默认在 JTabbedPane 容器的顶部,从左向右依次排列。JTabbedPane 容器可以使用

``` java
add(String text,Component c);
```

方法将组件 c 添加到 JTabbedPane 容器中，并指定和组件 c 对应的选项卡的文本提示是 text 。

可以使用构造方法

``` java
public JTabbedPane(int tabPlacement)
```

创建 JTabbedPane 容器，选项卡的位置由参数 tabPlacement 指定，该参数的有效值为 JTabbedPane.TOP、JTtabbedPane.BOTTOM、JTabbedPane.LEFT 和 JTabbedPane.RIGHT。

### 滚动窗格JScrollPane

滚动窗格只可以添加一个组件，可以把一个组件放到一个滚动窗格中，然后通过滚动条来观看该组件。JTextArea不自带滚动条，因此就需要把文本区放到一个滚动窗格中。例如：

``` java
JScrollPane scroll=new JScrollpane(new JTextArea ());
```

### 拆分窗格JSplitPane

顾名思义，拆分窗格就是被分成两部分的容器。拆分窗格有两种类型:水平拆分和垂直拆分。水平拆分窗格用一条拆分线把窗格分成左右两部分，左面放一个组件，右面放一个组件，拆分线可以水平移动。垂直拆分窗格用一条拆分线把窗格分成上下两部分，上面放一个组件,下面放一个组件,拆分线可以垂直移动。

JSplitPane的两个常用的构造方法如下：

``` java
JSplitPane(int a,Component b, Component c)
```

参数 a 取 JSplitPane 的静态常量 HORIZONTAL_SPLIT 或 VERTICAL SPLIT，以决定是水平还是垂直拆分。后两个参数决定要放置的组件。

``` java
JSplitPane(int a,boolean b, Component c, component d)
```

参数 a 取 JSplitPane 的静态常量 HORIZONTAL_SPLIT 或 VERTICAL_SPLIT，以决定邀水平还是垂直拆分，参数b决定当拆分线移动时，组件是否连续变化（true是连续）。

### JLayeredPane分层窗格

如果添加到容器中的组件经常需要处理重叠问题，就可以考虑将组件添加到分层窗格。分层窗格分成5个层，分层窗格使用：

``` java
add(Jcomponent com, int layer) ;
```

添加组件 com，并指定 com 所在的层，其中参数 layer 的取值为 JLayeredPane 类中的类常量：DEFAULT_LAYER、PALETTE_LAYER、MODAL_LAYER、POPUP_LAYER、DRAG_LAYER。

DEFAULT_LAYER 层是最底层，添加到 DEFAULT_LAYER 层的组件如果和其他层的组件发生重叠时，将被其他组件遮挡。DRAG_LAYER 层是最上面的层，如果分层窗格中添加了许多组件，当用户用鼠标移动一组件时，可以把该组件放到 DRAG_LAYER 层，这样，用户在移动组件的过程中，该组件就不会被其他组件遮挡。添加到同一层上的组件，如果发生重叠,后添加的会遮挡先添加的组件。分层窗格调用 public void setLayer(Component c,int layer) 可以重新设置组件 c 所在的层，调用 public int getLayer(Component c) 可以获取组件 c 所在的层数。

## 常用布局

通过常用布局方法可以很好的控制组件在容器中的位置，设置布局可以使用：

``` java
setLayout(<布局对象>);
```

### FlowLayout 流式布局

FlowLayout 类的一个常用构造方法如下：

``` java
FlowLayout()
```

该构造方法可以创建一个居中对齐的布局对象。使用 FlowLayout 布局的容器使用 add 方法将组件顺序地添加到容器中，组件按照加入的先后顺序从左向右排列，一行排满之后就转到下一行继续从左至右排列，每一行的组件都居中排列，组件之间的间的默认水平和垂直间隙是5个像素。组件的大小为默认的最佳大小，例如，按钮的大小刚好能保证显示其上面的名字。**对于添加到使用 FlowLayou 布局的容器中的组件，组件调用 setSize(int x,int y) 设置的大小无效，如果需要改变最佳大小，组件需调用 public void setPreferredSize(Dimension preferredSize)设置大小**，例如:

``` java
button.setPreferredsize(new Dimension(20,20));
```

**FlowLayout 布局对象调用 setAlignment(int align) 方法可以重新设置布局的对齐方式**，其中align可以取值 FlowLayout.LEFT、FlowLayout.CENTER、Flow Layout.RIGHT。

###  BorderLayout 布局

BorderLayout 也是一种简单的布局策略，如果一个容器使用这种布局,那么容器空间简单地划分为东、西、南、北、中5个区域，中间的区域最大。每加入一个组件都应该指明把这个组件加在哪个区域中，区域由 BorderLayout 中的静态常量 CENTER、NORTH、SOUTH、WEST、 EAST 表示，例如，一个使用 BorderLayout 布局的容器con，可以使用 add 方法将一个组件 b 添加到中心区域：

``` java
con.add(b,BorderLayout.CENTER);
```

添加到某个区域的组件将占据整个这个区域。每个区域只能放置一个组件，如果向某个已放置了组件的区域再放置一个组件，那么先前的组件将被后者替换掉。使用 BorderLayout 布局的容器，最多只能放置5个组件，如果容器中需要加入超过5个组件，就必须使用容器的嵌套或改用其他的布局策略。

### CardLayout 卡片布局

使用 CardLayout 的容器可以容纳多个组件，这些组件被层叠放入容器中，最先加入容器的是第一张（在最上面），依次向下排序。使用该布局的特点是，同一时刻容器只能从这些组件中选出一个来显示,就像叠“扑克牌”，每次只能显示其中的一张，这个被显示的组件将占据所有的容器空间。

假设有一个容器con，那么使用 CardLayout 的一般步骤：

- 创建 CardLayout 对象作为布局，例如：

  ``` java
  CardLavout card= new CardLayout();
  ```

- 使用容器的 setLayout() 方法为容器设置布局，例如：

  ``` java
  con.setLayout(card);
  ```

- 容器调用 add(String s,Component b) 将组件 b 加入容器，并给出了显示该组件的代号 s 。组件的代号是一个字符串，和组件的名字没有必然联系，但是不同的组件代号必须互不相同。最先加入 con 的是第一张,依次排序。

- 创建的布局 card 用 CardLayout 类提供的 show() 方法，显示容器 con 中组件代号为 s 的组件：

  ``` java
  card.show(con,s);
  ```

  也可以按组件加入容器的顺序显示组件：card.first(con) 显示 con 中的第一个组件；card.last(con) 显示 con中 的最后一个组件：card.next(con）显示当前正在被显示的组件的下一个组件；card.previous(con) 显示当前正在被显示的组件的前一个组件。

### GridLayout 表格布局

GridLayout 是使用较多的布局编辑器，其基本布局策略是把容器划分成若干行乘若干列的网格区域，组件就位于这些划分出来的小格中。使用 GridLayout 布局的容器调用方法 add(Component c) 将组件 c 加入容器，组件进入容器的顺序将按照第一行第一个、第一行第二个……、第一行最后一个、第二行第一个、……、最后一行最后一个排列。使用 GridLayout 布局的容器最多可添加m×n个组件。GridLayout 布局中每个网格都是相同大小并且强制组件与网格的大小相同。

### null 空布局

可以把一个容器的布局设置为 null 布局（空布局)。空布局容器可以准确地定位组件在容器中的位置和大小。setBounds(int a,int b,int width,int height)方法是所有组件都拥有的一个方法，组件调用该方法可以设置本身的大小和在容器中的位置。

### BoxIayout 布局

- javax.swing 包中的 Box容器称为一个盒式容器,在策划程序的布局时,可以利用容器的嵌套,将某个容器嵌入几个盒式容器,达到布局目的。

- 使用 Box类的类（静态）方法 createHorizontalBox() 获得一个行型盒式容器：使用 Box 类的类（静态）方法 createVerticalBox() 获得一个列型盒式容器。

- 想控制盒式布局容器中组件之间的距离,需使用水平支撑或垂直支撑。
 Box 类调用静态方法 createHorizontalStrut(int width) 可以得到一个不可见的水平 Strut 对象，称为水平支撑。该水平支撑的高度为0，宽度是width。
Box 类调用静态方法 create VerticalSttrut(int height) 可以得到一个不可见的垂直 Strut 对象，称之为垂直支撑。参数 height 决定垂直支撑的高度，垂直支撑的宽度为0。

## 处理事件

### 事件源

能产生事件的对象都可以称之为事件源。

### 监视器

对事件源设置的监视，对发生的事件做监控处理。

### ActionEvent 事件

- 事件源

  文本框、按钮、菜单项、密码框和单选按钮都可以触发该事件。按钮被点击、单选按钮被单选、菜单项选中、编辑框获得焦点后获得回车键都会触发。
  

### ItemEvent 事件

- 事件源

  选择框、下拉列表框都可以触发该事件，选择框状态改变、下拉列表某项被选中会触发。

### DocumentEvent 事件

- 事件源

  文本区，文本区文档发生变化，事件触发，用户改变文档区中维护的文档时事件会触发。

### MouseEvent 事件

- 事件源

  任何组件都能发生鼠标事件，如鼠标进入组件、退出组件、在组件上方单击鼠标、拖动鼠标等都能触发。

### 处理接口事件

![image-20201215220900252](C:\Users\HZN\Desktop\笔记\Java 桌面端GUI编程.assets\image-20201215220900252.png)

## 案例

### 创建自定义窗口类的案例

``` java
import javax.swing.*;
class HelloWord{
    public static void main(String[] args) {
       Window window = new Window();
    }
}

class Window extends JFrame{
    Window(){
        super("测试窗口");//设置标题
        setBounds(200, 200, 400, 600);//设置位置和大小
        setVisible(true);//设置为可见
    }
}
```

### 创建监视器处理按钮点击事件

``` java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

class HelloWord{
    public static void main(String[] args) {
       Window window = new Window();
    }
}

class Window extends JFrame{
    Window(){
        super("测试窗口");//设置标题
        JLabel label = new JLabel("请点击按钮");
        JButton button = new JButton("命令按钮");
        setLayout(new FlowLayout());
        add(label);
        add(button);
        setBounds(200, 200, 400, 600);//设置位置和大小
        setVisible(true);//设置为可见

        ActionListener listener = new ButtonListener(label);
        button.addActionListener(listener);
    }
}

class ButtonListener implements ActionListener{
    JLabel label;
    ButtonListener(JLabel label){
        this.label = label;
    }
    public void actionPerformed(ActionEvent e) {
        label.setText("按钮被单击了");
    }
}
```

注意事项：

![image-20201215224025027](\Java 桌面端GUI编程.assets\image-20201215224025027.png)

GUI界面：

![image-20201215225844714](\Java 桌面端GUI编程.assets\image-20201215225844714.png)