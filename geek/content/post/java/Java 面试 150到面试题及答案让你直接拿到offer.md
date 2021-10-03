title: Java 面试 150到面试题及答案让你直接拿到offer
author: 知识铺
date: 2021-10-03 11:33:33
tags: [Java]

### 1. 什么是Java？

Java 是一种计算机编程语言，具有并发性、基于类和对象导向。对象导向软件开发的优势如下：

- 代码的模块化开发，便于维护和修改。
- 代码的可重复性。
- 提高了代码的可靠性和灵活性。
- 加深对代码的理解。

### 2. OOP 的概念是什么？

对象导向编程 （OOP） 包括：

- 抽象化
- 封装
- 多态性
- Inheritance
- 预定义的类型必须是对象
- 用户定义的类型必须是对象
- 操作必须通过向对象发送消息来执行

### 3. 提及Java的某些功能

在 java 的流行中发挥重要作用的一些功能如下：

- 对象导向
- 独立平台
- 高性能
- 多线程
- 便携式
- 安全

java 中的 Helloworld 示例代码如下所示：

*世界好*

```
public class Helloworld{
     
public static void main(String args[])
{  
    System.out.println("Hello World");  
}  
     
}
```

### 4. Java 是否 100% 面向对象？

不是 100%Java 不满足所有 OOP 条件（预定义的类型必须是对象），因为它使用八种原始数据类型（Boolean、字节、字符、int、浮子、双、长、短）这些数据类型不是对象。

### 5. 什么是抽象？

[抽象](https://www.javacodegeeks.com/2014/07/abstraction-in-java.html)是将想法与特定实例分离的过程，因此，根据它们自己的功能而不是实施细节来发展课程。Java 支持创建和存在暴露界面的抽象类，但不包括所有方法的实际实现。抽象技术旨在将一个类的实现细节与其行为分开。

摘要类 人如下。它有一个抽象的方法得到名。

*抽象类人*

```
public abstract class Person  
{  
    public abstract String getName(); 
}
```

员工类扩展抽象类人员。方法获取名称返回员工的姓名属性。

*员工类*

```
public class Employee extends Person   
{  
    private String name;
     
    public Employee(String name)
    {
      this.name = name;
    }
    public String getName()
    {
       return this.name;
    }
    public static void main (String args[])  
    {  
        Employee employee = new Employee("John Wilson");
         
        System.out.println("Employee's Name "+ employee.getName()); 
         
        Person person = new Employee("Thomas Smith");
         
        System.out.println("Employee-Person's Name "+ person.getName());
         
         
    }  
} 
```

### 6. 什么是封装？

[封装](https://www.javacodegeeks.com/2013/04/the-three-greatest-paragraphs-ever-written-on-encapsulation.html)为对象提供了隐藏其内部特征和行为的能力。每个对象都提供了许多方法，其他对象可以访问这些方法并更改其内部数据。在 Java，有三个访问修饰器：公共、私人和受保护的。每个修饰器都对其他类别（相同或外部包）施加不同的访问权限。使用封装的一些优点如下：

- 每个对象的内部状态都通过隐藏其属性来保护。
- 它增加了代码的可用性和维护性，因为对象的行为可以独立更改或扩展。
- 它通过防止物体以不受欢迎的方式相互交互来改善模块化。

可以[在此](http://examples.javacodegeeks.com/java-basics/encapsulation-in-java/)处参考的教程，了解有关封装的更多详细信息和示例。

具有属性 Id 和名称的示例类学生将作为封装示例显示。

*学生班*

```java
public class Student{  
 private int id;  
 private String name;  
   
 public void setId(int id)
 {
   this.id = id;
 }
  
 public void setName(String name)
 {
   this.name = name;
 }
  
 public int getId()
 {
   return this.id;
 }
  
 public String getName()
 {
   return this.name;
 }
   
public static void main(String args[])
{  
  Student student=new Student();  
  student.setId(1034);
  student.setName("David Smith");
 
  System.out.println("Student id "+ student.getId());
  System.out.println("Student name "+ student.getName());
     
}  
 
}  
```

### 7. 抽象和封装有什么区别？

抽象和封装是互补的概念。一方面，抽象侧重于物体的行为。另一方面，封装侧重于对象行为的实现。封装通常是通过隐藏有关物体内部状态的信息来实现的，因此，可以被看作是一种用于提供抽象的策略。

### 8. 什么是多态性？

[多态性](https://www.javacodegeeks.com/2013/04/polymorphism-and-inheritance-are-independent-of-each-other.html)是编程语言为不同基础数据类型呈现相同界面的能力。多态型是一种操作也可以应用于其他类型的值的类型。

可以在下面看到车辆界面有方法提高速度的示例。卡车、火车和飞机实现车辆接口，该方法将速度增加到与车辆类型相关的适当速度。

![Java面试问题 - 多态性](https://cdn.jsdelivr.net/gh/zshipu/images/202110031555825.webp)

### 9. 多态性是什么类型？

Java有两种多态性：

- 编译时间多态性（静态绑定） - 方法超载
- 运行时间多态性（动态绑定） - 方法压倒

可以通过方法超载和方法超载来执行多态性。

| **编译时间**                                                 | **运行**                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 类的方法具有相同的名称。每个方法都有不同数量的参数。它可以具有不同类型和顺序的参数。 | 子类具有以超类方法命名的方法。它具有作为超级类方法的护身虫数量、参数类型和返回类型。 |
| 方法超载是添加到方法行为。它可以扩展到方法的行为。           | 方法压倒一切是修改方法的行为。                               |
| 超载方法的签名不同。                                         | 覆盖方法将具有完全相同的签名。                               |
| 在这种情况下，不需要继承。                                   | 继承是重新启用的。                                           |

计算器类超载方法减去的示例代码如下所示：

*计算器类*

```
public class Calculator {
 
public int subtract(int a, int b)
{
   return a-b;
}
public double subtract( double a, double b)
{
 return a-b;
}
 
public static void main(String args[])
{
  Calculator calculator = new Calculator();
  System.out.println("Difference of 150 and 12 is " +calculator.subtract(150,12));
  System.out.println("Difference of 15.5 and 15.4 is " +calculator.subtract(15.50,15.40));
}}
```

方法覆盖如下形状类。形状有一种方法得到区域。

*形状类*

```
public class Shape
{  
  public void getArea(){System.out.println("Shape Area");}  
}
```

矩形类覆盖获取区域方法，该方法的实现特定于矩形。覆盖注释用于向编译器指示该方法被覆盖。使用注释可改进代码的可读性。

*矩形类*

```
public class Rectangle extends Shape{ 
   
  @Override
  public void getArea()
  {
    System.out.println("Rectangle Area");
   
  }  
   
   
 
  public static void main(String args[])
  {  
    Shape shape = new Shape();
     
    shape.getArea();
     
    Rectangle rectangle = new Rectangle();  
     
    rectangle.getArea();  
  }  
}
```

### 10. 什么是继承？

[继承](https://www.javacodegeeks.com/2013/08/multiple-inheritance-in-java-and-composition-vs-inheritance.html)提供了一个对象，能够获得另一类，称为基础类的领域和方法。继承提供了代码的可重复使用性，可用于在不修改代码的情况下向现有类别添加附加功能。

样本类哺乳动物如下所示，其中有一个构造器。

*哺乳动物类*

```
public class Mammal{  
 
 public Mammal()
 {
   System.out.println("Mammal created"); 
 }
  
}

```

人类扩展哺乳动物，它有一个默认的构造器。示例代码如下所示。

*男子类*

```
public class Man extends Mammal{ 
 
 public Man()
 {  
   System.out.println("Man is created");  
 }  
}

```

通过创建使用默认构造器的"人"实例来测试继承。示例代码显示以证明继承。

*测试继承类*

```
public class TestInheritance{
 
public static void main(String args[])
{  
   Man man = new Man();  
 }  
}
```

### 11. 什么是组成？

[构图](https://www.javacodegeeks.com/2018/09/composition-in-java-jep-draft.html)完全像聚合，只是"部分"的寿命由"整体"控制。此控制可能是直接的或过渡性的。即，"整体"可能直接负责创建或销毁"部分"，或者它可能接受已创建的部分，然后将其传递给承担其责任的其他整体。

样板类汽车如下所示，以演示轮胎、车门、车窗和转向的组成。

*汽车类*

```
public class Car 
{  
  private Tire[] tires;
   
  private Door[] doors;
   
  private Steering steering;
   
  private Window[] windows;
}
 
class Tire
{
     
}
   
class Door
{
     
}
 
class Steering
{
     
}
 
class Window
{
     
}
```

### 12. 什么是关联？

关联表示一个实例向另一个实例发送消息的能力。这通常使用指点或参考实例变量实现，尽管它也可能作为方法参数或创建本地变量实施。

### 13. 什么是聚合？

聚合是典型的整体/部分关系。这与关联完全相同，但实例不能具有循环聚合关系。

示例类 人员如下所示，以显示与地址的聚合关系。

*人员类*

```
public class Person
{  
  private Address address;
 
}
 
class Address
{
  private String city;
   
  private String state;
   
  private String country;
   
  private String line1;
   
  private String line2;
 
}
```

## B. 关于Java的一般问题

### 14. 什么是合资企业？

Java 虚拟机 （JVM） 是一种可以执行 Java[字形码](https://www.javacodegeeks.com/2013/12/mastering-java-bytecode.html)的流程[虚拟机](https://www.javacodegeeks.com/2013/12/part-1-of-3-synopsis-of-articles-videos-on-performance-tuning-jvm-gc-in-java-mechanical-sympathy-et-al.html)。每个 Java 源文件被编译为字形码文件，该文件由 JVM 执行。

### 15. 为什么 Java 被称为平台独立编程语言？

Java 旨在允许构建可在任何平台上运行的应用程序程序，而无需由程序员为每个单独的平台重写或重新编译。Java 虚拟计算机之所以能够实现这一点，是因为它知道基础硬件平台的具体指令长度和其他特殊性。

### 16. Jdk 和 Jre 有什么区别？

Java 运行时间环境 （JRE） 基本上是执行Java程序的 Java 虚拟机 （JVM）。它还包括用于苹果执行的浏览器插件。Java 开发工具包 （JDK） 是 Java 的全功能软件开发工具包，包括 JRE、编译器和工具（如[JavaDoc](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html)和[Java Debugger），](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/jdb.html)以便用户开发、编译和执行 Java 应用程序。

| **JDK**                                  | **JRE**                                             |
| ---------------------------------------- | --------------------------------------------------- |
| JDK 代表术语 ：Java 开发套件。           | JRE 代表术语：Java运行时间环境。                    |
| JDK 是编译、记录和包装 Java 软件的工具。 | JRE 是一个运行时间环境。Java 字节代码在环境中执行。 |
| JDK 拥有 JRE 和开发工具。                | JRE 是合资企业的实现                                |

### 17. 静态关键字是什么意思？

静态关键字表示可以访问成员变量或方法，而无需对所属类进行说明。

示例静态方法，如下所示：

*静态方法*

```
static void printGreeting()  
    {
     
     
    }
```

### 18. 你能在Java超越私人或静态方法吗？

用户不能覆盖 Java[中的静态方法](https://www.javacodegeeks.com/2012/05/java-static-methods-can-be-code-smell.html)，因为方法覆盖基于运行时的动态绑定，静态方法在编译时间静态绑定。静态方法与类的任何实例无关，因此概念不适用。

### 19. 能否在静态上下文中访问非静态变量？

Java 中的静态变量属于其类别，其值在所有实例中保持不变。当类由 JVM 加载时，将初始化静态变量。如果的代码尝试访问非静态变量，而没有任何实例，编译器将投诉，因为这些变量尚未创建，并且它们与任何实例无关。

### 20. Java 支持的数据类型是什么？

Java 编程语言支持的八种原始数据类型是：

- byte
- short
- int
- long
- float
- double
- boolean
- char

### 21. 什么是Autoboxing和Unboxing？

Autoboxing是[Java 编译器在](https://www.javacodegeeks.com/2013/07/java-generics-tutorial-example-class-interface-methods-wildcards-and-much-more.html)原始类型和相应的对象包装类之间进行的自动转换。例如，编译器将 int 转换为[整数](https://docs.oracle.com/javase/7/docs/api/java/lang/Integer.html?is-external=true)，将双转为[双](https://docs.oracle.com/javase/7/docs/api/java/lang/Double.html)等。如果转换是相反的，此操作称为Unboxing。

### 22. Java的功能覆盖和超载是什么？

当同一类中的两种或两种以上方法具有完全相同的名称，但参数不同时，Java 中会发生方法超载。另一方面，当儿童类重新定义与父类相同的方法时，方法覆盖被定义为案例。覆盖方法必须具有相同的名称、参数列表和返回类型。压倒一切的方法可能不限制其覆盖的方法的访问。

### 23. 什么是构造器？

当创建新对象时，构造器被调用。每个班[级都有一个构造器](https://www.javacodegeeks.com/2014/01/which-is-better-option-cloning-or-copy-constructors.html)。如果程序员没有为类提供构造器，Java 编译器 （Javac） 将为该类创建默认构造器。

java 中的默认构造器如下示例所示：

*默认构造器*

```
public Man()
{  
  System.out.println("Man is created");  
}
```

取参数的构造器如下示例所示：

*构造 函数*

```
private String name;
     
    public Employee(String name)
    {
      this.name = name;
    }
```

### 24. 什么是构造器超载？

构造器超载类似于 Java 中的方法超载。可以为单个类创建不同的构造器。每个构造器必须有自己的唯一参数列表。

### 25. 什么是复制构造器？

最后，Java 确实支持像 C++ 这样的文稿构造器，但区别在于 Java 不会创建默认副本构造器，如果不编写自己的文稿构造器。

员工类的复制构造器如下所示：

*复制构造器*

```
public class Employee extends Person   
{  
    private String name;
     
    public Employee(String name)
    {
      this.name = name;
    }
     
    public Employee(Employee emp)
    {
      this.name = emp.name;
    }
     
}
```

### 26. Java 是否支持多种继承？

不，Java 不支持多重继承。每个类只能在一个类上扩展，但能够实现多个接口。

![Java面试问题 - 多重继承](https://cdn.jsdelivr.net/gh/zshipu/images/202110031555827.webp)

### 27. 界面和抽象类有什么区别？

Java 提供并支持[创建抽象类](http://examples.javacodegeeks.com/java-basics/java-abstract-class-example/)和界面。这两个实施都有一些共同的特点，但在以下特征上有所不同：

- 界面中的所有方法都是隐含抽象的。另一方面，抽象类可能包含抽象和非抽象方法。
- 一个类可以实现多个接口，但只能扩展一个抽象类。
- 为了让一个类实现接口，它必须实施其所有声明的方法。但是，类可能无法实施抽象类的所有声明方法。虽然，在这种情况下，子类也必须被宣布为抽象。
- 抽象类可以实现接口，甚至无需提供界面方法的实现。
- 在 Java 界面中声明的变量默认为最终变量。抽象类可能包含非最终变量。
- 默认情况下，Java 界面的成员是公开的。抽象类的成员可以是私人的、受保护的或公开的。
- 界面绝对抽象，无法刻例化。抽象类也不能被刻录，但如果包含主要方法，则可以调用。

此外，请查看[JDK 8 的抽象类和界面差异](https://www.javacodegeeks.com/2014/04/abstract-class-versus-interface-in-the-jdk-8-era.html)。

| **接口**                             | **抽象类**                                         |
| ------------------------------------ | -------------------------------------------------- |
| 界面具有方法签名。它没有任何实施。   | 抽象类有抽象的方法和细节要推翻。                   |
| 类可以实现多个接口                   | 在这种情况下，一个类只能扩展一个抽象类             |
| 界面具有所有抽象方法。               | 非抽象方法可以在抽象类中出现。                     |
| 实例属性不能在接口中出现。           | 实例属性可以在抽象类中存在。                       |
| 界面是公开可见的或不可见的。         | 抽象类可以是公共的、私人的和受保护的视网。         |
| 接口的任何更改都会影响实现界面的类。 | 将方法添加到抽象类并实施它不需要更改衍生类的代码。 |
| 界面不能具有构造器                   | 抽象类可以具有构造器                               |
| 界面在性能方面很慢                   | 抽象类在衍生类中执行方法的速度很快。               |

### 28. 什么是参考和传递价值？

当对象按值传递时，这意味着对象的副本被传递。因此，即使对该对象进行了更改，也不会影响原始值。当对象通过参考时，这意味着实际对象没有通过，而是通过对象的引用。因此，外部方法所做的任何更改，也反映在所有地方。

下面显示示例代码，显示按值传递。

*按价值传递*

```
public class ComputingEngine 
{ 
    public static void main(String[] args) 
    { 
        int x = 15;
        ComputingEngine engine = new ComputingEngine();
        engine.modify(x); 
        System.out.println("The value of x after passing by value "+x); 
    } 
    public  void modify(int x) 
    { 
        x = 12; 
    } 
}
```

下面示例显示代码中的参考通过。

*参考通过*

```
public class ComputingEngine 
{ 
    public static void main(String[] args) 
    { 
         
        ComputingEngine engine = new ComputingEngine();
         
        
        Computation computation = new Computation(65);
        engine.changeComputedValue(computation);
         
        System.out.println("The value of x after passing by reference "+ computation.x);
         
    } 
     
   
     
    public void changeComputedValue(Computation computation)
    {
        computation = new Computation();
        computation.x = 40;
    }
}
 
 
class Computation 
{ 
    int x; 
    Computation(int i) { x = i; } 
    Computation()      { x = 1; } 
}
```

### 29. Volatile变量的目的是什么？

[Volatile](https://www.javacodegeeks.com/2018/03/volatile-java-works-example-volatile-keyword-java.html)可变值可由不同的线程修改。他们永远不会有机会阻止和持有锁。每当访问变量时，就会发生同步。使用Volatile可能比锁快，但在某些情况下不会工作。在Java 5中，波动性有效的情况范围扩大：特别是，双检查锁定现在工作正常。

Volatile变量的示例代码如下所示：

*Volatile变量*

```
public class DistributedObject {
 
    public volatile int count = 0;
 
}

```

### 30. 瞬态变量的目的是什么？

即使属于该类的类是序列化的，也不会对瞬态变量进行序列化。

具有瞬态变量的示例类如下所示：

*过渡变量*

```
public class Paper implements Serializable
{
    private int id;
    private String title;
    private String author;
    private transient int version = 1;
     
}
```

### 31. 什么是本地可变和实例变量？

| **本地变量**                                       | **实例变量**                                             |
| -------------------------------------------------- | -------------------------------------------------------- |
| 在方法或构造器中声明本地变量。可以在一个街区内申报 | 实例变量在类中声明。                                     |
| 本地变量需要在使用前初始化。代码不会编译。         | 实例可变初始化是没有必要的。如果不初始化，则使用默认值。 |

### 32. Java 中有什么不同的访问修饰器？

访问修饰器有四种类型：

- 公共 - 从应用程序中的任何地方访问
- 受保护的 - 在包内访问和任何包中的子类
- 包专用（默认） - 可在包内严格访问
- 专用 + 仅在申报的同一类中访问

### 33. 静态绑定和动态绑定之间的差异

| **静态绑定**                       | **动态绑定**               |
| ---------------------------------- | -------------------------- |
| 程序的定义与静态绑定有关           | 动态绑定示例是激活程序     |
| 表示变量的名称是为了静态绑定变量。 | 名称的绑定可以是动态绑定。 |
| 声明的范围是静态绑定的。           | 绑定寿命是动态绑定的。     |

静态绑定示例代码如下所示：

*静态绑定*

```
public class Shape
{  
  public void getArea()
   {
     System.out.println("Shape Area");
    }  
 
 
public static void main(String args[])
  {  
    Shape shape = new Shape();
     
    shape.getArea();
  }
}
```

动态绑定示例代码如下所示：

*动态绑定*

```
public class Rectangle extends Shape{ 
   
   
  public void getArea()
  {
    System.out.println("Rectangle Area");
   
  }  
   
   
   
  public static void main(String args[])
  {  
   
    Shape shape = new Rectangle();  
     
    shape.getArea();  
  }  
}

```

### 34. 什么是包装类？

包装类将 java 原始体转换为对象。因此，原始包装类是一个包装类，它从八个原始数据类型中封装、隐藏或包装数据类型，以便这些数据类型可用于使用其他类或其他类中的方法创建实例化对象。原始包装类在 Java API 中找到。

### 35. 什么是单例，怎样才能使一个单例？

在单顿班，：

- 确保只存在单例类的一个实例
- 提供该实例的全球访问

要创建单例类，：

- 宣布该类的所有构造器为私有
- 提供静态方法，返回对实例的引用

下面的示例代码显示双重检查单例类实现。

*单例类*

```
public class DoubleCheckedSingleton {
    private static volatile DoubleCheckedSingleton instance;
    public static DoubleCheckedSingleton getInstance() {
        if (instance == null) {
            synchronized (DoubleCheckedSingleton .class) {
                if (instance == null) {
                    instance = new DoubleCheckedSingleton();
                }
            }
        }
        return instance;
    }
  
}
```

## C.Java线程

### 36. 过程和线程之间有何区别？

过程是程序的执行，而线程是过程中的单个执行序列。过程可以包含多个线程。螺纹有时称为轻量级过程。

| **过程**                               | **线程**                                         |
| -------------------------------------- | ------------------------------------------------ |
| 过程与执行程序有关。                   | 过程由多个重物组成。                             |
| 过程使用过程间通信相互交流。           | 过程的线程可以相互通信。                         |
| 流程可以控制儿童过程。                 | 过程的螺纹可以控制其他线程。                     |
| 父级过程中的任何修改都不会改变儿童流程 | 主线程中的任何修改都可能影响过程其他线程的行为。 |
| 进程在单独的内存空间中执行。           | 线程在共享内存空间中执行。                       |
| 操作系统控制着罗塞。                   | 软件的开发人员可以控制线程的使用。               |
| 流程相互独立。                         | 线程相互依赖。                                   |

### 37. 解释创建线程的不同方法。你更喜欢哪一个， 为什么？

有三种方法可用于创建线程：

- 类可能会扩展[线程](https://docs.oracle.com/javase/7/docs/api/java/lang/Thread.html)类。
- 类可以实现[可运行界](https://docs.oracle.com/javase/7/docs/api/java/lang/Runnable.html)面。
- 应用程序可以使用[执行器](https://docs.oracle.com/javase/7/docs/api/java/util/concurrent/Executor.html)框架，以便创建螺纹池。

可运行界面是首选，因为它不需要对象继承线程类。如果的应用设计需要多次继承，只有界面才能帮助。此外，螺纹池非常高效，可以非常容易地实现和使用。

### 38. 在高级别中解释可用的线程状态。

在执行过程中，线程可以位于以下[状态](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html)之一：

- [新](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html#NEW)： 线程已准备好运行， 但不一定立即开始运行。
- [可运行](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html#RUNNABLE)：Java 虚拟机 （JVM） 正在积极执行线程的代码。
- [已阻止](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html#BLOCKED)：在等待监视器锁时，线程处于被阻止状态。
- [等待](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html#WAITING)： 螺纹等待另一个线程执行特定操作。
- [TIMED_WAITING：](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html#TIMED_WAITING)螺纹等待另一个线程执行特定操作，直至指定的等待时间。
- [终止](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html#TERMINATED)： 线程已完成执行。

### 39. 同步的方法和块有什么区别？

在 Java 编程中，每个对象都有一个锁。线程可以通过使用同步关键字获取对象的锁。同步关键字可以应用于方法级别（粗粒锁）或代码块级（细粒度锁）。

### 40. 线程同步如何在监视器内部发生？

合资企业使用锁与监视器一起。监视器基本上是一个守护者，它监视同步代码序列，并确保一次只执行一个线程执行同步代码。每个监视器都与对象引用关联。在获取锁之前，线程不允许执行代码。

### 41. 什么是僵局？

当[两个过程等待对方完成](https://www.javacodegeeks.com/2013/01/java-deadlock-example-how-to-analyze-deadlock-situation.html)，然后再继续时，就会发生一种情况。结果是，这两个过程都无休止地等待。

### 42. 如何确保 N 线程能够在不陷入僵局的情况下访问 N 资源？

使用 N 线程时避免死锁的一个非常简单的方法是在锁上强制每个螺纹遵循该命令。因此，如果所有线程都以相同的顺序锁定和解锁粘层，则不会出现任何死锁。

### 43. Java的等待和睡眠方法有什么区别？

|                       | ** Wait**                                                    | **Sleep**                                                    |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Call on**           | current thread synchronizes on the lock object when there is a call on the object. | Call on a Thread happens on the currently executing thread.  |
| **Synchronized**      | Synchronized is used to access the same Object from multiple threads.. | Synchronized is used to sleep over the Sleeping thread from multiple threads. |
| **Hold lock**         | release the lock for other objects to have the chance to execute | keep lock for at least t times if timeout specified or somebody interrupt. |
| **Wake up condition** | until call notify(), notifyAll() from object                 | until at least time expire or call interrupt().              |
| **Usage**             | for time-synchronization                                     | for multi-thread-synchronization                             |

## D.Java系列

### 44. Java 收藏框架的基本界面是什么？

[Java 集合框架](https://docs.oracle.com/javase/7/docs/technotes/guides/collections/overview.html)提供了一套精心设计的界面和类，支持对象集合上的操作。位于 Java 收藏框架中的最基本界面是：

- [集合](https://docs.oracle.com/javase/7/docs/api/java/util/Collection.html)，它表示一组称为其元素的对象。
- [集](https://docs.oracle.com/javase/7/docs/api/java/util/Set.html)合，这是一个集合，不能包含重复的元素。
- [列表](https://docs.oracle.com/javase/7/docs/api/java/util/List.html)，这是一个有序的集合，可以包含重复的元素。
- [地图](https://docs.oracle.com/javase/7/docs/api/java/util/Map.html)，这是一个对象，映射键的值，不能包含重复的键。

![Java面试问题 - 收集层次结构](https://cdn.jsdelivr.net/gh/zshipu/images/202110031555828.webp)

### 45. 为什么集合不扩展可克隆和可串行界面？

[集合](https://docs.oracle.com/javase/7/docs/api/java/util/Collection.html)界面指定称为元素的对象组。集合的每一个具体实施可以选择自己的方式来维护和订购其元素。某些集合允许重复键，而其他一些集合不允许。在处理实际实施时，克隆或序列化的语义和影响发挥作用。因此，收集的具体实施应决定如何克隆或序列化。

### 46. 什么是传子器？

[传回器](https://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html)界面提供了许多方法，能够在任何[集合](https://docs.oracle.com/javase/7/docs/api/java/util/Collection.html)中重做。每个 Java 集合都包含返回传回器实例的传回器方法。迭代器能够在迭代过程中[从底层集合中删除元素](https://www.javacodegeeks.com/2011/05/avoid-concurrentmodificationexception.html)。

### 47. 传子器和列表器之间存在哪些差异？

以下元素的差异如下：

- [传历器](https://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html)可用于穿越[集](https://docs.oracle.com/javase/7/docs/api/java/util/Set.html)合和[列表](https://docs.oracle.com/javase/7/docs/api/java/util/List.html)集合，而[列表可以](https://docs.oracle.com/javase/7/docs/api/java/util/ListIterator.html)仅用于在列表上进行重定。
- 传转器只能在前进方向上穿越集合，而列表信息器只能在两个方向上穿过列表。
- ListItator 实现传道界面并包含额外的功能，例如添加元素、替换元素、获取前一个和下一个元素的索引位置等。

### 48. 故障快速与故障安全有何区别？

[传联器的](https://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html)故障安全属性与基础集合的克隆配合工作，因此，它不会受到集合中任何修改的影响。java.util 包中的所有收集类都快速故障，而 java.util.并发中的收集类是故障安全的。故障快速重复器抛出[并发修饰例外](http://examples.javacodegeeks.com/java-basics/exceptions/java-util-concurrentmodificationexception-how-to-handle-concurrent-modification-exception/)，而故障安全的重复器从不抛出这样的例外。

### 49. 哈希马普在Java是如何工作的？

[Java的哈希马普存储关键值对](https://www.javacodegeeks.com/2014/03/how-hashmap-works-in-java.html)。[哈希马普](https://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html)需要一个哈希功能，并使用[哈希码](https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#hashCode())和等价方法，以便分别放置和检索到和取回集合的元素。调用放放方法时，HashMap 计算密钥的哈希值，并将对存储在集合内的相应索引中。如果密钥存在，则其值将随新值进行更新。哈希马普的一些重要特征是其容量、负载因子和阈值调整。

### 50. 哈希码（）和等于（）方法的重要性是什么？

在 Java 中，[哈希马普](https://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html)使用[哈希代码](https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#hashCode())并[等于](https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#equals(java.lang.Object))方法确定键值对的索引并检测重复。更具体地说，使用哈希代码方法来确定指定密钥将存储在哪里。由于不同的密钥可能产生相同的哈希值，使用等值方法，以确定指定的密钥是否真的存在于集合中。因此，这两种方法的实施对于哈希马普的准确性和效率至关重要。

### 51. 哈希马普和哈希布有什么区别？

[哈希地图](https://docs.oracle.com/javase/7/docs/api/java/util/HashMap.html)和[哈希表](https://docs.oracle.com/javase/7/docs/api/java/util/Hashtable.html)类都实现了地图界面，因此具有非常相似的特征。但是，它们在以下功能上有所不同：

- 哈希马普允许空键和值的存在，而哈希表不允许空键和空值。
- 哈希表是同步的，而哈希马普不是。因此，哈希马普在单线程环境中是首选，而哈希表则适用于多线程环境。
- 哈希马普提供其一组密钥，Java 应用程序可以对其进行重做。因此，哈希马普是故障快。另一方面，哈希表提供了其键的[列举](https://docs.oracle.com/javase/7/docs/api/java/util/Enumeration.html)。
- 哈希表类被认为是一个传统类。

### 52. 阵列和阵列列表有何区别？何时会在阵列列表上使用阵列？

[阵列](https://docs.oracle.com/javase/7/docs/api/java/lang/reflect/Array.html)和[阵列列表](https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html)类在以下功能上有所不同：

- 阵列可以包含原始或对象，而阵列列表只能包含对象。
- 阵列具有修复大小，而阵列列表是动态的。
- 阵列列表提供了更多的方法和功能，如[添加所有](https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html#addAll(java.util.Collection))，[删除所有](https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html#removeAll(java.util.Collection))，[传动器](https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html#iterator())等。
- 对于原始数据类型的列表，集合使用Autoboxing来减少编码工作。但是，这种方法在处理固定大小原始数据类型时会减慢速度。

| **数组**                           | **阵列列表**                               |
| ---------------------------------- | ------------------------------------------ |
| 阵列不应具有不同数据类型的值       | 阵列列表可以具有不同数据类型的值。         |
| 声明时定义了 arrray 的大小         | 阵列列表的大小可以动态更改                 |
| 必须指定该索引才能在阵列中添加数据 | 不需要在阵列列表中指定索引                 |
| 阵列不是类型参数化                 | 阵列列表可以进行类型参数化。               |
| 阵列可以具有原始数据类型以及对象   | 阵列列表只能有对象，不允许使用原始数据类型 |

### 53. 阵列列表和链接列表有什么区别？

[阵列列表](https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html)和[链接列表](https://docs.oracle.com/javase/7/docs/api/java/util/LinkedList.html)类都实现了列表界面，但在以下功能上有所不同：

- 阵列列表是一个由 Array 支持的基于索引的数据结构。它提供随机访问其元素的性能等于 O（1）。另一方面，LinkedList 将其数据存储为元素列表，每个元素都链接到其前一个和下一个元素。在这种情况下，对元素的搜索操作的执行时间等于 O（n）。
- 与 ArrayList 相比，链接列表中的元素的插入、添加和删除操作更快，因为当组件添加到集合中的任意位置时，无需调整阵列大小或更新索引。
- 链接列表消耗的内存比 ArrayList 多，因为链接列表中的每个节点都存储两个参考项，一个用于其以前的元素，另一个用于其下一个元素。

请查看的文章[阵列列表与链接列表](https://www.javacodegeeks.com/2013/12/arraylist-vs-linkedlist.html)。

### 54. 可比性和比较器有何区别？

- Java 提供[可比](https://docs.oracle.com/javase/7/docs/api/java/lang/Comparable.html)界面，其中仅包含一种方法，称为[比较托](https://docs.oracle.com/javase/7/docs/api/java/lang/Comparable.html#compareTo(T))。此方法比较两个对象，以便在它们之间施加顺序。具体来说，它返回负整数、零或正整数，以表示输入对象小于、等于或大于现有对象。
- Java 提供[比较器](https://docs.oracle.com/javase/7/docs/api/java/util/Comparator.html)界面，其中包含两种方法，称为[比较](https://docs.oracle.com/javase/7/docs/api/java/util/Comparator.html#compare(T, T))和[等价](https://docs.oracle.com/javase/7/docs/api/java/util/Comparator.html#equals(java.lang.Object))。第一种方法比较了两个输入参数，并在它们之间施加了顺序。它返回负整数、零或正整数，以表示第一个参数小于、等于或大于第二个参数。第二种方法需要对象作为参数，旨在确定输入对象是否等于比较器。只有当指定对象也是比较器并且它施加与比较器相同的顺序时，该方法才会返回真实。

### 55. 什么是 Java 优先队列？

[优先级排是](https://docs.oracle.com/javase/7/docs/api/java/util/PriorityQueue.html)一个不受限制的队列，基于优先级堆，其元素按其自然顺序排列。在其创建时，可以提供一个比较器，负责订购优先级权限的元素。优先级权不允许[空值](http://examples.javacodegeeks.com/java-basics/exceptions/java-lang-nullpointerexception-how-to-handle-null-pointer-exception/)、不提供自然顺序的对象或不具有与它们相关的任何比较器的对象。最后，Java 优先排序不安全，它需要 O（日志）时间进行排序和排版操作。

### 56. 对大 O 符号了解哪些内容，能举一些不同数据结构的例子吗？

[Big-O 符号](https://www.javacodegeeks.com/2011/04/simple-big-o-notation-post.html)仅描述算法在最坏情况下随着数据结构中的元素数量的增加而缩放或执行得有多好。大 O 符号也可用于描述其他行为，如内存消耗。由于收集类实际上是数据结构，通常使用大 O 符号根据时间、内存和性能选择最佳实现使用。大 O 符号可以很好地指示大量数据的性能。

### 57. 使用无序阵列与订购阵列之间的权衡是什么？

订购阵列的主要优点是搜索时间具有 O（log n）的时间复杂性，而未排序阵列（O （n）） 的复杂性。有序阵列的缺点是插入操作具有 O（n）的时间复杂性，因为必须移动具有较高值的元素，以便为新元素腾出空间。相反，未排序阵列的插入操作需要 O（1）的恒定时间。

### 58. 与 Java 收集框架相关的一些最佳实践是什么？

- 根据应用程序的需求选择正确的集合类型，对于其性能至关重要。例如，如果元素的大小是固定的，并且知道先验，将使用[阵列](https://docs.oracle.com/javase/7/docs/api/java/lang/reflect/Array.html)，而不是[阵列列表](https://docs.oracle.com/javase/7/docs/api/java/util/ArrayList.html)。
- 某些收集类允许指定其初始容量。因此，如果对将要存储的元素数量进行估计，可以使用它来避免重置或调整大小。
- 始终使用通用技术来获得类型安全性、可读性和稳健性。此外，通过使用通用，可以避免在运行期间[的类禁用](https://docs.oracle.com/javase/7/docs/api/java/lang/ClassCastException.html)。
- 使用 Java 开发工具包 （JDK） 提供的不可变类作为地图中的密钥，以避免哈[希代码](https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html#hashCode())的实现，并等于自定义类的方法。
- 接口方面的程序而不是实现。
- 返回零长度集合或阵列，而不是返回空，以防基础集合实际上是空的。

### 59. 列举和迭代接口有何区别？

与迭代器相比，[列举](https://docs.oracle.com/javase/7/docs/api/java/util/Enumeration.html)速度是迭代器的两倍，并且使用的记忆非常少。但是，[迭代器](https://docs.oracle.com/javase/7/docs/api/java/util/Iterator.html)比计算安全得多，因为其他线程无法修改当前迭代器所穿越的收集对象。此外，迭代器允许呼叫者从底层集合中删除元素，这在列举中是不可能的。

### 60. 哈希集和树集有什么区别？

[哈希集](https://docs.oracle.com/javase/7/docs/api/java/util/HashSet.html)使用哈希表实现，因此，其元素不进行订购。添加、删除和包含哈希集的方法具有恒定的时间复杂性 O（1）。另一方面，[使用树结构实现树集](https://docs.oracle.com/javase/7/docs/api/java/util/TreeSet.html)。树集中的元素进行排序，因此，添加、删除和包含方法具有 O（logn）的时间复杂性。

## E.垃圾收集器

### 61. Java垃圾收集的目的是什么，何时使用？

收集垃圾的目的是识别和丢弃应用程序不再需要的对象，以便回收和再利用资源。

### 62. 系统.gc （） 和运行时间.gc （） 方法是做什么的？

这些方法可以用作对 JVM 的提示，以便开始收集垃圾。但是，这要由 Java 虚拟机器 （JVM） 立即或稍后开始收集垃圾。

示例类参考对象如下所示，以演示系统.gc 和运行时间.gc 方法的使用情况。



```
public class ReferenceObject
{  
 public void finalize()
 {
    System.out.println("object is garbage collected");
     
 }
 
 public static void main(String args[]){  
  ReferenceObject refObj1=new ReferenceObject();  
  ReferenceObject refObj2=new ReferenceObject();  
  refObj1=null;  
  refObj2=null;  
  System.gc(); 
 
  Runtime.gc(); 
 }  
}
```

### 63. 何时叫定（） ？最终确定的目的是什么？

最终确定的方法由垃圾收集器调用，就在释放对象的内存之前。通常建议在最终确定方法中释放对象所持有的资源。

参考对象类中的最终确定方法如下所示。

*最终确定方法*

```
public class ReferenceObject
{  
 public void finalize()
 {
    System.out.println("object is garbage collected");
     
 }
 }
```

### 64. 如果对象引用设置为无效，垃圾收集器会立即释放该对象所持有的内存吗？

不，该对象将在下一个周期的垃圾收集器中用于垃圾收集。

### 65. Java堆的结构是什么？

[JVM 有一堆](https://www.javacodegeeks.com/2012/07/5-tips-for-proper-java-heap-size.html)是分配所有类实例和阵列内存的运行时间数据区域。它是在合资企业初创公司创建的。物体堆存储器由自动内存管理系统回收，该系统称为垃圾收集器。堆内存由活的和死的物体组成。申请可访问实时对象，不会成为垃圾收集的主题。死物是那些永远不会访问的应用程序，但尚未收集的垃圾收集器。这些物品占据堆存储空间，直到它们最终被垃圾收集者收集。

### 66. 串行垃圾收集器和吞吐量垃圾收集器有什么区别？

吞吐量垃圾收集器使用年轻一代收集器的并行版本，用于具有中到大型数据集的应用程序。另一方面，串行收集器通常足以满足大多数小型应用（现代处理器上需要高达 100MB 的堆）。

### 67. 对象何时有资格在Java收集垃圾？

当 Java 对象无法访问当前使用的程序时，会进行垃圾收集。

### 68. 垃圾收集是否发生在合资企业的永久生成空间中？

垃圾收集确实发生在 PermGen 空间中，如果 PermGen 空间已满或跨过阈值，则可以触发完整的垃圾收集。如果你仔细观察垃圾收集器的输出，你会发现PermGen空间也是垃圾收集。这就是为什么正确调整 PermGen 空间大小对于避免频繁的垃圾收集非常重要的原因。也检查的文章[Java8：永久到元空间](https://www.javacodegeeks.com/2013/02/java-8-from-permgen-to-metaspace.html)。

## F.例外处理

### 69. 已检查的例外和未检查的例外有何区别？

| **Checked Exception**                                        | **Unchecked Exception**                                    |
| ------------------------------------------------------------ | ---------------------------------------------------------- |
| known as compile time exceptions                             | known as Runtime exceptions                                |
| propagated using throws keyword                              | automatically propagated                                   |
| can create custom exception by extending java.lang.Exception class | can create custom exception by extending Runtime exception |

### 70. java 中的例外和错误有什么区别？

[例外](https://docs.oracle.com/javase/7/docs/api/java/lang/Exception.html)类和[错误](https://docs.oracle.com/javase/7/docs/api/java/lang/Error.html)类都是[可投掷](https://docs.oracle.com/javase/7/docs/api/java/lang/Throwable.html)类的子类。例外类用于用户程序应捕获的异常条件。错误类定义了预计不会被用户程序捕获的例外情况。

### 71. 投掷和投掷有什么区别？

投掷关键字用于在程序中明确提出例外。相反，投掷条款用于表示未通过方法处理的例外情况。每个方法必须明确指定哪些例外不处理，以便该方法的呼叫者可以防范可能的例外。最后，多个例外由逗号分开。

| **Throw**                                                   | **Throws**                                         |
| ----------------------------------------------------------- | -------------------------------------------------- |
| Throw is used for throwing an exception explicitly.         | To declar an exception,throws is used.             |
| Using throw only, Checked exceptions can not be propagated. | Using throws, Checked exception can be propagated. |
| Throw is always used with an instance.                      | Throws is always used with a class.                |
| Throw is used inside the method.                            | Throws is used always with the method signature.   |
| You should not throw multiple exception                     | You can declare multiple exceptions.               |

### 72. 最终阻止例外处理的重要性是什么？

无论是否真的抛出了例外，最终的方块总是会被执行。即使在缺少捕获语句和抛出例外的情况下，最终阻止仍将执行。最不需要提及的是，最终的块用于释放资源，如 I/O 缓冲器、数据库连接等。

下面的示例代码显示抛出异常时的最终块。

*最后阻止*

```
public class DivideByZeroException
{  
     public static void main(String []args){  
        try{  
            int a = 1;   
            System.out.println(a/0);  
        }
        catch(Exception exception)
        {
          System.out.println("exception is thrown");
        }
        finally 
        {  
            System.out.println("after the exception is handled");  
        }  
     }  
}
```

### 73. 例外处理后例外对象会发生什么情况？

[例外](https://docs.oracle.com/javase/7/docs/api/java/lang/Exception.html)对象将是在下一次垃圾收集中收集的垃圾。

### 74. 关键字最终完成并最终实现什么目的？

- **最终**关键字用于对类（不可变）、方法（不能覆盖）和变量（常数）施加限制。
- **最后**是一个块，始终执行时，尝试块退出，即使意外的例外发生。
- **最终确定**是一种在销毁对象之前由垃圾收集器清洁或释放资源的方法。

## G. Java苹果

### 75. 什么是苹果？

java 苹果是可以包含在 HTML 页面中的程序，并在支持 java 的客户端浏览器中执行。苹果用于创建动态和交互式 Web 应用程序。

### 76. 解释苹果的生命周期。

苹果可以经历以下状态：

- Init： 每次加载时都会初始化苹果。
- 开始：开始执行一个苹果。
- 停止：停止执行苹果。
- 销毁：在卸下苹果之前进行最后的清理。

![Java面试问题 - 苹果生命周期](https://cdn.jsdelivr.net/gh/zshipu/images/202110031555829.webp)

### 77. 装苹果时会发生什么？

首先，创建了苹果控制类的实例。然后，苹果启动自己，最后，它开始运行。

### 78. 苹果和Java应用程序有什么区别？

Applet 在支持 java 的浏览器中执行，但 Java 应用程序是一个独立的 Java 程序，可以在浏览器之外执行。但是，它们都需要有 Java 虚拟机 （JVM）的存在。此外，Java 应用程序需要具有特定签名的主要方法才能开始执行。Java苹果不需要这样的方法来开始执行。最后，Java 苹果通常使用限制性安全策略，而 Java 应用程序通常使用更宽松的安全策略。

### 79. 对Java苹果有什么限制？

主要出于安全原因，对 Java 苹果施加了以下限制：

- 苹果不能加载库或定义本地方法。
- 苹果通常不能在执行主机上读取或写文件。
- 苹果不能读取某些系统属性。
- 苹果不能建立网络连接，除了它来自主机。
- 苹果不能在执行程序的主机上启动任何程序。

### 80. 什么是不信任的苹果？

不信任的苹果是那些无法访问或执行本地系统文件的 Java 苹果。默认情况下，所有下载的苹果都被视为不可信。

### 81. 通过互联网加载的苹果和通过文件系统加载的苹果有什么区别？

关于苹果通过互联网加载的情况，苹果由苹果类装载机加载，并受苹果安全经理实施的限制。对于从客户端本地磁盘中装载苹果的情况，苹果由文件系统装载机加载。通过文件系统加载的 Applet 允许读取文件、编写文件并在客户端上加载库。此外，通过文件系统加载的苹果可以执行过程，最后，通过文件系统加载的苹果不会通过字形码验证器。

### 82. 什么是苹果类装载机，它提供什么？

当苹果通过互联网加载时，苹果由苹果类装载机加载。类装载机执行 Java 命名空间层次结构。此外，类装载机保证来自本地文件系统的类存在唯一的命名空间，并且每个网络源都存在一个唯一的命名空间。当浏览器将苹果加载到网中时，该苹果的类被放置在与苹果的起源相关的私人命名空间中。然后，类装载机加载的这些类通过验证器。验证器检查类文件是否符合 Java 语言规范。除其他事项外，验证器确保没有堆栈溢出或溢出，并且所有字节代码指令的参数正确。

### 83. 什么是苹果安全经理，它提供什么？

苹果安全经理是一种对Java苹果施加限制的机制。浏览器可能只有一个安全管理器。安全经理是在启动时建立的，之后不能更换、超载、超载或延长。

### 84. 选择和列表有什么区别？

选择以紧凑的形式显示，必须向下拉，以便用户能够查看所有可用选项的列表。只能从"选择"中选择一个项目。[列表](http://examples.javacodegeeks.com/desktop-java/swing/jlist/create-jlist-example/)的显示方式可能为可见多个列表项目。列表支持选择一个或多个列表项目。

### 85. 什么是布局经理？

布局管理器用于在容器中组织组件。

### 86. Scrollbar 和 JScrollPane 有什么区别？

[Scrollbar](https://docs.oracle.com/javase/7/docs/api/java/awt/Scrollbar.html)是一个[组件](https://docs.oracle.com/javase/7/docs/api/java/awt/Component.html)，但不是[一个容器](https://docs.oracle.com/javase/7/docs/api/java/awt/Container.html)。[滚动板](https://docs.oracle.com/javase/7/docs/api/javax/swing/JScrollPane.html)是一个容器。滚动板处理自己的事件并执行自己的滚动。

### 87. 哪些摆动方法是安全的？

只有三种线程安全的方法：重新涂漆、重新验证和无效。

### 88. 说出支持绘画的三个组分类。

[画布](https://docs.oracle.com/javase/7/docs/api/java/awt/Canvas.html)、[框架](https://docs.oracle.com/javase/7/docs/api/java/awt/Frame.html)、[面板](https://docs.oracle.com/javase/7/docs/api/java/awt/Panel.html)和苹果类支持绘画。

### 89. 什么是剪报？

剪裁定义为将油漆操作局限于有限区域或形状的过程。

### 90. 菜单和复选框梅努伊特姆有什么区别？

[复选框梅努伊特姆](https://docs.oracle.com/javase/7/docs/api/java/awt/CheckboxMenuItem.html)类扩展[了菜单类别](https://docs.oracle.com/javase/7/docs/api/java/awt/MenuItem.html)，并支持可能被检查或未检查的菜单项。

### 91. 边界外延的要素是如何组织的？

[边界外延](https://docs.oracle.com/javase/7/docs/api/java/awt/BorderLayout.html)的要素在边界（北部、南部、东部和西部）和集装箱中心组织。

### 92. 网格袋的元素是如何组织的？

[网格袋的](https://docs.oracle.com/javase/7/docs/api/java/awt/GridBagLayout.html)元素是根据网格组织的。元素大小不同，可能占据网格的多个行或列。因此，行和列可能具有不同的大小。

### 93. 窗口和框架有什么区别？

[帧](https://docs.oracle.com/javase/7/docs/api/java/awt/Frame.html)类扩展了[窗口](https://docs.oracle.com/javase/7/docs/api/java/awt/Window.html)类，并定义了可以具有菜单栏的主要应用窗口。

### 94. 剪报和重新粉刷之间有什么关系？

当窗口由 AWT 绘画线重新绘制时，它会将剪贴区域设置为需要重新涂漆的窗口区域。

### 95. 事件-听众界面与事件适配器类之间有何关系？

事件-听众界面定义了特定事件事件处理程序必须实施的方法。事件适配器提供事件-听众界面的默认实现。

### 96. GUI 组件如何处理自己的事件？

GUI 组件可以通过实现相应的事件-听众界面并添加为自己的事件听者来处理自己的事件。

### 97. Java 的布局管理器比传统的窗口系统具有哪些优势？

Java 使用布局管理器在所有窗口平台上以一致的方式布局组件。由于布局管理器与绝对大小和定位无关，他们能够适应窗口系统之间的平台特定差异。

### 98. Java 对所有Swing组件使用的设计模式是什么？

Java 用于所有Swing组件的设计模式是模型视图控制器 （MVC） 模式。

![Java面试问题 - MVC](https://cdn.jsdelivr.net/gh/zshipu/images/202110031555830.webp)

## 伊杰德布克

### 99. 什么是 Jdbc？

[JDBC](https://www.javacodegeeks.com/jdbc-tutorials)是一个抽象层，允许用户在数据库之间进行选择。[JDBC 使开发人员能够在 Java 中编写数据库应用程序](https://www.javacodegeeks.com/2014/03/java-8-friday-java-8-will-revolutionize-database-access.html)，而不必担心特定数据库的基本详细信息。

### 100. 什么是 Jdbc API 组件？

java.sql 包包含：

**接口**：

- Driver
- Connection
- Statement
- PreparedStatement
- CallableStatement
- ResultSet

**类**：

- DriverManager
- SQLException

### 101. 解释司机在 JDBC 中的角色。

JDBC 驱动程序提供 JDBC API 提供的抽象类的供应商特定实现。每个驱动程序必须提供以下接口的 java.sql 包的实现：[连接](https://docs.oracle.com/javase/7/docs/api/java/sql/Connection.html)，[声明](https://docs.oracle.com/javase/7/docs/api/java/sql/Statement.html)，[准备声明](https://docs.oracle.com/javase/7/docs/api/java/sql/PreparedStatement.html)，[可调用状态](https://docs.oracle.com/javase/7/docs/api/java/sql/CallableStatement.html)，[结果集](https://docs.oracle.com/javase/7/docs/api/java/sql/ResultSet.html)和[驱动程序](https://docs.oracle.com/javase/7/docs/api/java/sql/Driver.html).

### 102. 什么是 JDBC 连接接口？

连接界面与数据库保持会话。执行 SQL 语句，并在连接范围内返回结果。连接对象的数据库能够提供描述其表、其支持的 SQL 语法、其存储程序、此连接功能等的信息。此信息是使用 getMetaData 方法获得的。

### 103. 连接池是什么意思？

与数据库的交互成本可能很高，涉及数据库连接的打开和关闭。特别是当数据库客户数量增加时，成本会很高，并且消耗了大量资源。数据库连接池由应用程序服务器启动时获取，并保留在池中。[居住在池中的连接](http://examples.javacodegeeks.com/enterprise-java/hibernate/hibernate-connection-pool-configuration-with-c3p0-example/)会送达连接请求。在连接结束时，请求返回到池中，可用于满足未来的请求。

### 104. JDBC 驾驶员经理班的作用是什么？

驾驶员经理为用户提供管理一组 JDBC 驱动程序的基本服务。它与可用的驱动程序保持联系，并与适当的驱动程序建立数据库连接。

### 105. 目的类是什么。

此方法用于加载将建立数据库连接的驱动程序。

下面显示了类类加载器，以演示类.forname（） 方法的使用。

*类. for 名*

```
public class ClassLoader 
{
 
   public static void main(String[] args) {
 
      try
      {
         Class cls = Class.forName("BasicClass");
          
         .....
          
         System.out.println("Class = " + cls.getName());
          
      }
          
     catch(ClassNotFoundException exception) 
      {
         System.out.println(exception.toString());
      }
       
}
```

### 106. 准备陈述比声明的优势是什么？

准备陈述是预先编组的，因此，[性能要好得多](http://examples.javacodegeeks.com/core-java/sql/batch-statement-execution-example/)。此外，准备陈述对象可以以不同的输入值重复使用其查询。

### 107. 可调用声明的用途是什么？

[可调用状态](https://docs.oracle.com/javase/7/docs/api/java/sql/CallableStatement.html)用于执行存储的程序。存储的程序由数据库存储和提供。存储的程序可能会从用户那里获得输入值，并可能返回结果。高度鼓励使用存储程序，因为它提供了安全性和模块化性。准备可调用状态的方法是可调用状态。

### 108. 在 JDBC 批量处理是什么意思？

批次处理组相关 SQL 对帐单，并在批次大小达到预期阈值时执行多个查询。这使得性能更快。

## J.远程方法调用 （RMI）

### 109. 什么是 Rmi？

Java 远程方法调用 （Java RMI） 是一种 Java API，可执行面向对象的等价物远程程序呼叫 （RPC），支持直接传输序列化 Java 类和分布式垃圾收集。远程方法调用 （RMI） 也可被视为激活远程运行对象上的方法的过程。RMI 提供位置透明度，因为用户认为方法是在本地运行的对象上执行的。在此处查看一些[RMI 提示](https://www.javacodegeeks.com/2013/11/two-things-to-remember-when-using-java-rmi.html)。

### 110. RMI 架构的基本原则是什么？

RMI 架构基于一个非常重要的原则，该原则指出行为的定义和该行为的实现是单独的概念。RMI 允许定义行为的代码和实现该行为的代码保持独立并在单独的 JVM 上运行。

![Java面试问题 - RMI 架构](https://cdn.jsdelivr.net/gh/zshipu/images/202110031555831.webp)

### 111. RMI 架构的层数是哪些？

RMI 架构由以下层组成：

- 存根和骷髅层：这一层位于开发人员视图的正下方。此层负责拦截客户端拨打界面的方法呼叫，并将这些呼叫重定向到远程 RMI 服务。
- 远程参考层：RMI 架构的第二层处理从客户端到服务器远程对象的引用的解释。此层解释和管理从客户端到远程服务对象的引用。该连接是一对一（单播）链接。
- 运输层：此层负责连接参与服务的两个 JVM。此层基于网络中计算机之间的 TCP/IP 连接。它提供基本的连接，以及一些防火墙渗透策略。

### 112. 远程接口在 RMI 中的作用是什么？

远程接口用于识别可能从非本地虚拟计算机调用其方法的接口。任何远程对象必须直接或间接实现此接口。实现远程接口的类应声明正在实施的远程接口，定义每个远程对象的构造器，并为所有远程接口中的每个远程方法提供实现。

### 113. java. rmi. 命名类的作用是什么？

java.rmi.命名类提供了在远程对象注册表中存储和获取远程对象引用的方法。命名类的每个方法都以 URL 格式中的字符串为名称，作为其论点之一。

### 114. RMI 中的绑定是什么意思？

绑定是关联或注册远程对象名称的过程，该名称可在以后使用，以便查找该远程对象。远程对象可以使用命名类的绑定或重绑法与名称关联。

### 115. 使用绑定（）和重新绑定（）命名类方法有何区别？

绑定方法绑定负责将指定的名称绑定到远程对象，而重绑方法负责将指定的名称重新绑定到新的远程对象。如果该名称存在绑定，请替换绑定。

### 116. 使工作成为 RMI 计划所涉及的步骤是什么？

必须涉及以下步骤，以便 RMI 计划正常工作：

- 汇编所有源文件。
- 使用 rmic 的存根生成。
- 开始注册。
- 启动 RMIServer。
- 运行客户端程序。

![Java面试问题 - RMI 流](https://cdn.jsdelivr.net/gh/zshipu/images/202110031555832.webp)

### 117. 存根在RMI中的作用是什么？

远程对象的存根充当客户端的本地代表或远程对象的代理。呼叫者调用本地存根上的方法，该方法负责在远程对象上执行该方法。调用存根的方法时，会经历以下步骤：

- 它启动连接到包含远程对象的远程 JVM。
- 它将参数编组到远程 JVM。
- 它等待方法调用和执行的结果。
- 如果方法未成功执行，则会取消返回值或例外。
- 它将值返回给呼叫者。

### 118. 什么是 DGC，它是如何工作的？

DGC 代表分布式垃圾收集。远程方法调用 （RMI） 使用 DGC 进行自动垃圾收集。由于 RMI 涉及跨 JVM 的远程对象引用，垃圾收集可能相当困难。DGC 使用参考计数算法为远程对象提供自动内存管理。

### 119. 在 RMI 中使用 RMI 安全管理器的目的是什么？

RMI 安全管理器提供可用于 RMI 应用程序的安全管理器，该应用程序使用下载的代码。如果尚未设置安全管理器，RMI 的类装载机将不会从远程位置下载任何类。

### 120. 解释马歇尔和划界。

当应用程序想要将其内存对象通过网络传递给其他主机或将其持续到存储时，内存表示必须转换为合适的格式。此过程称为编组，恢复操作称为分界。

### 121. 解释序列化和去航空化。

Java 提供了一种称为对象序列化的机制，其中对象可以表示为字节序列，并包括对象的数据以及有关对象类型和存储在对象中的数据类型的信息。因此，序列化可以被看作是一种扁平对象的方式，以便存储在磁盘上，然后读回并重新构想。去隔离是将物体从扁平状态转换为活物体的反向过程。

## K. 服务

### 122. 什么是服务？

[servlet](http://examples.javacodegeeks.com/enterprise-java/servlet/sample-java-servlet/)是一个 Java 编程语言类，用于处理客户请求和生成动态 Web 内容。Servlet 主要用于处理或存储 HTML 表格提交的数据、提供动态内容和管理无状态 HTTP 协议中不存在的状态信息。

### 123. 解释服务的结构。

所有服务必须实现的核心抽象是 javax.servlet.Servlet 接口。每个伺服器必须直接或间接地实现它， 无论是通过扩展 javax. servlet. 通用服务或 javax. servlet. http. http 服务。最后，每个服务器能够使用多阅读并行提供多个请求。

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110031555833.webp)

### 124. 苹果和服务有什么区别？

Applet 是客户端 java 程序，在客户端计算机上的 Web 浏览器中运行。另一方面，服务器是运行在 Web 服务器上的服务器侧组件。苹果可以使用用户界面类，而服务没有用户界面。相反，伺服器等待客户的 HTTP 请求，并在每个请求中生成响应。

### 125. 通用服务与赫特普服务有何区别？

通用服务是一个通用和协议独立的服务，实现服务和服务配置界面。扩展通用服务类的伺服项应凌驾于服务方法的覆盖范围。最后，为了开发一个用于 Web 上的 HTTP 服务，使用 HTTP 协议提供服务请求，的服务器必须扩展 HttpServlet。在此处查看[Servlet 示例](http://examples.javacodegeeks.com/tag/servlet/)。

### 126. 解释服务的生命周期。

根据每个客户的要求，Servlet 发动机加载服务并调用其 init 方法，以便初始化伺服。然后，Servlet 对象通过单独调用每个请求的服务方法来处理来自该客户端的所有后续请求。最后，通过调用服务器的销毁方法来删除服务器。

![img](https://cdn.jsdelivr.net/gh/zshipu/images/202110031555834.webp)

### 127. DoGet （） 和 DoPost （）有什么区别？

多吉特： GET 方法附加了请求 URL 上的名称值对。因此，字符数和随后可用于客户请求的值数都有限制。此外，请求的价值是可见的，因此，敏感信息不得以这种方式传递。DOPOST：POST 方法通过将请求的值发送到其内部，克服了 GET 请求施加的限制。此外，要发送的值数量没有限制。最后，外部客户端看不到通过 POST 请求传递的敏感信息。

下面的代码显示了基本服务器类，该类具有要实施的 DoGet 和 doPost 方法。

*获取和张贴方法*

```
public class BasicServlet extends HttpServlet 
{
  
   public void doGet(HttpServletRequest request, HttpServletResponse response)
      throws ServletException, IOException
      {
       
      }
       
    public void doPost(HttpServletRequest request, HttpServletResponse response)
      throws ServletException, IOException
      {
       
      }      
       
}
```

### 128. 网络应用程序是什么意思？

Web 应用程序是 Web 或应用程序服务器的动态扩展。网络应用有两种类型：演示文稿导向和服务导向。面向演示文稿的 Web 应用程序生成交互式网页，其中包含各种类型的标记语言和动态内容，以响应请求。另一方面，以服务为导向的 Web 应用程序实现了 Web 服务的终点。一般来说，Web 应用程序可被视为安装在服务器 URL 名称空间特定子集下的伺服物集。

### 129. 什么是服务器侧包括 （SSI）？

服务器侧包含 （SSI） 是一种简单的解释服务器端脚本语言，几乎完全用于 Web，并嵌入了服务器标签。SSI 最常用的是将一个或多个文件的内容包含到 Web 服务器上的网页中。当浏览器访问网页时，Web 服务器会用相应的服务器生成的超文本替换该网页中的伺服标记。

### 130. 什么是服务链？

伺服链是将一个伺服的输出发送到第二个伺服板的方法。第二个伺服的输出可以发送到第三个伺服，等等。链条中的最后一个服务器负责向客户发送响应。

### 131. 如何找出哪个客户端机器正在向的服务器提出请求？

Servlet 请求类具有查找客户端机的 IP 地址或主机名称的功能。获取客户端机的 IP 地址，获取客户端机的主机名。请参阅[此处](http://examples.javacodegeeks.com/enterprise-java/servlet/get-client-s-address-and-hostname-in-servlet/)示例。

### 132. HTTP 响应的结构是什么？

HTTP 响应由三个部分组成：

- 状态代码：描述响应的状态。它可用于检查请求是否已成功完成。如果请求失败，可以使用状态代码来找出失败背后的原因。如果的服务不返回状态代码，则默认退回成功状态代码（HttpServletResponse.SC_OK）。
- HTTP 头：它们包含有关响应的更多信息。例如，头条可以指定响应被视为过时的日期/时间，或用于安全地将实体传输给用户的编码形式。看看[如何检索在Servlet的头在这里](http://examples.javacodegeeks.com/enterprise-java/servlet/get-all-request-headers-in-servlet/)。
- 身体：它包含响应的内容。身体可能包含 HTML 代码、图像等。机构由在头后立即在 HTTP 交易消息中传输的数据字节组成。

### 133. 什么是饼干？

[Cookie](http://examples.javacodegeeks.com/core-java/net/urlconnection/get-cookies-from-http-connection/)是 Web 服务器发送到浏览器的一些信息。浏览器将每个 Web 服务器的 Cookie 存储在本地文件中。在以后的请求中，浏览器以及该请求会为该特定 Web 服务器发送所有存储的 cookie。

### 134. 会话和饼干有什么区别？

会话和 Cookie 之间的区别如下：

- 无论客户端浏览器上的设置如何，会话都应工作。客户可能选择禁用 Cookie。但是，会话仍然有效，因为客户端无法在服务器端禁用它们。
- 会话和 Cookie 在可以存储的信息量上也有所不同。HTTP 会话能够存储任何 Java 对象，而 Cookie 只能存储字符串对象。

### 135. 浏览器和服务器将使用哪种协议进行通信？

浏览器使用 HTTP 协议与服务器进行通信。

### 136. 什么是 HTTP 隧道？

HTTP 隧道技术是一种使用各种网络协议执行的通信使用 HTTP 或 HTTPS 协议进行封装的技术。因此，HTTP 协议充当隧道中网络协议用于通信的通道的包装。将其他协议请求作为 HTTP 请求的掩蔽是 HTTP 隧道。

### 137. 发送直接和转发方法有何区别？

发送向法创建新请求，而转发方法只是将请求转发到新目标。重定向后无法提供以前的请求范围对象，因为它会导致新的请求。另一方面，在转发后可提供以前的请求范围对象。从一般情况上讲，发送向导方法被认为比转发方法慢。

| **发送向导**                                                 | **向前**                             |
| ------------------------------------------------------------ | ------------------------------------ |
| 此方法始终发送新请求。这是因为它使用浏览器的 URL 条进行重定向。 | 此方法通过转发将请求发送到其他资源。 |
| 此方法在客户端使用。                                         | 此方法在服务器端使用。               |
| 此方法在 Web 服务器内外使用。                                | 此方法仅在 Web 服务器内部使用。      |

### 138. 什么是网址编码和网址解码？

URL 编码程序负责将 URL 的所有空间和所有其他特殊字符替换到相应的十六进制表示中。在通信中，URL 解码是完全相反的程序。

### 139. 什么是请求调度员？

[Servlet 请求调度器](https://examples.javacodegeeks.com/enterprise-java/servlet/java-servlet-requestdispatcher-tutorial/)是一个界面，其实现定义对象可以将请求发送到服务器上的任何资源（如 HTML、图像、JSP、Servlet 等）。此界面的另一个优点是，它用于两种情况：

- 将一个 Servlet 的响应包含到另一个服务中（即客户端获得两个 Servlet 的响应）
- 将客户请求转发给另一个 Servlet 以履行请求（即客户致电 Servlet，但另一个 Servlet 会给出对客户的响应）

## L.JSP

### 140. 什么是 Jsp 页面？

Java 服务器页面[（JSP）](https://www.javacodegeeks.com/2015/06/jsp-tutorial.html)是包含两种文本类型的文本文档：静态数据和 JSP 元素。静态数据可以以任何基于文本的格式表示，如 HTML 或 XML。JSP 是一种将静态内容与动态生成内容混合的技术。在此处查看[JSP 示例](http://examples.javacodegeeks.com/enterprise-java/jsp/sample-jsp-java-server-page/)。

### 141. JSP 请求如何处理？

在 JSP 请求到达时，浏览器首先请求具有.jsp扩展的页面。然后，Web 服务器读取请求并使用 JSP 编译器，Web 服务器将 JSP 页面转换为服务类。请注意，JSP 文件仅在页面的第一个请求上进行编译，或者如果 JSP 文件已更改。调用生成的服务类，以处理浏览器的请求。请求执行结束后，服务器将回复回客户端。查看[如何在 JSP 中获取请求参数](http://examples.javacodegeeks.com/enterprise-java/jsp/get-request-parameter-in-jsp-page/)。

### 142. JSP的优势是什么？

使用 JSP 技术的优势如下：

- JSP 页面可动态编译为服务，因此，开发人员可以轻松地对演示代码进行更新。
- JSP 页面可以预编。
- JSP 页面可以轻松地组合到静态模板，包括 HTML 或 XML 片段，并带有生成动态内容的代码。
- 开发人员可以提供自定义的 JSP 标签库，这些库使用类似 XML 的语法来访问页面作者。
- 开发人员可以在组件级别进行逻辑更改，而无需编辑使用应用程序逻辑的单个页面。

### 143. 什么是指令？

指令是 JSP 引擎处理的指令，当页面被编译到伺服器时。指令用于设置页面级别指令、插入外部文件的数据以及指定自定义标签库。

### 144. JSP 中提供的不同类型的指令是什么？

指令在 > 的 <% 和% 之间定义。不同类型的指令如下所示：

- 包括指令：它用于包含文件并将文件内容与当前页面合并。
- 页面指令：用于定义 JSP 页面中的特定属性，如错误页面和缓冲器。
- 塔格利布：它用于声明页面中使用的自定义标签库。

### 145. 什么是 JSP 操作？

JSP 操作使用 XML 语法中的构造来控制伺服发动机的行为。当请求 JSP 页面时，它们会被执行。它们可以动态插入到文件中，重复使用 JavaBeans 组件，将用户转发到另一页，或者为 Java 插件生成 HTML。以下列出了一些可用操作：

- jsp：包括一个文件，当JSP页面被请求。
- jsp： 使用豆发现或刻录JavaBean。
- jsp： 设置财产设置JavaBean的属性。
- jsp： 获得财产得到JavaBean的财产。
- jsp：转发请求者到新的页面。
- jsp：插件生成浏览器特定代码。

### 146. 什么是脚本？

在 Java 服务器页面 （JSP） 技术中，脚本是嵌入在 JSP 页面中的Java代码。脚本是标签内的一切。在这些标签之间，用户可以添加任何有效的脚本。

### 147. 什么是声明？

声明类似于Java的可变声明。声明用于声明变量，以便随后用于表达式或脚本。要添加声明，必须使用序列来附上声明。

下面添加示例代码以显示 JSP 声明。

*声明*

```
<%! int j = 0; %> 
<%! int d, e, f; %> 
<%! Shape a = new Shape(); %> 
```

### 148. 什么是表达？

JSP 表达式用于将脚本语言表达式（转换为字符串）的值插入 Web 服务器返回到客户端的数据流中。表达式的定义在<% = 和 %> 标签之间。



*JSP 快递*

```
<html> 
   <head><title>My Blog</title></head> 
    
   <body>
      <p>Today's Date is: <%= (new java.util.Date()).toLocaleString()%></p>
   </body> 
</html>
```

### 149. 隐性对象是什么意思？它们是什么？

JSP 隐性对象是 JSP 容器提供给每个页面中的开发人员的 Java 对象。开发人员可以直接拨打电话，但无需明确声明。JSP 隐性对象也称为预定义变量。以下对象在 JSP 页面中被视为隐含：

- application
- page
- request
- response
- session
- exception
- out
- config
- pageContext

禁用会话的 JSP 示例标签如下所示：

*禁用会话*

```
<%@ page session=“false” %> 
```

### 150. JSTL 中提供的标签有何不同？

有 5 种类型的 JSTL 标签：

**Core：**

- 可变支持
- 流控制
- 网址管理
- 杂项

**XML：**

- 核心
- 流控制
- 转型

**国际化：**

- 现场
- 消息格式化
- 编号和日期格式

**数据库：**

- SQL

**功能：**

- 收集长度
- 字符串操作