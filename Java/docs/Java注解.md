* [Java注解]()
    * [一、Java注解概述](#%E4%B8%80java%E6%B3%A8%E8%A7%A3%E6%A6%82%E8%BF%B0)
    * [二、注解的作用分类](#%E4%BA%8C%E6%B3%A8%E8%A7%A3%E7%9A%84%E4%BD%9C%E7%94%A8%E5%88%86%E7%B1%BB)
    * [三、jdk的内置注解](#%E4%B8%89jdk%E7%9A%84%E5%86%85%E7%BD%AE%E6%B3%A8%E8%A7%A3)
      * [3.1 内置注解分类](#31-%E5%86%85%E7%BD%AE%E6%B3%A8%E8%A7%A3%E5%88%86%E7%B1%BB)
      * [3.2  @Override注解](#32-override%E6%B3%A8%E8%A7%A3)
      * [3.3 @Deprecated注解](#33-deprecated%E6%B3%A8%E8%A7%A3)
      * [3.4 @SuppressWarnings注解](#34-suppresswarnings%E6%B3%A8%E8%A7%A3)
      * [3.5 @Repeatable注解](#35-repeatable%E6%B3%A8%E8%A7%A3)
    
    
# Java注解

### 一、Java注解概述

> 注解（Annotation），也叫元数据。一种代码级别的说明。它是JDK1.5及以后版本引入的一个特性，与类、接口、枚举是在同一个层次。它可以声明在包、类、字段、方法、局部变量、方法参数等的前面，用来对这些元素进行说明，注释。

### 二、注解的作用分类

> -  **编写文档：** 通过代码里标识的元数据生成文档【生成文档doc文档】
> -  **代码分析：** 通过代码里标识的元数据对代码进行分析【使用反射】
> -  **编译检查：** 通过代码里标识的元数据让编译器能够实现基本的编译检查【Override等】

***编写文档***
> 首先，我们要知道Java中是有三种注释的，分别为单行注释、多行注释和文档注释。而文档注释中，也有@开头的元注解，这就是基于文档注释的注解。有了文档注释，我们就可以使用javadoc命令来生成doc文档，此时文档内的元注解也会生成对应的文档内容。这就是编写文档的作用。

***代码分析***
> 我们频繁使用之一，也是包括使用反射来通过代码里标识的元数据对代码进行分析的，此内容我们在后续展开讲解。

***编译检查***
>至于在编译期间在代码中标识的注解，可以用来做特定的编译检查，它可以在编译期间就检查出“你是否按规定办事”，如果不按照注解规定办事的话，就会在编译期间飘红报错，并予以提示信息。可以就可以为我们代码提供了一种规范制约，避免我们后续在代码中处理太多的代码以及功能的规范。比如，@Override注解是在我们覆盖父类（父接口）方法时出现的，这证明我们覆盖方法是继承于父类（父接口）的方法，如果该方法稍加改变就会报错；@FunctionInterface注解是在编译期检查是否是函数式接口的，如果不遵循它的规范，同样也会报错。

### 三、jdk的内置注解

#### 3.1 内置注解分类
> * **@Override：** 标记在成员方法上，用于标识当前方法是重写父类（父接口）方法，编译器在对该方法进行编译时会检查是否符合重写规则，如果不符合，编译报错。
> * **@Deprecated：** 用于标记当前类、成员变量、成员方法或者构造方法过时如果开发者调用了被标记为过时的方法，编译器在编译期进行警告。
> * **@SuppressWarnings：** 压制警告注解，可放置在类和方法上，该注解的作用是阻止编译器发出某些警告信息。

#### 3.2 @Override注解
> 标记在成员方法上，用于标识当前方法是重写父类（父接口）方法，编译器在对该方法进行编译时会检查是否符合重写规则，如果不符合，编译报错。

这里解释一下@Override注解，在我们的Object基类中有一个方法是toString方法，我们通常在实体类中去重写此方法来达到打印对象信息的效果，这时候也会发现重写的toString方法上方就有一个@Override注解。如下所示：

![image-20200604203535421](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200604203537.png)

于是，我们试图去改变重写后的toString方法名称，将方法名改为toStrings。你会发现在编译期就报错了！如下所示：

![image-20200604203645332](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200604203647.png)

那么这说明什么呢？这就说明该方法不是我们重写其父类（Object）的方法。这就是@Override注解的作用。


#### 3.3 @Deprecated注解

> 用于标记当前类、成员变量、成员方法或者构造方法过时如果开发者调用了被标记为过时的方法，编译器在编译期进行警告。

我们解释@Deprecated注解就需要模拟一种场景了。假设我们公司的产品，目前是V1.0版本，它为用户提供了show1方法的功能。这时候我们为产品的show1方法的功能又进行了扩展，打算发布V2.0版本。但是，我们V1.0版本的产品需要抛弃吗？也就是说我们V1.0的产品功能还继续让用户使用吗？答案肯定是不能抛弃的，因为有一部分用户是一直用V1.0版本的。如果抛弃了该版本会损失很多的用户量，所以我们不能抛弃该版本。这时候，我们对功能进行了扩展后，发布了V2.0版本，我们给予用户的通知就可以了，也就是告知用户我们在V2.0版本中为功能进行了扩展。可以让用户自行选择版本。

但是，除了发布告知用户版本情况之外，我们还需要在原来版本的功能上给予提示，在上面的模拟场景中我们需要在show1方法上方加@Deprecated注解给予提示。通过这种方式也告知用户“这是旧版本时候的功能了，我们不建议再继续使用旧版本的功能”，这句话的意思也就正是给用户做了提示。用户也会这么想“奥，这版本的这个功能不好用了，肯定有新版本，又更好用的功能。我要去官网查一下下载新版本”，还会有用户这么想“我明白了，又更新出更好的功能了，但是这个版本的功能我已经够用了，不需要重新下载新版本了”。

![image-20200604205459205](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200604205500.png)

那么我们怎么查看我上述所说的在功能上给予的提示呢？这时候我需要去创建一个方法，然后去调用show1方法，并查看调用时它是如何提示的。

![image-20200604205659588](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200604205702.png)

图已经贴出来了，你是否发现的新旧版本功能的异同点呢？很明显，在方法中的提示是在调用的方法名上加了一道横线把该方法划掉了。这就体现了show1方法过时了，已经不建议使用了，我们为你提供了更好的。

回想起来，在我们的api中也会有方法是过时的，比如我们的Date日期类中的方法有很多都已经过时了。如下图：

![image-20200604210154348](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200604210157.png)

![image-20200604210416762](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200604210419.png)

如你所见，是不是有很多方法都过时了呢？那它的方法上是加了@Deprecated注解吗？来跟着我的脚步，我带你们看一下。

![image-20200604210515910](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200604210517.png)

我们已经知道的Date类中的这些方法已经是过时的了，如果我们使用该方法并执行该程序的话。执行的过程中就会提示该方法已过时的内容，但是只是提示，并不影响你使用该方法。如下：

![image-20200604221938895](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200604221941.png)

OK！这也就是@Deprecated注解的作用了。



#### 3.4 @SuppressWarnings注解

> 压制警告注解，可放置在类和方法上，该注解的作用是阻止编译器发出某些警告信息，该注解为单值注解，只有 一个value参数，该参数为字符串数组类型，参数值常用的有如下几个。
>
> - unchecked：未检查的转化，如集合没有指定类型还添加元素
> - unused：未使用的变量
> - resource：有泛型未指定类型
> - path：在类路径，原文件路径中有不存在的路径
> - deprecation：使用了某些不赞成使用的类和方法
> - fallthrough：switch语句执行到底没有break关键字
> -  rawtypes：没有写泛型，比如: List list = new ArrayList();
> - all：全部类型的警告

压制警告注解，顾名思义就是压制警告的出现。我们都知道，在Java代码的编写过程中，是有很多黄色警告出现的。但是我不知道你的导师是否教过你，程序员只需要处理红色的error，不需要理会黄色的warning。如果你的导师说过此问题，那是有原因的。因为在你学习阶段，我们认清处理红色的error即可，这样可以减轻你学习阶段在脑部的记忆内容。如果你刚刚加入学习Java的队列中，需要大脑记忆的东西就有太多了，也就是我们目前不需要额外记忆其他的东西，只记忆重点即可。至于黄色warning嘛，在你的学习过程中慢慢就会有所了解的，而不是死记硬背的。

那为了解释@SuppressWarnings注解，我们还使用上一个例子，因为在那个例子中就有黄色的warning出现。

![image-20200604213625474](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200604213627.png)

而每一个黄色的warning都会有警告信息的。比如，这一个图中的警告信息，就告知你show2()方法没有被使用，简单来说，你创建的show2方法，但是你在代码中并没有调用过此方法。以后你便会遇到各种各样黄色的warning。然后， 我们就可以使用不同的注解参数来压制不同的注解。但是在该注解的参数中，提供了一个all参数可以压制全部类型的警告。而这个注解是需要加到类的上方，并赋予all参数，即可压制所有警告。如下：

![image-20200604213943722](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200604213945.png)

我们加入注解并赋予all参数后，你会发现use方法和show2方法的警告没有了，实际上导Date包的警告还在，因为我们Date包导入到了该类中，但是我们并没有创建Date对象，也就是并没有写入Date在代码中，你也会发现那一行是灰色的，也就证明了我们没有去使用导入这个包的任何信息的说法，出现这种情况我们就需要把这个没有用的导包内容删除掉，使用`Ctrl + X`删除导入没有用到的包即可。还有一种办法就是在包的上方修饰压制警告注解，但是我认为在一个没有用的包上加压制注解是毫无意义的，所以，我们直接删除就好。

然后，我们还见到上图，注解那一行出现了警告信息提示。这一行的意思是冗余的警告压制。这就是说我们压制以下的警告并没有什么意义而造成的冗余，但是如果我们使用了该类并做了点什么的话，压制注解的冗余警告就会消失，毕竟我们使用了该类，此时就不会早场冗余了。

上述解释@SuppressWarnings注解也差不多就这些了。OK，继续向下看吧。持续为大家讲解。



#### 3.5 @Repeatable注解

> **@Repeatable** 表明标记的注解可以多次应用于相同的声明或类型，此注解由Java8版本引入。我们知道注解是不能重复定义的，其实该注解就是一个语法糖，它可以重复多此使用，更适用于我们的特殊场景。

首先，我们先创建一个可以重复使用的注解。

```java
package com.mylifes1110.anno;

import java.lang.annotation.Repeatable;

@Repeatable(Hour.class)
public @interface Hours {
    double[] hours() default 0;
}
```

你会发现注解要求传入的值是一个类对象，此类对象就需要传入另外一个注解，这里也就是另外一个注解容器的类对象。我们去创建一下。

```java
package com.mylifes1110.anno;

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

//容器
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
public @interface Hour {
    Hours[] value();
}
```

其实，这两个注解的套用，就是将一个普通的注解封装了一个可重复使用的注解，来达到注解的复用性。最后，我们创建一下测试类，随后带你去看一下源码。

```java
package com.mylifes1110.java;

import com.mylifes1110.anno.Hours;

@Hours(hours = 5)
@Hours(hours = 6)
@Hours(hours = 2)
public class Worker {
    public static void main(String[] args) {
        //通过Hours注解类型来获取Worker中的值数组对象
        Hours[] hours = Worker.class.getAnnotationsByType(Hours.class);
        //遍历数组
        for (Hours h : hours) {
            System.out.println(h);
        }
    }
}
```

测试类，是一个工人测试类，该工人使用注解记录早中晚的工作时间。测试结果如下：

![image-20200606183652359](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200606184056.png)

然后我们进入到源码一探究竟。

![image-20200606183737877](https://gitee.com/Ziphtracks/Figurebed/raw/master/img/1/20200606184053.png)

我们发现进入到源码后，就只看见一个返回值为类对象的抽象方法。这也就验证了该注解只是一个可实现重复性注解的语法糖而已。
