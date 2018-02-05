## 桥梁模式 (Bridge Pattern)

### 定义
> 桥梁模式/桥接模式，将**抽象和实现解耦**，使得两者可以独立地变化

### 通用类图
![](http://www.dofactory.com/images/diagrams/net/bridge.gif)

### 通用源码
##### 1.实现化角色
	public interface Implementor{
		public void doSomething();
		public void doAnything();
	}

##### 2.具体实现化角色
	public class ConcreteImplementorA implements Implementor{
		public void doSomething(){
			//业务逻辑处理
		}
		public void doAnything(){
			//业务逻辑处理
		}
	}

##### 3.抽象化角色
	public abstract class Abstraction{
		//定义对实现化角色的引用
		private Implementor imp;
		//约束子类必须实现该构造函数
		public Abstraction(Implementor _imp){
			this.imp = _imp;
		}
		//自身的行为和属性
		public void request(){
			this.imp.doSomething();
		}
		//获得实现化的角色
		public Implementor getImp(){
			return imp;
		}
	}

##### 4.具体抽象化角色
	public class RefinedAbstraction extends Abstraction{
		//覆写构造函数
		public RefinedAbstraction(Implementor _imp){
			super(_imp);
		}

		//修正父类的行为
		@Override
		public void request(){
			//业务处理
			super.request();
			super.getImp().doAnything();
		}
	}

##### 5.场景类
	public class Client{
		public static void main(String[] args){
			//定义一个实现化角色
			Implementor imp = new ConcreteImplementor1();
			//定义一个抽象化角色
			Abstraction abs = new RefinedAbstraction(imp);
			//执行行文
			abs.request();
		}
	}

### 优点
- 抽象与实现分离
- 优秀的扩充能力
- 实现细节对客户透明

### 注意事项
1.抽象角色引用实用角色，或者说抽象角色的部分实现是由实现角色完成的
2.发现类的继承有N层时，可以考虑使用桥梁模式
3.适用于不希望或不适用使用继承的场景，接口或抽象类不稳定的场景，重用性要求较高的场景

### 总结


### 参考