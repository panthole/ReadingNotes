## 责任链模式 (Chain Pattern)

### 定义
> 建造者模式/生成器模式是指将一个复杂对象的构建与它的表示分离，使得同样的构建过程可以创建不同的表示

### 通用类图
![](http://www.dofactory.com/images/diagrams/Net/Chain.gif)

### 通用源码
##### 1.产品类
	public class Product{
		public void doSomething(){
			//独立业务处理
		}
    }
##### 2.抽象建造者
	public abstract class Builder{
		public abstract void setPart();

		public abstract Product buildProduct();
	}
##### 3.具体建造者
	public class ConcreteProduct extends Builder{
		private Product product = new Product();
		
		public void setPart(){
		}
		
		public Product buildProduct(){
			return product;
		}
	}

##### 4.导演类
	public class Director{
		private Builder builder = new ConcreteProduct();
		
		public Product getAProduct(){
			builder.setPart();
			return builder.buildProduct();
		}
	}

### 优点
- 封装性
- 建造者独立，容易扩展
- 便于控制细节风险

### 扩展

### 注意事项
1.建造者模式最主要的功能是基本方法的调用**顺序**安排；而工厂方法则重点是创建


### 总结
建造者关注的是零件的调用顺序，工厂方法关注的是零件的创建

### 参考