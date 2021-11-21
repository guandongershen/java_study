## 创建Java项目

1. IDEA新建---project---Java

   项目名和文件夹名相同

2. SRC目录下为java源代码，out目录默认为Java编译输出目录，*.java和public类名相同，一个\*.java文件下可以有多个class，但只有一个public类型class

## 变量类型

### 返回一个对象地址

传入一个对象实例

```java
Log log = LogFactory.getLog(Commons.class);
```

上述写法不是创建一个对象，是对Log 类型的引用变量进行赋值，值的类型是对象地址，等号右边是调用的函数，函数有返回类型。log就相当于右边函数创造的对象。

## 局部变量

1. 局部变量，方法内的变量；
2. 局部变量不可以和方法形参同名，会报错
3. 局部变量和成员变量同名时，Java采取就近原则，局部变量近就使用局部变量

## 构造方法

1. 构造方法用来初始化实例，方法名与类名相同

2. 构造方法参数无限制，**构造方法没有返回值**（也没有void）

   ```java
   class Person{
       //创建构造方法
       public Person(){
           ...
       }
   }
   ```

3. 可以定义多个构造方法，通过new操作符调用时，编译器通过构造方法的参数数量、位置和类型自动区分

   ```java
   class Person {
       private String name;
       private int age;
   
       public Person(String name, int age) {
           this.name = name;
           this.age = age;
       }
   
       public Person(String name) {
           this.name = name;
           this.age = 12;
       }
   
       public Person() {
       }
   }
   ```

4. 一个构造方法可以调用其他构造方法，便于代码复用，语法是this(...):

   ```java
   class Person {
       private String name;
       private int age;
   
       public Person(String name, int age) {
           this.name = name;
           this.age = age;
       }
   
       public Person(String name) {
           this(name, 18); // 调用另一个构造方法Person(String, int)
       }
   
       public Person() {
           this("Unnamed"); // 调用另一个构造方法Person(String)
       }
   }
   ```

## 方法重载

1. 方法重载是指多个方法的方法名相同，但各自的参数不同；
2. 重载方法应该完成类似的功能，参考`String`的`indexOf()`；
3. 重载方法返回值类型应该相同。

## 继承

1. 继承关键字extends

2. 构造函数
   - 子类不继承父类构造函数，只是调用。
   - 如果父类构造函数有参数，则必须在子类构造器中显式通过super关键字调用父类的构造器，并且必须包含适当的参数列表（参数可多不可少）
   - 如果父类构造函数无参数，则在子类构造函数中不需要使用super调用，系统自动调用父类无参构造函数
   
3. protected关键字
   - private字段不可被子类访问
   - protected关键字把字段和方法的访问控制权限控制在继承树内部
   
4. 阻止继承

   ```
   java 15 允许使用sealed修饰class，并通过permits明确写出能够从该class继承的子类名称
   ```

5. 向上转型和向下转型（暂不考虑）

## 重写(Override)与重载(Overload)

### 方法签名

方法签名由方法名+形参列表构成；意思是方法名和形参数据类型列表可以唯一的确定一个方法

方法签名不同overload，overload是一个新方法；方法签名相同，返回值相同override

**注意：**方法名相同，方法参数相同，但是方法返回值不同，也是不同的方法。

### 方法的重写

- 参数列表与被重写方法的参数列表必须完全相同。
- 返回类型与被重写方法的返回类型可以不相同，**但是必须是父类返回值的派生类**（java5 及更早版本返回类型要一样，java7 及更高版本可以不同）。
- 访问权限不能比父类中被重写的方法的访问权限更低。例如：如果父类的一个方法被声明为 public，那么在子类中重写该方法就不能声明为 protected。
- 父类的成员方法只能被它的子类重写。
- 声明为 final 的方法不能被重写。
- 声明为 static 的方法不能被重写，但是能够被再次声明。

### 方法的重载

重载(overloading) **是在一个类里面，方法名字相同**，而参数不同。返回类型可以相同也可以不同。

每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。

最常用的地方就是**构造器的重载**。

**重载规则**

- 被重载的方法必须改变参数列表(参数个数或类型不一样)；
- 被重载的方法可以改变返回类型；
- 被重载的方法可以改变访问修饰符；
- 被重载的方法可以声明新的或更广的检查异常；
- 方法能够在同一个类中或者在一个子类中被重载。
- 无法以返回值类型作为重载函数的区分标准。

## 多态

- 方法重载是一个类的多态性表现,而方法重写是子类与父类的一种多态性表现。
- 多态存在的三个必要条件
  1. 继承
  2. 重写
  3. 父类引用指向子类对象
- 多态的实现方式
  1. 重写
  2. 借口
  3. 抽象类和抽象方法
- 当使用多态方式调用方法时，首先检查父类中是否有该方法，如果没有，则编译错误；如果有，再去调用子类的同名方法。

## 抽象类

- 抽象类被设计成只能用于被继承，因此父类可以强迫子类必须实现其定义的抽象方法，否则编译报错，抽象方法实际相当于定义了“规范”
- 抽象类和抽象方法使用abstract修饰
- 子类必须声明为抽象类或者子类必须实现父类的抽象方法才可以继承抽象类
- 抽象类中的非抽象方法可以有方法体

### 面向抽象编程

- 当我们定义了抽象类`Person`，以及具体的`Student`、`Teacher`子类的时候，我们可以通过抽象类`Person`类型去引用具体的子类的实例

- 尽量引用高层类型，避免引用实际子类型的方式，称之为面向抽象编程。

- 面向抽象编程本质

  ```
  上层代码只定义规范（例如：abstract class Person）；
  
  不需要子类就可以实现业务逻辑（正常编译）；
  
  具体的业务逻辑由不同的子类实现，调用者并不关心。
  ```

## 接口

- 接口是抽象方法的集合，interface关键字声明，目的是被类实现

  接口内的方法默认pulic abstract

- 一个类可以实现多个接口，使用implements关键字

- 接口可以继承接口

- default方法

  ```
  default 方法目的：需要给接口新增一个方法时，会设计到修改全部子类，如果新增default方法，那么子类只需在需要重写的地方去扩展方法
  default方法需要有方法体
  ```

## 静态字段和静态方法

- 静态字段属于所有实例共享，实际是属于对应class的
- 调用静态方法不需要实例，无法访问this，但可以访问静态字段和其他静态方法
- 静态方法常用语工具类和辅助方法
- 推荐类名.静态字段（或静态方法）访问
- 接口是一个纯抽象类，不能定义实例字段，接口可以有静态字段，且为final类型，interface中的字段只能是public static final类型，可简写。

## 包

- 包的意义：为了防止命名冲突，访问控制，搜索定位
- IDEA右键创造包，包下边创造类，推荐命名方法：域名倒叙命名
- import导入不同包

## 核心类

### 字符串和编码

1. 字符串操作不改变原字符串内容，返回新字符串；

2. 常用字符串操作：比较、提取、查找、大小写转换，Java封装了很多处理字符串的函数。

3. Java使用Unicode编码表示String和char

4. 转换编码就是将string和byte[]转换，需要指定编码。

   ```java
   byte[] b2 = "Hello".getBytes("UTF-8"); // 按UTF-8编码转换
   ```

5. 转换byte[] 时，始终优先考虑UTF-8编码

6. 字符串格式化

   ```java
   System.out.println(String.format("%s","fuck"));
   ```

### StringBuilder

- 循环拼接字符串，会循环创建对象销毁，浪费内存，影响效率
- StringBuilder 可以预分配缓冲区

### StringJoiner

- 分隔符拼接数组

## 日志

### IDEA引入第三方库（jar）

项目结构---模块---依赖---+jar

### JDK logging

java 标准库提供的日志

```java
import java.util.logging.Logger;
```

### Commons Logging

第三方日志库，由Apache创建的日志模块，可**挂接不同的日志系统**，并通过配置文件指定挂接的日志系统，**相当作为日志接口来使用，它不是日志实现**；默认自动搜索Log4j（另一个流行的日志系统），如果没找到，使用JDK Logging

1. 使用Commons Logging时，如果在静态方法中引用Log，通常直接定义一个静态变量

   ```java
   // 在静态方法中引用Log:
   public class Main {
       static final Log log = LogFactory.getLog(Main.class);
   
       static void foo() {
           log.info("foo");
       }
   }
   ```

2. 在实例方法中引用Log，通常定义一个实例变量

   ```java
   // 在实例方法中引用Log:
   public class Person {
       protected final Log log = LogFactory.getLog(getClass());
   
       void foo() {
           log.info("foo");
       }
   }
   ```

3. 传参使用getClass() ，好处是子类可以从父类继承log实例

### Log4j

1. 日志的实现，Log4j是一种流行的日志框架
2. Log4j可自动把一条日志输出到不同目的地
   - console：输出到屏幕
   - file：输出到文件
   - socket：通过网络输出到远程计算机
   - jdbc：输出到数据库
3. 输出日志过程中，通过Filter来过滤哪些log需要被输出，哪些log不需要被输出，通过Layout来格式化日志信息
4. Log4j实际使用是通过配置文件来配置，即 .xml 文件

### LSF4J和Logback

> Commons Logging和Log4j，它们一个负责充当日志API，一个负责实现日志底层

SLF4J 类似 Commons Logging，也是一个日志接口，而Logback类似Log4j，是一个日志实现

### LSF4J日志打印（常用）

打印日志常见代码

```java
//Commons Logging
int score = 99;
p.setScore(score);
log.info("Set score " + score + " for Person " + p.getName() + " ok.");
```



```java
//slf4j
int score = 99;
p.setScore(score);
logger.info("Set score {} for Person {} ok.", score, p.getName());
```

导入的包

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
```

同之处就是Log变成了Logger，LogFactory变成了LoggerFactory。使用SLF4J和Logback和使用Commons Logging加Log4j是类似的。

## 反射

- Java的反射是指程序在运行期可以拿到一个对象的所有信息。

- `class`是由JVM在执行过程中动态加载的。JVM在第一次读取到一种`class`类型时，将其加载进内存。

  每加载一种`class`，JVM就为其创建一个`Class`类型的实例，并关联起来。注意：这里的`Class`类型是一个名叫`Class`的`class`

  ```java
  public final class Class {
      private Class() {}
  }
  ```

- 以`String`类为例，当JVM加载`String`类时，它首先读取`String.class`文件到内存，然后，为`String`类创建一个`Class`实例并关联起来

- Class实例是由JVM内部创建的，Class类的构造方法是private，因此只能由JVM创建

- JVM为每个加载的`class`创建了对应的`Class`实例，并在实例中保存了该`class`的所有信息，包括类名、包名、父类、实现的接口、所有方法、字段等，因此，如果获取了某个`Class`实例，我们就可以通过这个`Class`实例获取到该实例对应的`class`的所有信息（Class实例封装了许多方法来完成获取）

- **通过`Class`实例获取`class`信息的方法称为反射（Reflection）**

## 注解

java程序的一种特殊注释——注解

1. 注解是放在java源码的类、方法、字段、参数前的一种特殊注释
2. 注解的作用
   - 第一类是由编译器使用的注解
     - `@Override`：让编译器检查该方法是否正确地实现了覆写；
     - `@SuppressWarnings`：告诉编译器忽略此处代码产生的警告。
     - 这类注解不会被编译进.class文件，编译后被扔掉
   - 第二类是由工具处理.class 文件使用的注解，比如有些工具会在加载class的时候，对class做动态修改，实现一些特殊的功能。这类注解会被编译进入`.class`文件，但加载结束后并不会存在于内存中。这类注解只被一些底层库使用，一般我们不必自己处理。
   - 第**三类是程序运行期间能够读取的注解，它们在加载后一直存在JVM中，这是最常用的注解**，例如，一个配置了`@PostConstruct`的方法会在调用构造方法后自动被调用（这是Java代码读取该注解实现的功能，JVM并不会识别该注解）。

### 注解的定义

Java语言使用`@interface`语法来定义注解（`Annotation`），它的格式如下：

```java
public @interface Report {
    int type() default 0;
    String level() default "info";
    String value() default "";
}
```

注解的参数类似无参数方法，可以用`default`设定一个默认值（强烈推荐）。最常用的参数应当命名为`value`。

**元注解**

有一些注解可以修饰其他注解，这些注解就称为元注解（meta annotation）。

**常用元注解**

- @Target，最常用的元注解是`@Target`。使用`@Target`可以定义`Annotation`能够被应用于源码的哪些位置
- @Retention，元注解`@Retention`定义了`Annotation`的生命周期
- @Inherited，使用`@Inherited`定义子类是否可继承父类定义的`Annotation`

**注解定义**

1. 使用@interface定义注解
2. 添加参数、默认值
3. 用元注解配置注释

### 注解处理

ava的注解本身对代码逻辑没有任何影响。根据`@Retention`的配置。

### 注解使用

注解如何使用，完全由程序自己决定。例如，JUnit是一个测试框架，它会自动运行所有标记为`@Test`的方法。

## 泛型

针对数据类型做检查，代码模板，实现编写一次万能匹配，通过编译器保证了类型安全。

编写举例：

例如String，来编写类

```java
public class Pair {
    private String first;
    private String last;
    public Pair(String first, String last) {
        this.first = first;
        this.last = last;
    }
    public String getFirst() {
        return first;
    }
    public String getLast() {
        return last;
    }
}
```

然后标记所有特定类型，即String；

最后，把特定类型String替换为T，并声明<T>

```java 
public class Pair<T> {
    private T first;
    private T last;
    public Pair(T first, T last) {
        this.first = first;
        this.last = last;
    }
    public T getFirst() {
        return first;
    }
    public T getLast() {
        return last;
    }
}
```

**应用**

实现编写一次模板，可以创建任意类型的ArrayList

```java
public class ArrayList<T> {
    private T[] array;
    private int size;
    public void add(T e) {...}
    public void remove(int index) {...}
    public T get(int index) {...}
}
```

```java
// 创建可以存储String的ArrayList:
ArrayList<String> strList = new ArrayList<String>();
// 创建可以存储Float的ArrayList:
ArrayList<Float> floatList = new ArrayList<Float>();
// 创建可以存储Person的ArrayList:
ArrayList<Person> personList = new ArrayList<Person>();
```

**注意**

- 泛型的好处是使用时不必对类型进行强制转换，它通过编译器对类型进行检查；

- 注意泛型的继承关系：可以把`ArrayList<Integer>`向上转型为`List<Integer>`（`T`不能变！），但不能把`ArrayList<Integer>`向上转型为`ArrayList<Number>`（`T`不能变成父类）。

## 异常

异常如果出现，程序就会自动中断，后续语句都不再执行，捕获异常是为了处理异常并且继续执行后续的程序。
