#### 工厂模式
工厂模式主要是为创建对象提供过渡接口，以便将创建对象的具体过程屏蔽隔离起来，达到提高灵活性的目的。

特点： 
1) 当客户程序不需要知道要使用对象的创建过程。
2) 客户程序使用的对象存在变动的可能，或者根本就不知道使用哪一个具体的对象。

工厂模式在《Java 与模式》中分为三类：

1）简单工厂模式（Simple Factory）

2）工厂方法模式（Factory Method）

3）抽象工厂模式（Abstract Factory）

这三种模式从上到下逐步抽象，并且更具一般性。

###### 简单工厂模式
通过工厂的判断,来调用接口的具体不同的实现类
```Java
//抽象产品角色
public interface Car{
    public void drive();
}
//具体产品
public class BCar implements Car{
    public void drive() {
        System.out.println("B Car");
    }
}

public class CCar implements Car{
    public void drive() {
        System.out.print("C Car");
    }
}

//简单工厂类
public class Driver{
	public static Car driverCar(String s) {
		switch (s) {
			case "B": return new BCar();
			case "C": return new CCar();
			default: return null;
		}
	}
}
```
###### 工厂方法模式
工厂方法模式去掉了简单工厂模式中工厂方法的静态属性，使得它可以被子类继承。
```Java
//抽象工厂角色
public interface Driver{
	public Car driverCar();
}
public class BDriver implements Driver{
	public Car driverCar(){
		return new BCar();
	}
}
public class CDriver implements Driver{
	public Car driverCar() {
		return new CCar();
	}
}
```
###### 抽象工厂模式
更加一般性的工厂方法模式
```Java
interface IProduct1 {
	public void show();
}
interface IProduct2 {
	public void show();
}
 
class Product1 implements IProduct1 {
	public void show() {
		System.out.println("这是1型产品");
	}
}
class Product2 implements IProduct2 {
	public void show() {
		System.out.println("这是2型产品");
	}
}
 
interface IFactory {
	public IProduct1 createProduct1();
	public IProduct2 createProduct2();
}
class Factory implements IFactory{
	public IProduct1 createProduct1() {
		return new Product1();
	}
	public IProduct2 createProduct2() {
		return new Product2();
	}
}
 
public class Client {
	public static void main(String[] args){
		IFactory factory = new Factory();
		factory.createProduct1().show();
		factory.createProduct2().show();
	}
}
```
