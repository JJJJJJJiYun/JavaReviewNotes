# 六、Java Web

## 1. jsp 和 servlet 的区别

- jsp 经编译后就成为了 servlet，本质上没有区别
- jsp 负责页面表现，可以和 html 共同展现，servlet 负责逻辑控制，是一个 Java 类
- Servlet 中没有内置对象，Jsp 中的内置对象都是必须通过HttpServletRequest 对象，HttpServletResponse 对象以及 HttpServlet 对象得到

## 2. jsp 有哪些内置对象及其作用

- request：封装客户端的请求，其中包含来自GET或POST请求的参数
- response：封装服务器对客户端的响应
- pageContext：通过该对象可以获取其他对象
- session：封装用户会话的对象
- application：封装服务器运行环境的对象
- out：输出服务器响应的输出流对象
- config：Web应用的配置对象
- page：JSP页面本身（相当于Java程序中的this）
- exception：封装页面抛出异常的对象

## 3. jsp 的四种作用域

- page 代表与一个页面相关的对象和属性
- request 代表与 Web 客户端发出的一个请求相关的对象和属性。一个请求可能跨越多个页面，涉及多个 Web 组件，需要在页面显示的临时数据可以置于此作用域
- session 代表与某个用户与服务器建立的一次会话相关的对象和属性。跟某个用户相关的数据应该放在用户自己的session中
- application 代表与整个Web应用程序相关的对象和属性，它实质上是跨越整个Web应用程序，包括多个页面、请求和会话的一个全局作用域

## 4. session 和 cookie 有什么区别

- 保存位置：session 在服务器，cookie 在客户端
- 安全性：session 用唯一的 session id 标识，较安全，cookie 储存在客户端上，用户可见，不安全
- 大小：session 可能较大，可能会用到单独服务器，cookie 较小

## 5. session 的工作原理

- 类似于一个 HashMap

## 6. 如果客户端禁用了 cookie 那么 session 还能用吗

- 一般来说 session id 会放在 cookie 中
- 但也可以通过 url 传值或者表单传值的方式传递

## 7. spring mvc 和 struts 的区别

- 拦截机制的不同
  - Struts2 是类级别的拦截，每次请求就会创建一个 Action，和 Spring 整合时 Struts2 的 ActionBean 注入作用域是原型模式 prototype，然后通过setter，getter 把 request 数据注入到属性。Struts2 中，一个 Action 对应一个 request，response 上下文，在接收参数时，可以通过属性接收，这说明属性参数是让多个方法共享的。Struts2 中 Action 的一个方法可以对应一个 url，而其类属性却被所有方法共享，这也就无法用注解或其他方式标识其所属方法了，只能设计为多例
  - SpringMVC 是方法级别的拦截，一个方法对应一个 Request 上下文，所以方法直接基本上是独立的，独享 request，response 数据。而每个方法同时又和一个url 对应，参数的传递是直接注入到方法中的，是方法所独有的。处理结果通过ModeMap 返回给框架。在 Spring 整合时，SpringMVC 的 Controller Bean 默认单例模式 Singleton，所以默认对所有的请求，只会创建一个 Controller，有应为没有共享的属性，所以是线程安全的，如果要改变默认的作用域，需要添加 @Scope注解修改
- 底层框架的不同
  - Struts2 采用 Filter（StrutsPrepareAndExecuteFilter）实现，SpringMVC（DispatcherServlet）则采用 Servlet 实现。Filter在容器启动之后即初始化；服务停止以后销毁，晚于Servlet。Servlet在是在调用时初始化，先于Filter调用，服务停止后销毁
- 性能方面
  - Struts2 是类级别的拦截，每次请求对应实例一个新的 Action，需要加载所有的属性值注入，SpringMVC 实现了零配置，由于 SpringMVC 基于方法的拦截，有加载一次单例模式 bean 注入。所以，SpringMVC 开发效率和性能高于 Struts2
- 配置方面
  - spring MVC 和 Spring 是无缝的。从这个项目的管理和安全上也比 Struts2高
  - Struts2 有自己的拦截 Interceptor 机制，SpringMVC 这是用的是独立的Aop 方式，这样导致 Struts2 的配置文件量还是比 SpringMVC大

## 8. 如何避免 sql 注入

- PreparedStatement（简单又有效的方法）
- 使用正则表达式过滤传入的参数
- 字符串过滤
- JSP中调用该函数检查是否包函非法字符
- JSP页面判断代码

## 9. 什么是 XSS 攻击以及如何避免

- XSS 攻击又称 CSS，全称 Cross Site Script  （跨站脚本攻击），其原理是攻击者向有 XSS 漏洞的网站中输入恶意的 HTML 代码，当用户浏览该网站时，这段 HTML 代码会自动执行，从而达到攻击的目的。XSS 攻击类似于 SQL 注入攻击，SQL注入攻击中以SQL语句作为用户输入，从而达到查询/修改/删除数据的目的，而在 XSS 攻击中，通过插入恶意脚本，实现对用户游览器的控制，获取用户的一些信息。 XSS是 Web 程序中常见的漏洞，XSS 属于被动式且用于客户端的攻击方式

## 10. 什么是 CSRF 攻击以及如何避免

- CSRF（Cross-site request forgery）也被称为 one-click attack 或者 session riding，中文全称是叫跨站请求伪造。一般来说，攻击者通过伪造用户的浏览器的请求，向访问一个用户自己曾经认证访问过的网站发送出去，使目标网站接收并误以为是用户的真实操作而去执行命令。常用于盗取账号、转账、发送虚假消息等。攻击者利用网站对请求的验证漏洞而实现这样的攻击行为，网站能够确认请求来源于用户的浏览器，却不能验证请求是否源于用户的真实意愿下的操作行为