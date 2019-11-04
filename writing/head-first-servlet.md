1. HTTP 请求流三要素：http方法，请求地址，表单参数
2. HTTP 响应流三要素：状态码，响应内容的类型，响应内容
3. HTTP协议
4. HTTP方法：get,post,head.trace,delete,put,options,connect
5. get 与 post 的区别（表单提交默认采用get）：
	+ get参数追加在url中，url 总长度有限
	- 追加在 url 里的请求参数会暴露在地址栏里
	+ get 可以建立书签，post不能
	- get与post的请求意义不同，get获取，post更新服务器，涉及请求的幂等性（HTTP 1.1 规定 get，head,put 是幂等的，post不是，当然可以自定义这些方法的幂等性问题，put与post都是用来更改服务器数据的，put表示幂等，post则不是 ）    
6. content-type 展示的 mime 内容类型值，必须是 accept 中指定的值
7. TCP 端口是一个16位数（2^16=65535,服务器上一共有65536个端口，0-65535），标识服务器硬件上的一个特定的软件程序（唯一标识），逻辑连接，0-1023为保留端口，供公知服务程序使用
8. URL：协议://服务器:端口/路径（Unix语法）/资源（默认是index.html） 
9. web 服务器只处理静态资源，动态资源由 web 服务器转交给一个 辅助应用处理（他处理1.动态内容，2.表单数据，以前都是 CGI 程序），最终 servlet 取代了 CGI（尤其是perl CGI）
10. web.xml 部署描述文件（英文名 DD） <web-app> ... </web-app>，提供了一种“声明”机制来定制web应用，而不用修改源代码
11. 在 servlet 中创建一个动态的 web 页面，必须把整个 HTML 打印出来，如：response.getWriter.println("<html>...</html>"); 这是把HTML放在了java里,不过很麻烦也很容易出错
12. JSP 可以实现把 java 放在 html 里，规定 jsp 中要尽可能少的放置 java 代码 <% ... %>
13. web 容器 管理 servlet ，servlet 没有 main 方法，有容器调用管理 
14. 容器提供：通信支持，servlet 生命周期管理，多线程支持，声明式安全管理，JSP翻译
15. 请求与响应对象（HttpServletRequest,HttpServletResponse）由容器创建与销毁，是注入 servlet 中的，在 servlet 生命周期外
16. 基本上 servlet 都是 HttpServlet
17. servlet 与 jsp ，业务逻辑 与 表示层 的 设计分离
18. MVC ，业务逻辑 与 表示 分离 后，也要实现 业务逻辑（M 模型包含业务逻辑与状态） 的可重用，加上一层 控制器 C 达到 业务逻辑 不和 表示 交互
19. J2EE 是一种超级规范，包括 针对 web 容器的（servlet 规范和 jsp 规范），和 针对 EJB 容器的（EJB 规范），所以，一个完整的 J2EE 服务器 应该包括 一个 web 容器和一个 EJB 容器，Tomcat 只是一个 web 容器，基本是没有独立的 EJB 容器  
20. servlet 的任务是得到一个请求，发回一个响应
21. 容器根据url找到正确的servlet，调用其service(),并传递请求与响应对象（HttpServletRequest,HttpServletResponse），service方法根据请求的HTTP方法来决定调用具体的servlet方法
22. 继承体系：Servlet(接口，三个生命周期方法，两个其他) --> GenericServlet（抽象类，实现了基本的servlet方法） -->  HttpServlet（Servlet的HTTP特性实现，get,post,在前面没有，属于HTTP特性）  
23. 空构造（在这里操作时机过早），用户初始化在init方法中，三个生命周期方法：init(初始化，一生只调用一次),service(具体处理，每一个请求都有独立的线程调用service)，destroy（资源回收，一生只调用一次）  
24. 一个JVM中的容器正常情况只维持一个 servlet 实例，运行多个线程来处理对一个 servlet 的多个请求  
25. 寻找类，然后加载类（加载可能发生在容器启动时，也可能发生在第一次客户请求时）  
26. 构造函数（不建议用户操作） 只是令其成为一个普通对象，要成为 servlet 必须给其注入 servlet特性，在构造与init（init使servlet可以访问servletConfig和servletContext）之间，servlet 对象处在 一种薛定谔servlet状态中（两不完全），实现了一点servlet代码，但仅仅是一点  
27. HttpServletRequest , HttpServletResponse 都是接口，具体实现交给容器开发商,ServletRequest-->HttpServletRequest,ServletResponse-->HttpServletResponse  
28. servlet 模型中只内置提供了HTTP特性的servlet，尚未包含其他特性的servlet  
29. ServletRequest的getInputStream()，返回只包含请求体，不包含请求的首部
30. getRemoteHost() 服务器的代码，远程即客户浏览器的端口； getServerPort请求原来发送到的端口 ；getLocalPort请求最后发送到的端口，服务器会为每个线程找一个不同的本地端口，来达到一个应用处理多个请求的目的  
31. getParameterValues("paramName") 用来获取一个指定参数包含多个值的情况，返回String[]
32. response.setContentType(),设置响应内容的类型（MIME类型），服务器一次只响应一种类型，不能中途更改毫无意义，response.getWriter(字符)(或者其他IO流getOutputStream(字节)，完成响应内容IO，可以实现HTML，jar多类型文件输出)
33. ctx.getResourceAsStream() "/"表示从应用的根目录开始
34. 重定向响应码 301，重定向地址在首部 Location属性 ，sendRedirect()可以使用绝对与相对地址，其中相对地址区别于"/",不带"/"表示相对于原资源的位置，带"/"表示/应用根目录开始的路径  
35. 
