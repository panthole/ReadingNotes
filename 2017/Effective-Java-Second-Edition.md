##Java Effective(second Edition)
#####第14条 公有类中使用私有域和公有访问(getter)/设值(setter)方法
* 原因：public类的实例域必须私有防止外部直接访问，失去完全性
* 包私有类或私有嵌套类可以不必这样
* 不可变域，如public final类 + public final域用于只读可以接受

#####第15条 使可变性最小
* 不可变类只是其实例不能被修改的类
* 使类成为不可变
 * 1.不要提供任何改变对象属性的方法
 * 2.保证类不会被扩展
 * 3.使**所有的域都是final的**
 * 4.使所有的域都成为私有的
 * 5.确保对于任何可变组件的互斥访问
* 不可变对象本质上是线程安全的，不要求同步，可以被自由的共享，不需要进行保护性拷贝
* 不可变对象为其他对象提供了大量的构件
* 不可变类的缺点：对于每个不同的值都需要一个单独的对象，存在性能问题
* 构件不可变类的两个方法：**使类成为final的**，**私有构造器添加公有静态工厂**
* 坚决不要为每个get方法编写一个相应的set方法

#####第16条 当一个类扩展另一个类时，复合优于实现继承
* 实现继承（implementation inheritance）,当一个类扩展另一个类的时候
* 接口继承（interface inheritance）,当一个类实现一个接口的时候，或者当一个接口扩展另一个接口的时候
* 继承打破了封装性
* 原因：子类脆弱不安全，超类存在自用性方法导致不安全，超类可以获得新的方法
* 包装类可以实现于多类继承的功能
* 包装类不适合用回调框架
* 只有当子类和超类确实存在子类型关系时，使用继承才是恰当的。判断是否适合继承，一是明确两者确实存在is-a关系，每个子类确实也是父类。二是对于试图扩展的类，它的API中没有缺陷
* 如果子类覆盖了父类的方法，父类调用该方法时走子类的调用

#####第17条 为继承提供文档说明
* 可覆盖(overridable)的方法，是指非final的，公有的或受保护的
* 类必须有文档说明其每个公有的或受保护的方法或者构造器调用了哪些可覆盖方法。
* 构造器决不能调用可被覆盖的方法，无论是直接调用还是间接调用
* 无论是clone还是readObject,不能调用可被覆盖的方法，无论是直接调用还是间接调用
* 禁止子类化的两种方式：
  * 把类声明为final的
  * 把所有构造器都变成私有的，或者包级私有的，并增加一些共有的静态工厂来替代构造器
* 安全地进行子类化，合理的办法是确保类永远不会调用它的任何可覆盖的方法，完全消除这个类中可覆盖方法的自用特性
* 如果类实现了Serializable，并且该类有一个readResolve或者writeReplace方法，继承这个类的时候，就必须使得readResolve或者writeReplace成为受保护的方法，而不是私有方法。

#####第18条 接口优于抽象类
* 接口与抽象类的区别：
  * 抽象类允许包含某些方法的实现，但是接口则不允许
  * 为了实现由抽象类定义的类型，类必须成为抽象类的子类
  * 接口不用管类处于类层次的哪个位置
* 接口优点：
  * 现有的类可以很容易被更新，以实现新的接口。因为接口的类层次不高，而抽象类需要放到类层次的高处。
  * 接口是定义混合类型的理想选择。除了实现基本类型还能实现混合类型
  * 接口允许我们构造非层次结构的类型框架
* 总结的来说，接口优于抽象类是由于类层次不需要高处，而骨架实现优于接口。骨架实现就不直接提供接口，而是用抽象类实现接口，确定接口中最基本的方法，这些方法将成为骨架中的抽象方法，接口中其他具体的方法提供具体的实现。
* 骨架实现的优势在于抽象类的演变比接口的演变容易得多。解决了接口改变导致的实现类都需要改变问题。
 
#####第19条 接口只用于定义类型，不用于定义常量接口模式
* 常量接口是对接口的不良使用
* 导出常量的合理方案：
  * 如果常量与某个现有类或者接口紧密相关，就应该把这些常量添加到这个类或者接口中
  * 如果这些常量最好被看作枚举类型的成员，就应该用枚举类型（enum type）来导出这些常量
  * 使用不可实例化的工具类（utility class）来导出这些常量
* 利用Java版本1.5之后的静态导入（static import）机制，避免用类名来修饰常量名
* 接口应该只被用来定义类型，它们不应该被用来到处常量

#####第21条 用函数对象实例化具体策略类
* 如果具体策略类是无状态，没有域，那么这个类所有实例在功能上都是互相等价的。它作为一个**Singleton**是非常合适的，可以节省不必要的对象创建开销。
* 具体的策略类往往使用匿名类声明
* 使用匿名类将会在每次执行调用的时候创建一个新的实例，如果它被重复执行，考虑使用单例将函数对象存储到一个私有的静态final域里，并重用它。
* 当一个具体策略只被使用一次时，通常使用匿名类来声明和实例化这个具体策略类。当一个具体策略是设计用来重复使用的时候，它的类通常被实现为私有的静态成员类，并通过公有的静态final域被导出，其类型为该策略接口