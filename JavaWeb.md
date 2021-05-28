### JavaWeb

```html
//设置服务器启动后的默认页面
<welcome-file-list>
        <welcome-file>/html/login.html</welcome-file>
</welcome-file-list>
//配置前端页面请求对应的servlet
    <servlet>
        <servlet-name>hello</servlet-name>
        <servlet-class>com.bus.controller.loginServlet</servlet-class>
    </servlet>
   <!--从浏览器输入login 即从hello映射到servlet得实现类-->
    <servlet-mapping>
        <servlet-name>hello</servlet-name>//姓名映射
    <url-pattern>/login</url-pattern>//请求
    </servlet-mapping>
```

![image-20210518182607343](C:\Users\26728\AppData\Roaming\Typora\typora-user-images\image-20210518182607343.png)

```Java
@WebServlet(value = {"/login"})//注解式配置路径 内可配置多个路径
```

```java
//重定向
resp.sendRedirect("/Java_war_exploded/html/welcome.html");
/Java_war_exploded：tomcat指定目录
/html：web根目录下的html文件目录
```

```java
//解决tomcat无法加载css文件问题
<base href="/JavaWeb_war_exploded/">
<link rel="stylesheet" href="css/login.css">//web目录下的css文件目录
```

### 前端

###### margin在Y轴会发生塌陷现象
即大的包含进小的
width height表示内容的大小而不是盒子
盒子大小是 padding width/height +border
浮动特性 1.收缩 收缩到盒子内容周围 2.脱标：脱离标准文档流，如原来行内元素无宽高，浮动后就有了宽高，或覆盖。3.字围：浮动元素会被字围住。4.贴边：如果是左浮动自动往左边靠，左边不够往下边靠
清除浮动 clear:both 会导致margin失效

##### 

```css
//按钮添加阴影实现闪光（可多层）
#login_btn:hover {
  border-radius: 5px;
  color: #fff;
  background: #03e9f4;
  box-shadow: 0 0 5px 0 #03e9f4,
              0 0 25px 0 #03e9f4,
              0 0 50px 0 #03e9f4,
              0 0 100px 0 #03e9f4;
}
```

```css
//创建环绕线条环绕特效 使用span
#login_btn>span:nth-child(1){
  width: 100%;
  height: 2px;
  background: -webkit-linear-gradient(left,transparent,#03e9f4);线条流向，透明，颜色
  left: -100%;距离左边距离
  top: 0px;距离上层
  animation: line1 1s s linear infinite;特效动作名称，持续时间，等待时间，匀速，循环
}
@keyframes line1{
      50%,100%{
        left: 100%;从开始到结束的变化幅度
      }
    }
```