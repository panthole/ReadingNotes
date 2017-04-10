## 策略模式 (Strategy Pattern)

### 定义
> 策略模式也叫做政策模式（Policy Pattern）,定义一组算法，将每个算法都封装起来，并且使它们之间互换。

### 通用类图
![](http://www.dofactory.com/images/diagrams/net/strategy.gif)

### 通用源码
##### 1.策略接口
	public interface IStrategy{
		//策略模式的运算法则
		public void doSomething();
    }
##### 2.具体策略类
	public class ConcreteStrategy implements Strategy{
		public void doSomething(){
			System.out.println("具体策略类的运算法则")
		}
	}
##### 3.封装角色
	public class Context{
		//抽象策略
		private IStrategy strategy = null;

		//构造函数设置具体策略
		public Context(IStrategy strategy){
			this.strategy = strategy;
		}

		//封装后的策略方法
		public void doSomething(){
			this.strategy.doSomething();
		}
	}

##### 4.高层模块
	public class Client{
		public static void main(String[] args){
			//声明一个具体的策略
			IStrategy strategy = new ConcreteStrategy();
			//声明上下文对象
			Context context = new Context(strategy);
			//执行封装后的方法
			context.doSomething();
		}
	}

### 优点
- 算法可以自由切换
- 避免使用多重条件判断（**避免条件语句判断**）
- 扩展性良好

### 缺点
- 策略类数量增多
- 所有的策略类都需要对外暴露（**可以使用工厂方法模式，代理模式和享元模式修正**）

### 扩展
##### 策略枚举
	public enum Calculator{
		//加法运算
		ADD("+"){
			public int exec(int a, int b){
				return a + b;
			}
		},
		//减法运算
		SUB("-"){
			public int exec(int a, int b){
				return a - b;
			}
		};
		String value = "";
		//定义成员值类型
		private Calculator(String _value){
			this.value = _value;
		}
		//获得枚举成员的值
		public String getValue(){
			return this.value;
		}
		//声明一个抽象函数
		public abstract int exec(int a, int b);
	}
#
	public class Client{
		public static void main(String[] args){
			int a = Integer.parseInt(args[0]);
			String symbol = args[1];
			int b = Integer.parseInt(args[2]);
			System.out.println("输入的参数为：" + Arrays.toString[args]);
			System.out.println("运行结果为："+a + symbol + b + "=" + Calculator.ADD.exec(a,b));
		}
	}

### 注意事项
1. 策略模式使用的就是面向对象的**继承**和**多态机制**
2. 策略模式的重点是**封装角色**，它与代理模式的差别是策略模式的封装角色和被封装的策略类不用是同一个接口，如果是**同一个接口**那就成为了**代理模式**
3. 如果策略家族的具体策略数量**超过4个**，则需要考虑使用**混合模式**，解决策略类膨胀和对外暴露的问题
4. **策略枚举**是一个非常优秀和方便的模式，但是它受枚举类型的限制,每个枚举项都是public、final、static的，扩展性受到了一定的约束，因此在系统开发中，策略枚举一般担当不经常发生变化的角色

### 总结
**策略模式**是由面向对象的**继承**和**多态**实现的，如果它的**封装对象**实现**策略接口**就成为**代理模式**了。策略模式最大的用途是用于多个算法的**选择**，“选择”这个实现可以用**条件语句**、**三目运算符**、**策略模式**、**策略枚举**等实现。策略模式最大的弊端就是**类对外暴露**，这个可以通过**工厂方法模式**，**代理模式**和**享元模式**修正。同时，可以不实现具体策略类，而在使用时通过**匿名函数**、lambda表达式**实现策略接口**，但是，这会导致每次执行调用的时候创建一个新的实例。所以，当一个具体策略**只被使用一次**时，通常使用匿名类来声明和实例化这个具体策略类。当一个具体策略是设计用来**重复使用**的时候，就可以考虑使用**单例模式**实现具体策略类，它的类通常被实现为私有的静态成员类，并通过公有的静态final域被导出，或者使用策略枚举。
