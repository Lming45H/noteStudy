## jsp和jstl

------



### 	1.jsp

#### 			1.1jsp的基础用法

##### 			1.1.1 jsp简介

​				jsp：java Server Page SUN公司提供的动态网页编程技术，是java Web服务器的动态资源。

​				它相比html而言，html只能为用户提供静态资源，而jsp技术除了可以用java代码产生动态数据的同时，也很容易对数据进行排版。

​				不管是jsp还是servlet，虽然都可以用于开发动态web资源，但是由于这两门技术的各自的特点，在长期的软件实践中，人们逐渐把servlet作为web应用中的控制器组件来使用，而把jsp技术作为数据显示模板来使用。

​				其中jsp就是一个servlet，当我们第一次访问jsp的时候，jsp引擎都会将这个jsp编译成一个servlet，这个文件存放在tomcat中的work目录中。

##### 		1.1.2  注释

​				在jsp中支持两种注释的语法操作：

​				一种是显示注释，这种注释是允许客户端看见的；另一种是隐式注释，不允许客户端看见的。

​				（1）显示注释：从html风格继承而来

​				（2）隐式注释：从java风格继承而来，jsp自己的注释

​				jsp的三种注释方式：

```jsp
1.//注释，单行注释 /* 多行注释*/
2.<!-- html风格注释-->
3.<%-- jsp注释 --%>
```

##### 		1.1.3  Scriptlet

​				在jsp中最重要的部分就是scriptlet(脚本小程序)，所有嵌入在html代码中的java程序。在jsp中一共又三种script代码：都必须用scriptlet标记出来。

```jsp
第一种：<%  %>:java脚本段，可以定义局部变量，编写语句
第二种：<%! %>:声明定义全局变量，方法，类
第三种：<%= %>:表达式
```

#### 		1.2 jsp的指令标签

​				使用包含操作，可以将公共代码抽离出来进而引入。

##### 				1.1.4.1 include静态包含

```jsp
<%@ include file="要包含的文件路径" %> <!--相对路径-->
```

​				原理：使用静态包含实际是jsp编译成java代码之前将引入的jsp文件一起在jspservice方法中生成一个servlet对象，耦合度高。

##### 				1.1.4.2 include动态包含

```jsp
<jsp:include page="要包含的文件路径"></jsp:include>
```

​				原理：动态包含实质是对要包含的jsp文件的一次调用，生成多个java文件，实质是多个servlet，因此可包含同名变量。

#### 			1.3 jsp的四大域对象

​					page作用域: 在当前页面有效，跳转后无效

​					request作用域：在一次请求中有效，服务端跳转有效，客户端跳转无效，跳转用请求转发，重定向作用域会失效

​					session作用域：在一次会话中有效，服务器和客户端跳转都有效。会话：一个浏览器

​					application作用域：只要服务器不关闭都有效

##### 					jsp的跳转方式

​						1.服务器跳转		

```jsp
<jsp:forword page="要跳转的地址"></jsp:forword>
```

​						2.客户端跳转

```html
<a></a> 超链接跳转
```

#### 			1.4 EL 表达式

​						EL(Expression language)是为了使jsp写起来更简单。

```jsp
格式：${prarmeter}
```

​						EL表达式一般操作的都是域对象中的数据，操作不了局部变量。**当数据为空时，返回空字符串，为不是null**.如果域对象同名，则按小范围优先。

​						域对象的概念在jsp中一共有四个：pageContext,request,session,application,范围依次是当前页面，一次请求，一次会话，整个应用。

##### 						1.4.1 EL Empty

```jsp
<%--
	empty
		判断域对象是否为空，为空返回true，否则返回false
			${empty 域变量名}
			${!empty 域变量名}
--%>
```

##### 						1.4.2 EL 运算

```jsp
1.等值比较 大小比较  +-*/
```



### 	2.	jstl

##### 			2.1.标签的使用

​				java Server Pages Standard Tag Libray:jsp标准标签库，是一个定制的标签库的集合，用于解决一些常见的问题，例如迭代一个映射和集合，条件测试，xml处理。使用需要下载jar包。

​			**核心标签库：**

​				http://java.sun.com/jsp/jstl/core

​				包含web应用的常见工作，比如：循环，表达式赋值，基本输入输出。

​			**格式化标签库：**

​				http://java.sun.com/jsp/jstl/fmt

​				用来格式化显示数据的工作，比如：对不同区域的日期格式化。

```jsp
格式：<%@taglib url="" prefix=" %>"
```

##### 			2.2 fomatdate日期格式

```jsp
格式：<fmt:formatDate
		value="日期对象"
		type="格式化类型"
		pattern="自定义类型"
	</fmt:formatDate>
```

### 3.过滤器和监听器

##### 	3.1介绍

​		Filter即为过滤，用于在servlet之外对request或response进行修改，它主要用于对用户请求进行预处理。也可以对response响应进行后处理，完整流程为：Filter对用户的请求进行预处理，接着将请求交给servlet进行处理并生成响应，接着Filter在对服务器响应进行后处理，一个web应用可以编写多个Filter，称为Filter链。

​	过滤器

​		1.@webFilter("拦截路径")

​		2.doFilter() 方法中要设置放行，否则无法到达资源

​		filterChain.doFilter(servletrequest,servletresponse)

​		3.如果是过滤器链，先配置的先执行(首字母在前) 响应反过来。

##### 	3.2 非法访问拦截

​		拦截资源

​				拦截所有资源 /*

​		需要放行的资源(判断路径)

​				1.指定页面 放行 (无需登录即可访问 如：登录页面，注册页面)

​				2.静态资源 放行 (image,css,js)

​				3.指定操作 放行 (无需登录即可执行的操作，登录，注册)

​				4.登录状态放行 (判断session中是否为空)