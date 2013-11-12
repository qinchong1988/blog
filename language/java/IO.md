java IO
1. SystemDemo 其他对象 System。
2. RuntimeDemo
3. DateDemo 日期类
4. CalendarDemo 日期 
5. CalendarDemo2 练习
6. MathDemo ，工具类Math 和Random
7. FileWriterDemo 文件写
8. FileWriterDemo2 IO异常的处理方式
9. FileWriterDemo3 文件续写
10. FileReaderDemo 文本文件读取方式一；
11. FileReaderDemo2 文本文件读取方式二；int read(char[] cbuf) 
12. FileReaderTest 文本文件读写练习：
13. CopyTest 文件复制

SystemDemo
----------
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