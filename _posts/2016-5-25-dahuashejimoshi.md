---
title: 大话设计模式学习笔记 
tags: Java,设计模式,编程
grammar_cjkRuby: true
grammar_codeLinenums: true
---


欢迎使用 **{小书匠}(xiaoshujiang)编辑器**，您可以通过==设置==里的修改模板来改变新建文章的内容。

[TOC]

# 六大原则

## 一、单一职责原则
### 1、定义
单一职责原则
: (SRP)，就一个类而言，应用仅有一个引起它变化的原因。
### 2、使用
- 如果一个类承担的职责过多，就等于把这些职责耦合在一起，一个职责的变化可能会削弱或者抑制这个类完成其他职责的能力，这种耦合会导致脆弱的设计，当变化时，设计会遭受到意想不到的破坏。
- 软件设计真正要做的许多内容，就是发现职责并把那些职责相互分离，如果你能想到多于一个动机去改变一个类，那么这个类就具有多于一个的职责。

## 二、开放-封闭原则
### 1、定义
开闭原则
: 软件实体（类、模块、函数等）应该可以扩展，但是不可修改
- 对于扩展是开放的（Open for extension）
- 对于更改是封闭的（Closed for modification） 

### 2、使用
- 怎样的设计才能面对需求的改变却可以保持相对稳定，从而使得系统可以在第一个版本以后不断推出新的版本呢？开闭能给出答案。
- 无论模块是多么的“封闭”，都会存在一些无法对之封闭的变化。既然不可能完全封闭，设计人员必须对于他设计的模块应该对哪些变化封闭做出先把。他必须猜测出最有可能发生的变化种类，然后构造抽象来隔离那些变化。
- 在我们最初编写代码时，假设变化不会发生，当变化发生时，我们就创建抽象来隔离以后发生的同类变化。也就是等到变化发生时立即采取行动。
- 我们希望的是在开发工作展开不久就知道可能发生变化。查明可能发生变化所等待的时间越长，要创建正确的抽象就越困难。
- **开闭原则是面向对象设计的核心所在**。遵循这个原则可以带来面向对象技术所声称的巨大好处，也就是`可维护`、`可扩展`、`可复用`、`灵活性好`。开发人员应该仅对程序中呈`现出频繁变化的那些部分做出抽象`，然而，对于应用程序中的每个部分都刻意地进行抽象同样不是一个好主意。拒绝不成熟的抽象和抽象本身一样重要。

## 三、依赖倒转原则
### 1、定义
依赖倒置原则
: 抽象不应用依赖细节，细节应该依赖于抽象，说简单点就是`针对接口编程，不要对实现编程`。
- 高层模块不应该依赖低层模块。两个都应该依赖抽象。
- 抽象不应该依赖细节。
- 细节应该依赖抽象。

在Java语言中表现就是：
- 模块间的依赖通过抽象发生，实现类之间不发生直接依赖关系，其依赖关系是通过接口或抽象类产生的。
- 接口或抽象类不依赖于实现类
- 实现类依赖接口或者抽象类。

> 注意：在Java中，只要定义变量就必然要有类型，一个变量可以有两种类型：`表面类型`和`实际类型`，表面类型是在**定义的时候赋予的类型**，实际类型是**对象的类型**。

### 2、依赖的三种写法
1. 构造函数传递依赖对象
    在类中通过构造函数声明依赖对象，按照依赖注入的说法，这种方式叫做构造函数注入
2. setter方法传递依赖对象
    在抽象设置setter方法声明依赖关系，依照依赖注入的说法，这是setter依赖注入
3. 接口声明依赖对象
    在接口的方法中声明依赖对象，这是接口注入。

### 3、使用规则
- 每个类尽量都有接口或抽象类，或者抽象类和接口两者都具备。这是依赖倒置的基本要求，接口和抽象类都属于抽象的，有了抽象才可能依赖倒置
- 变量的表面类型尽量是接口或者是抽象类
- 任何类都不应该从具体类派生
- 尽量不要覆写基类的方法
- 结合里氏替换原则使用
    - 接口负责定义public属性和方法，并且声明与其他对象的依赖关系，抽象类负责公共构造部分的实现，实现类准确的实现业务逻辑，同时在适当的时候对父类进行细化。

==依赖倒置其实可以说是面向对象设计的标志，用哪种语言来编写程序不重要，如果编写时考虑的都是如何针对抽象编程而不是针对细节编程，即程序中依赖关系都是终止于抽象类或者接口，那就是面向对象的设计，反之那就是过程化的设计了。==

## 四、里氏替换原则
### 1、定义
里氏替换原则
: 一个软件实体如果使用的是一个父类的话，那么一定适用于其子类，而且它察觉不出父类对象和子类对象的区别。也就是说，在软件里面，把父类都替换成它的子类，程序的行为没有变化。`子类型必须能够替换掉它他们的父类型。`

- 只有当子类可以替换掉父类，软件单位的功能不受到影响时，父类才能真正被复用，而子类也能够在父类的基础上增加新的行为。


### 2、含义
1. 子类必须完全实现父类的方法
    > 注意：在类中调用其他类时务必要使用父类或接口，如果不能使用父类或接口，则说明类的设计已经违背了LSP（里氏替换原则）。如果子类不能完整地实现父类的方法，或者父类的某些方法在子类中已经发生“畸变”，则建议断开父子继承关系，采用依赖、聚合、组合等关系代替继承
2. 子类可以有自己的个性
    ==子类可以出现的地方，父类未必能出现==
3. 覆盖或实现父类的方法时输入参数可以被放大
    ==子类中方法的前置条件必须与超类中被覆写的方法的前置条件相同或者更宽松。==
4. 覆写或实现父类的方法时输出结果可以被缩小
    

## 五、迪米特法则
### 1、定义
迪米特法则
: 如果两个类不必彼此直接通信，那么这两个类就不应当发生直接的相互作用。如果其中一个类需要调用另一个类的某一个方法的话，可以通过第三者转发这个调用。


# 23种设计模式

## 一、简单工厂模式

### 1、面向对象的好处
- 通过封装、继承、多态把程序的耦合度降低
- 使用设计模式使得程序更加灵活，容易修改，并且易于利用

### 2、UML类图
- 类
    - 类用矩形框表示，类图分三层，第一层显示`类的名称`，如果是抽象类，就用`斜体`显示。第二层是`类的特性`，通常就是字段和属性。第三层是`类的操作`，通过是方法或行为。
    > 注意：前面的符号，`“+”`表示`public`,`"-"`表示`private`，`"#"`表示`protected`。
- 接口
    - 与类图的区别主要是顶端有`<<interface>>`显示，第一行是`接口名称`，第二行是`接口方法`。接口还有另一种表示方法，俗称棒棒糖表示法。
- 继承
    - 继承关系用`空心三角形+实线表示`
- 关联
    - 当一个类`‘知道’`另一个类时，可以用关联（association）。关联关系用`实线箭头`表示。成员变量与类就是关联关系。
- 聚合
    - 聚合（Aggregation）关系表示一种弱的“拥有”关系，体现的是A对象可以包含B对象，但B对象不是A对象的一部分。如大雁和雁群两个类，大雁是群居动物，每只大雁都是属于一个雁群，一个雁群可以有多只大雁。聚合关系用`空心菱形+实线箭头`来表示。
- 合成
    - 合成（Composition，也有翻译成“组合”）关系是一种强的“拥有”关系，体现了严格的部分和整体的关系，部分和整体的生命周期一样。例如鸟和其翅膀就是合成（组合）关系，因为它们是部分与整体的关系，并且翅膀和鸟的生命周期是相同的。合成关系用`实心菱形+实线箭头`表示。
- 依赖
    - 依赖（Dependency）关系表示一事物依赖于其他事物，如果动物的几大特征，比如有新陈代谢，能繁殖。而动物要有生命力，需要氧气，水以及食物等，也就是说，动物依赖于氧气和水。他们之间是依赖关系，用`虚线箭头`表示。

==编程是一门技术，更是一门艺术==

## 二、策略模式
### 1、定义
策略模式
: 策略模式是一种定义一系列算法的方法，从概念上来看，所有这些算法完成的都是相同的工作，只是实现不同，它可以以相同的方式调用所有的算法，减少了各种算法类与使用算法类之间的耦合。

### 2、优点
- 策略模式的Strategy类层次为Context定义了一系列可供重用的算法和行为。继承有助于提取出这些算法中的公共功能。
- 策略模式简化了单元测试，因为每个算法都有自己的类，可以通过息的接口单独测试。

### 3、使用
- 当不同的行为堆砌在一个类中时，就很难避免使用条件语句来选择合适的行为。将这些行为封装在一个独立的Strategy类中，可以在使用这些行为的类中消除条件语句。
- 策略模式就是用来`封装算法`的，但在实践中，我们发现可以用它来封装几乎任何类型的规则，只要在分析过程中听到需要在`不同时间应用不同的业务规则`，就可以考虑使用策略模式处理这种变化的可能性。
- 在基本的策略模式中，选择所用具体实现的职责由客户端对象承担，并转给策略模式的Context对象。这本身**并没有**解除客户端选择判断的压力，而策略模式与简单工厂模式结合后，先把具体实现 的职责也可以由Context来承担，这就最大化地减轻了客户端的职责。

### 4、类图
![策略模式](https://www.processon.com/chart_image/57353b47e4b0d4e097691f53.png)

### 5、示例
- Strategy.java
```
public interface Strategy {
    public void doSomething();
}
```

- Context.java
```
public class Context {
    private Strategy mStrategy = null;

    public Context(Strategy strategy) {
        mStrategy = strategy;
    }

    public void doAnything() {
        mStrategy.doSomething();
    }
}
```

- ConcreteStrategy1.java
```
public class ConcreteStrategy1 implements Strategy {
    @Override
    public void doSomething() {
        System.out.println("具体策略1的运算法则...");
    }
}
```

- ConcreteStrategy2.java
```
public class ConcreteStrategy2 implements Strategy {
    @Override
    public void doSomething() {
        System.out.println("具体策略2的运算法则...");
    }
}
```

- Client.java
```
public class Client {
    public static void main(String[] args) {
        Strategy strategy = new ConcreteStrategy1();
        Context context = new Context(strategy);
        context.doAnything();
    }
}
```

## 三、装饰模式
### 1、定义
装饰模式
: 动态地给一个对象添加一些额外的职责，就增加功能来说，装饰模式比生成子类更为灵活。
装饰模式是为已有功能动态地添加更多功能的一种方式。

### 2、使用

- **使用时机**
起初当系统需要新功能的时候，是向旧的类中添加新的代码，这些新加的代码通常装饰了原有类的核心职责或主要行为。但这种方式的问题在于，它们在主类中加入了新的字段，新的方法和新的逻辑，从而增加了主类的复杂度，而这些新加入的东西仅仅是为了满足一些只在某种特定情况下才会执行的特殊行为的需要。而**装饰模式却提供了一个非常好的解决方案，它把每个要装饰的功能放在单独的类中，并让这个类包装它所要装饰的对象，因此，当需要执行特殊行为时，客户代码就可以在运行时根据需要有选择地，按顺序地使用装饰功能包装对象**

### 3、优点
- 装饰模式把类中的装饰功能从类中搬移去除，这样可以简化原有的类。
- 装饰模式有效地把类的核心职责和装饰功能区分开了。而且可以去除相关类中重复的装饰逻辑。

### 4、类图
![装饰模式](https://www.processon.com/chart_image/57352bfbe4b0a43bbdd95670.png)


  
### 5、示例
- Component.java
```
public abstract class Component {
    public abstract void operate();
}
```

- ConcreteComponent.java
```
public class ConcreteComponent extends Component {
    @Override
    public void operate() {
        System.out.println("do something...");
    }
}
```

- Decorator.java
```
public abstract class Decorator extends Component {
    private Component mComponent = null;

    public Decorator(Component component) {
        mComponent = component;
    }

    @Override
    public void operate() {
        mComponent.operate();
    }

}
```

- ConcreteDecorator1.java
```
public class ConcreteDecorator1 extends  Decorator{
    public ConcreteDecorator1(Component component) {
        super(component);
    }

    @Override
    public void operate() {
        method1();
        super.operate();
    }

    private void method1() {
        System.out.println("method1 decorator...");
    }
}
```
- ConcreteDecorator2.java
```
public class ConcreteDecorator2 extends Decorator {
    public ConcreteDecorator2(Component component) {
        super(component);
    }

    private void method2() {
        System.out.println("method2 decorator...");
    }

    @Override
    public void operate() {
        super.operate();
        method2();
    }
}
```

- Client.java
```
public class Client {
    public static void main(String[] args) {
        Component component = new ConcreteComponent();
        component = new ConcreteDecorator1(component);
        component = new ConcreteDecorator2(component);
        component.operate();
    }
}
```

> 注意： 使用装饰模式的时候，需要注意装饰的顺序。

## 四、代理模式
### 1、定义
代理模式
: 为其他对象提供一种代理以控制对这个对象的访问

### 2、使用
- 远程代理
    就是为一个对象在不同的地址空间

### 3、优点
- 高扩展性
- 智能化

### 4、类图
![代理模式](https://www.processon.com/chart_image/57357724e4b0a43bbddd9c82.png)

### 5、示例
- Subject.java
```
public interface Subject {
    public void request();
}
```
- RealSubject.java
```
public class RealSubject implements Subject {
    @Override
    public void request() {
        System.out.println("do Something...");
    }
}
```

- Proxy.java
```
public class Proxy implements Subject {
    private Subject mSubject = null;

    public Proxy(Subject subject) {
        mSubject = subject;
    }

    @Override
    public void request() {
        before();
        mSubject.request();
        after();
    }

    private void before() {
        System.out.println("Proxy begin to working...");
    }

    private void after() {
        System.out.println("Proxy finish working...");
    }
}
```

- Client.java
```
public class Client {
    public static void main(String[] args) {
        Subject subject = new RealSubject();
        Proxy proxy = new Proxy(subject);
        proxy.request();
    }
}
```

## 五、工厂方法模式
### 1、定义
工厂方法模式
: 定义一个用于创建对象的接口，让子类决定实例化哪一个类。工厂方法使一个类的实例化延迟到其子类。

### 2、使用

### 3、优点
- 良好的封闭性，代码结构清晰
- 扩展性非常优秀
- 屏蔽产品类
- 工厂方法模式是典型的解耦框架

### 4、类图
![工厂方法模式](https://www.processon.com/chart_image/573a7eaae4b06d790957a35e.png)

### 5、示例
- Product.java
```
public abstract class Product {
    public void method1() {

    }
    public abstract void method2();
}
```

- ConcreteProduct1.java
```
public class ConcreteProduct1 extends Product {
    @Override
    public void method2() {

    }
}
```

- ConcreteProduct2.java
```
public class ConcreteProduct2 extends Product {
    @Override
    public void method2() {

    }
}
```

- Creator.java
```
public abstract class Creator {
    public abstract <T extends Product> T createProduct(Class<T> c);
}
```

- ConcreteCreator.java
```
public class ConcreteCreator extends Creator {
    @Override
    public <T extends Product> T createProduct(Class<T> c) {
        Product product = null;
        try {
            product = (Product) Class.forName(c.getName()).newInstance();
        } catch (InstantiationException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        return null;
    }
}
```

- Client.java
```
public class Client {
    public static void main(String[] args) {
        Creator creator = new ConcreteCreator();
        Product product = creator.createProduct(ConcreteProduct1.class);
        product.method1();
        product.method2();
    }
}
```

## 六、原型模式
### 1、定义
原型模式
: 用原型实例指定创建对象的种类，并且通过拷贝这些原型创建新的对象。

### 2、使用
- 资源优化场景
- 性能和安全要求的场景
- 一个对象多个修改者的场景

### 3、优点
- 性能优良
- 逃避构造函数的约束

### 4、类图
![原型模式](https://www.processon.com/chart_image/573c4872e4b0285a372d17af.png)

### 5、示例
- PrototypeClass.java
```
public class PrototypeClass implements Cloneable {
    @Override
    protected PrototypeClass clone()  {
        PrototypeClass prototypeClass  = null;

        try {
            prototypeClass = (PrototypeClass) super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }

        return prototypeClass;
    }
}
```

- Client.java
```
public class Client {
    public static void main(String[] args) {
        PrototypeClass prototypeClass = new PrototypeClass();
        PrototypeClass clonePrototypeClass = prototypeClass.clone();
    }
}
```

### 6、注意事项
1. 构造函数不会被执行   
2. 浅拷贝和深拷贝
> 注意：
1.使用原型模式时，引用的成员变量必须满足两个条件才会被拷贝：一是类的成员变量，而不是方法内变量；二是必须是一个可变的引用对象，而不是一个原始类型或不可变对象。
2.深拷贝和浅拷贝建议不要混合使用，特别是在涉及类的继承时，父类有多个引用的情况就非常复杂，建议的方案是深拷贝和浅拷贝分开实现。
3. clone与final两个会冲突。

## 七、模板方法模式
### 1、定义
模板方法模式
: 定义一个操作中的算法的骨架，而将一些步骤延迟到子类中。使用子类可以不改变一个算法的结构即可重定义该算法的某些特定步骤。

### 2、使用
- 多个子类有公有的方法，并且逻辑基本相同时
- 重要、复杂的算法，可以把核心算法设计为模板方法，周边的相关细节功能则由各个子类实现。
- 重构时，模板方法模式是一个经常使用的模式，把相同的代码抽取到父类中，然后通过钩子函数约束其行为。

### 3、优点
- 封闭不变部分，扩展可变部分
- 提取公共部分代码，便于维护
- 行为由父类控制，子类实现


### 4、类图
![模板方法模式](https://www.processon.com/chart_image/573e68ffe4b0efb527112e0c.png)

### 5、示例
- HummerModel.java
```
public abstract class HummerModel {
    public abstract void start();
    public abstract void stop();
    public abstract void alarm();
    public abstract void engineBoom();

    public void run() {
        start();
        engineBoom();
        if (isAlarm()) {
            alarm();
        }
        stop();
    }

    protected boolean isAlarm() {
        return true;
    }
}
```

- HummerH1Model.java
```
public class HummerH1Model extends HummerModel {
    private boolean alarmFlag = true;

    @Override
    public void start() {
        System.out.println("悍马H1发动。。。");
    }

    @Override
    public void stop() {
        System.out.println("悍马H1停车。。。");
    }

    @Override
    public void alarm() {

        System.out.println("悍马H1鸣笛。。。");
    }

    @Override
    public void engineBoom() {
        System.out.println("悍马H1引擎声音是这样的。。。");
    }

    @Override
    protected boolean isAlarm() {
        return alarmFlag;
    }

    public void setAlarmFlag(boolean alarmFlag) {
        this.alarmFlag = alarmFlag;
    }
}
```

- Client.java
```
public class Client {
    public static void main(String[] args) {
        HummerH1Model h1 = new HummerH1Model();
        h1.setAlarmFlag(false);
        h1.run();
    }
}
```

## 八、外观模式
### 1、定义
外观模式
: 为子系统中的一组接口提供一个一致的界面，此模式定义了一个高层接口，这个接口使得这一子系统更加容易使用。

### 2、使用
1. 在设计初期阶段，应该要有意识的将不同的两个层分离，层与层之间建立外观Facade，这样可以为复杂的子系统提供一个简单的接口，使得耦合大大降低。
2. 在开发阶段，子系统往往因为不断重构演化而变得越来越复杂，增加外观Facade可以提供一个简单的接口，减少它们之间的依赖。
3. 在维护一个遗留的大型系统时，可能这个系统已经非常难以维护和扩展了，这时可以为新系统个外观Facade类，来提供设计粗糙或高度复杂的遗留代码的比较清晰简单的接口，让新系统与Facade对象交互，Facade与遗留代码交互所有复杂的工作。

### 3、优点
- 减少系统的相互依赖
- 提高了灵活性
- 提高安全性
- 

### 4、类图

### 5、示例




