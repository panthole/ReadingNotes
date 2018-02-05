## 单例模式 (Singleton Pattern)

### 定义
> 单例模式是指确保某一个类只有一个实例，而且自行实例化并向整个系统提供这个实例

### 通用类图
![](http://www.dofactory.com/images/diagrams/net/Singleton.gif)

Singleton类成为单例类，通过**使用private的构造函数**确保了在应用中只产生一个实例，并且是自行实例化的。

### 通用源码
	public class Singleton{
		private static final Singleton singleton = new Singleton();
		//限制产生多个对象
		private Singleton(){
		}

		//通过该方法获得实例对象
		public static Singleton getInstance(){
			return singleton;
		}
		
		//类中其他方法，尽量是static
		public static void doSomething(){
		}
	}