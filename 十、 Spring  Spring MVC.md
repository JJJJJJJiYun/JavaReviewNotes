# 十、 Spring / Spring MVC

## 1. AOP （Aspect-Oriented Programming）

- 切面编程，相对于 OOP 来说
- 用于对分散对象引入公共行为
- 将软件分为两部分：核心关注点和横切关注点，横切关注点一般发生在核心关注点的多处
- 将应用程序中的商业逻辑同对其提供支持的通用服务进行分离

## 2. IOC（Inversion of Control）

- 控制反转
- 将具有依赖关系的对象进行解耦，利用 IOC 容器进行拼接
- 原本如果 A 依赖于 B，那么在初始化 A 的时候或者要使用 B 时，必须主动创建 B，引入 IOC 容器后，IOC 容器会主动创建 B 并注入到 A 中需要的地方

## 3. Spring 的常用注入方式

- 构造方法注入

  ```xml
  <bean id="userService" class="com.lyu.spring.service.impl.UserService">
  	<constructor-arg ref="userDaoJdbc"></constructor-arg>
  </bean>
  ```
  - 在注册 bean 的时候传入构造方法所需参数

- setter 注入

- ```xml
  <!-- 注册userService -->
  <bean id="userService" class="com.lyu.spring.service.impl.UserService">
      <!-- 写法一 -->
      <!-- <property name="UserDao" ref="userDaoMyBatis"></property> -->
      <!-- 写法二 -->
      <property name="userDao" ref="userDaoMyBatis"></property>
  </bean>
  ```
  
  - 在注册 bean 的时候传入 property，对应在类中写上 set 方法
  
- 注解注入

  - 注册 bean 的注解：
    - @Component：可以用于注册所有bean
    - @Repository：主要用于注册dao层的 bean
    - @Controller：主要用于注册控制层的bean
    - @Service：主要用于注册服务层的 bean
  - 注册依赖的注解
    - @Resource：java的注解，默认以 byName 的方式去匹配与属性名相同的 bean 的 id，如果没有找到就会以 byType 的方式查找，如果 byType 查找到多个的话，使用 @Qualifier 注解（spring 注解）指定某个具体名称的 bean

    ```java
    @Resource
    @Qualifier("userDaoMyBatis")
    private IUserDao userDao;
    ```
    - @Autowired：spring 注解，默认是以 byType 的方式去匹配与属性名相同的 bean 的 id，如果没有找到，就通过 byName 的方式去查找

    ```java
    @Autowired
    @Qualifier("userDaoJdbc")
    private IUserDao userDao;
    ```

