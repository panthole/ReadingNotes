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

###注意事项
1. 策略模式使用的就是面向对象的**继承**和**多态机制**
2. 策略模式的重点是**封装角色**，它与代理模式的差别是策略模式的封装角色和被封装的策略类不用是同一个接口，如果是**同一个接口**那就成为了**代理模式**
3. 如果策略家族的具体策略数量**超过4个**，则需要考虑使用**混合模式**，解决策略类膨胀和对外暴露的问题
