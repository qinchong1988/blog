java IO 目录
-----
* [SystemDemo](#systemdemo) 其他对象 System。
* [RuntimeDemo](#runtimedemo)
* DateDemo 日期类
* CalendarDemo 日期 
* CalendarDemo2 练习
* MathDemo ，工具类Math 和Random
* FileWriterDemo 文件写
* FileWriterDemo2 IO异常的处理方式
* FileWriterDemo3 文件续写
* FileReaderDemo 文本文件读取方式一；
* FileReaderDemo2 文本文件读取方式二；int read(char[] cbuf) 
* FileReaderTest 文本文件读写练习：
* CopyTest 文件复制

## SystemDemo
```java
import java.util.Properties;

/*
 * System:类中的方法和属性都是静态的。
 * out：标准输出，默认是控制台
 * in:标准输入，默认是键盘
 * 
 * 描述系统一些信息;
 * 
 * 获取系统属性信息
 * public static Properties getProperties()
 */
public class SystemDemo {
	public static void main(String[] args) {
		Properties prop = System.getProperties();
		// 因为Properties是HashTable的子类，也就是Map集合的一个子类对象
		// 那么可以通过map的方法取出该集合中的元素
		// 该集合中存储的都是字符串，没有泛型定义

		// 如何在系统中自定义一些特有信息呢？
//		System.setProperty("mykey", "myvalue");
		// 可不可以在jvm启动时，动态的加载一些属性信息呢？
		String v = System.getProperty("haha");
		System.out.println("v=" + v);

		for (Object key : prop.keySet()) {
			String value = (String) prop.get(key);
			System.out.println(key + "::" + value);
		}
	}
}
```

## RuntimeDemo
```java
/*
 * Runtime对象，该类并没有提供构造函数
 * 说明不可以new对象，那么会直接想到该类中的方法都是静态的。
 * 发现该类中还有非静态方法。
 * 说明该类肯定会提供方法获取本类对象，而且该方法是静态的，并返回值类型是本类类型。
 * 
 * 由这个特点可以看出该类使用了单例设计模式
 * 该方式是 static Runtime getRuntime();
 */
public class RuntimeDemo {
 
	public static void main(String[] args) throws Exception {
	   Runtime r = Runtime.getRuntime();
	   Process p  =r.exec("notepad.exe RuntimeDemo.java");
	   
	   //Thread.sleep(4000);
	   //p.destory();
	}

}
```
