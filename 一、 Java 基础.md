# 一、 Java 基础

## 1. JDK 和 JRE 区别

- JDK 是 Java Development Kit 是一个完整的 Java SDK，包括 JRE 和编译器（javac）和工具，能够创建和编译运行程序
- JRE 是 Java Runtime Environment 是一个运行时环境，只能运行已编译程序

## 2. == 和 equals 区别

- == 比较的是对象在内存中的地址
- equals 是判断两个对象是否相等，需要根据对象进行重写，默认和 == 相同

## 3. hashcode() 相同，则 equals() 也一定为 true，对吗

- 不对
- 反过来是对的

## 4. final 在 java 中有什么作用

- 修饰类：不能被继承
- 修饰方法：不能被重写，private 方法默认是 final 的
- 修饰变量：如果是基本数据类型，值不能被修改，如果是引用数据类型，不可以指向其他引用对象

## 5. java 中 Math.round()、ceil()、floor() 的区别

- round() 四舍五入取整，判断再数轴的那一小格里，超过 0.5 则向右，不超过则向左，Math.round(-1.5) == -1
- ceil() 向上取整，也就是向数轴右边取整
- floor() 向下取整，也就是向数轴左边取整

## 6. String 属于基本数据类型吗

- 不属于，是引用数据类型
- 基本数据类型只包含，boolean、byte(8-bits)、char(16-bits)、short(16-bits)、int(32-bits)、long(64-bits)、float(32-bits)、double(64-bits)

## 7. Java 中操作字符串都有哪些类，之间的区别是什么

- String、StringBuilder、StringBuffer

- String 是不可变对象，不可变是因为 String 类储存字符串用的是

- ```java
  private final char[]
  ```

- StringBuilder 和 StringBuffer 都是可变对象，继承自AbstractStringBuilder

- StringBuilder 线程不安全，StringBuffer 线程安全

## 8. String str = "i" 和 String str = new String("i") 一样吗

- 不一样
- String str = "i" 会优先查看常量池中是否存在 "i" 这个 String，如果有，直接引用常量池中的对象，如果没有会先在常量池中创建，并引用它
- String str = new String("i") 会先查看常量池中是否存在 "i" 这个 String，如果没有则创建，接着用这个常量池中的 "i" 去创建一个新的对象

## 9. 如何反转字符串

- 用 StringBuilder 或 StringBuffer 的 reverse() 方法

## 10. String 类的常用方法

- indexOf()：返回指定字符的索引。
- charAt()：返回指定索引处的字符。
- replace()：字符串替换。
- trim()：去除字符串两端空白。
- split()：分割字符串，返回一个分割后的字符串数组。
- getBytes()：返回字符串的 byte 类型数组。
- length()：返回字符串长度。
- toLowerCase()：将字符串转成小写字母。
- toUpperCase()：将字符串转成大写字符。
- substring()：截取字符串。
- equals()：字符串比较。

## 11. 抽象类必须要有抽象方法吗

- 不一定
- 只要声明为 abstract class 的都是抽象类

## 12. 普通类和抽象类有哪些区别

- 普通类不能有抽象方法
- 抽象类不可以被实例化为对象

## 13. 抽象类能使用 final 修饰吗

- 不可以，抽象类的实现就是为了被继承，如果用 final 修饰了就没有意义了

## 14. 接口和抽象类有什么区别

- 接口中的变量都是常量（public static final），抽象类中对变量的修饰符没有要求
- 接口中的方法都是抽象方法，抽象类中可以有普通方法，但 jdk 1.8 之后接口中也可以实现默认方法（default ...）
- 接口不可以有构造器，抽象类可以有
- 接口不可以有 main 方法，抽象类可以有
- Java 类只能单继承，但可以实现多个接口
- 接口是辐射型设计，更多的像行为规范，抽象类是模板类设计

## 15. Java 中 IO 流分为几种

- 按功能：输入、输出
- 按类型：字节流（InputStream、OutputStream）、字符流（Reader、Writer）

## 16. BIO、NIO、AIO 区别

- 同步和异步
  - 同步：发起一个调用，在被调用者执行完毕之前不返回
  - 异步：发起一个调用，立刻得到回应为已接受到请求，但不返回结果，等被调用者执行完毕后利用回调等机制返回结果
- 阻塞和非阻塞
  - 阻塞：发起一个请求，调用者一直等待结果返回，无法执行其他任务
  - 非阻塞：发起一个请求，调用者不用一直等待返回结果
- BIO 是 Blocking-IO，指同步阻塞 IO，会阻塞当前线程
- NIO 是 NEW-IO，也是 None-Blocking IO，指非阻塞 IO
  - Channel：通道，NIO 通过通道来进行读写，通道是双向的，改变通道的方向使用 flip() 函数
  - Buffer：缓冲区，NIO 是基于缓冲区的，所有数据都是用缓冲区处理的
  - Selector：选择器，NIO 使用选择器来利用单线程处理多通道，选择器会对通道进行轮询，直到某一个通道准备好读写
- AIO 是 Asynchronous-IO，指异步非阻塞 IO，应用还不是很广泛

## 17. Files 的常用方法有哪些

- Files.exists()：检测文件路径是否存在。
- Files.createFile()：创建文件。
- Files.createDirectory()：创建文件夹。
- Files.delete()：删除一个文件或目录。
- Files.copy()：复制文件。
- Files.move()：移动文件。
- Files.size()：查看文件个数。
- Files.read()：读取文件。
- Files.write()：写入文件。