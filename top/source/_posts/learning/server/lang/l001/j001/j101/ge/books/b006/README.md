#   深入理解Java 7：核心技术与最佳实践

>   第 12 章 Java 泛型

在程序中通常只对固定类型的对象进行操作，有些代码可以对多种不同类型的对象进行操作。实际使用的类型在代码中只是以参数形式出现的占位符，在具体实例化时，用实际类型替代其中的占位符，这种方式被称为泛型编程。

泛型适用于对抽象类型进行处理，可以有效地减少代码重复，通过一份代码即可对不同类型的对象进行操作，典型的例子是处理集合相关的数据结构。对于这些数据结构可以进行一些抽象的操作，如排序和反转等，这些操作只与数据结构的特征相关，与其中包含的对象的类型无关。在实现这些操作时，对象的类型用占位符表示即可，并不影响操作的实现逻辑，使用者可以根据需要指定实际的类型。

Java 语言在 J2SE 5.0 引入了泛型特性。泛型的主要动机是为了实现类型安全的集合类。除此之外，泛型还可以用来创建处理抽象类型的新类型。


##  目录
-   [泛型基本概念](10x.md)
-   [类型擦除](11x.md)
-   [上界和下界](12x.md)
-   [通配符](13x.md)
-   [泛型与数组](14x.md)
-   [类型系统](15x.md)
-   [覆写与重载](16x.md)
    -   覆写对方法类型签名的要求
    -   覆写对返回值类型的要求
    -   覆写对异常声明的要求
    -   重载
-   [类型推断和操作符](17x.md)
-   [泛型与反射API](18x.md)
-   [使用案例](19x.md)
-   [小结](20x.md)


----