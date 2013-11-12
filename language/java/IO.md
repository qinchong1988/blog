java IO Ŀ¼
-----
1. [SystemDemo]（#SystemDemo） �������� System��

2. RuntimeDemo

3. DateDemo ������

4. CalendarDemo ���� 

5. CalendarDemo2 ��ϰ

6. MathDemo ��������Math ��Random

7. FileWriterDemo �ļ�д

8. FileWriterDemo2 IO�쳣�Ĵ�����ʽ

9. FileWriterDemo3 �ļ���д

10. FileReaderDemo �ı��ļ���ȡ��ʽһ��

11. FileReaderDemo2 �ı��ļ���ȡ��ʽ����int read(char[] cbuf) 

12. FileReaderTest �ı��ļ���д��ϰ��

13. CopyTest �ļ�����

## SystemDemo
```java
import java.util.Properties;

/*
 * System:���еķ��������Զ��Ǿ�̬�ġ�
 * out����׼������Ĭ���ǿ���̨
 * in:��׼���룬Ĭ���Ǽ���
 * 
 * ����ϵͳһЩ��Ϣ;
 * 
 * ��ȡϵͳ������Ϣ
 * public static Properties getProperties()
 */
public class SystemDemo {
	public static void main(String[] args) {
		Properties prop = System.getProperties();
		// ��ΪProperties��HashTable�����࣬Ҳ����Map���ϵ�һ����������
		// ��ô����ͨ��map�ķ���ȡ���ü����е�Ԫ��
		// �ü����д洢�Ķ����ַ�����û�з��Ͷ���

		// ������ϵͳ���Զ���һЩ������Ϣ�أ�
//		System.setProperty("mykey", "myvalue");
		// �ɲ�������jvm����ʱ����̬�ļ���һЩ������Ϣ�أ�
		String v = System.getProperty("haha");
		System.out.println("v=" + v);

		for (Object key : prop.keySet()) {
			String value = (String) prop.get(key);
			System.out.println(key + "::" + value);
		}
	}
}
```
