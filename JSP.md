# 一、JSP 介绍

JSP(全称 Java Server Pages)Java 服务端页面技术，是 JavaEE 平台下的技术规范。它允许使用特定的标签在 HTML 网页中插入 Java 代码，实现动态页面处理，所以 JSP 就是 HTML 与Java 代码的复合体。JSP 技术可以快速的实现一个页面的开发，相比在 Servlet 中实现页面开发将变得更加容易。

# 二、JSP 运行原理

## 1、JSP 技术特点

JSP 和 Servlet 是本质相同的技术。当一个 JSP 文件第一次被请求时，JSP 引擎会将该 JSP编译成一个 Servlet，并执行这个 Servlet。如果 JSP 文件被修改了，那么 JSP 引擎会重新编译这个 JSP。

JSP 引擎对 JSP 编译时会生成两个文件分别是.java 的源文件以及编译后的.class 文件，并放到 Tomcat 的 work 目录的 Catalina 对应的虚拟主机目录中的 org\apache\jsp 目录中。两个文件的名称会使用 JSP 的名称加”_jsp”表示。如：index_jsp.java、index_jsp.class。

## 2、JSP 与 Servlet 区别

JSP以源文件形式部署到容器中。而Servlet需要编译成class文件后部署到容器中.

JSP 部署到 web 项目的根目录下或根目录下的其他子目录和静态同资源位于相同位置。而Servlet 需要部署到 WEB-INF/classes 目录中。

JSP中的HTML代码会被JSP 引擎放入到Servlet的out.write()方法中.而在Servlet中我们需要自己通过对字符流输出流的操作生成响应的页面.

JSP更擅长表现于页面显示, Servlet更擅长于逻辑控制.



# 三、 JSP 的使用

## 1、JSP 的三种原始标签

JSP 的原始标签在 JSP 的任何版本中都可以使用。

### 1.1<%!  %> 声明标签

声明标签用于在JSP中定义成员变量与方法的定义。标签中的内容会出现在JSP被编译后的 Servlet 的 class 的0中。

### 1.2<%  %>脚本标签

脚本标签用于在JSP中编写业务逻辑。标签中的内容会出现在JSP被编译后的Servlet的_jspService 方法体中。_

### 1.3<%= %>赋值标签

赋值标签用于在JSP中做内容输出。标签中的内容会出现在_jspService方法的out.print()方法的参数中。注意我们在使用赋值标签时不需要在代码中添加";"。



## 2、JSP 原始标签的使用

需求：以 20%概率显示你中奖

```
<html>
<head>
    <title>Title</title>
</head>
<body>
欢迎来到中奖游戏
<%
int flag = new Random().nextInt(100);
if (flag <= 20){
 %>
中奖了  <%=flag %>
<% }else {%>
再试一次吧 <%= flag %>
<% } %>
</body>
</html>
```



## 3、 JSP 的指令标签

JSP 指令标签的作用是声明 JSP 页面的一些属性和动作。

```
<%@指令名称 属性=“值” 属性=“值”%>
```

## 4、JSP 指令标签分类

- page：主要声明 JSP 页面的一些属性
- include：静态包含.
- taglib：导入标签库

### 1、Page 指令标签

2.1.1.1 contentType					设置相应类型和编码

2.1.1.2 pageEncoding				设置页面的编码.

2.1.1.3 import							导入所需要的包。

2.1.1.4 language						当前 JSP 页面里面可以嵌套的语言。

2.1.1.5 session						设置JSP 页面是否获取 session 内置对象.

2.1.1.6 buffer							设置JSP 页面的流的缓冲区的大小。

2.1.1.7 autoFlush					是否自动刷新。

2.1.1.8 extends						声明当前 JSP的页面继承于那个类.必须继承的是 httpservlet 及其子类。

2.1.1.9 isELIgnored				是否忽略 el 表达式。

2.1.1.10 errorPage				当前 JSP 页面出现异常的时候要跳转到的 JSP 页面。	

2.1.1.11isErrorPage				当前JSP页面是否是一个错误页面。若值为 true,可以使用 JSP 页面的一个内置对象exception

### 2、Include 指令标签

静态包含,可以将其他页面内容包含进来,一起进行编译运行.生成一个 java 文件.

```
<%@include file=“被包含 JSP 的相对路径” %>
```

### 3、 Taglib 指令标签

导入标签库。

```
<%@taglib prefix=“前缀名” uri=“名称空间” %>
```

# 四、JSP 的内置对象

JSP 中一共预先定义了 9 个这样的对象，分别为：request、response、session、application、out、pagecontext、config、page、exception。

3.1request 对象				request对象是HttpServletRequest类型的对象。

3.2response 对象			response 对象是 HttpServletResponse 类型的对象。

3.3session 对象				session 对象是 HttpSession 类型的对象。只有在包含 session= “true”的页面中才可以被使用。

3.4application对象			application对象是ServletContext类型的对象

3.5out 对象						out对象是JspWriter类型的对象。

3.6config 对象					config 对象是 ServletConfig 类型的对象。

3.7pageContext 对象		pageContext对象是PageContext类型的对象。作用是取得任何范围的参数,通过它可以获取 JsP 页面的 out、request、reponse、session, application 等对象。pageContext对象的创建和初始化都是由容器来完成的，在 JSP 页面中可以直接使用 pageContext 对象。

3.8page 对象					page 对象代表 JSP 本身。

3.9exception 对象			exception 对象的作用是显示异常信息，只有在包含 isErrorPage="true"的页面中才可以被使用。



# 五、 请求转发

## 1、什么是请求转发

请求转发是服务端的一种请求方式，相当于在服务端中直接请求某个资源。	

RequestDispatcher dispatcher = request.getRequestDispatcher("/test.jsp");

dispatcher.forward(request,response);

简写方式：request.getRequestDispatcher("/test.jsp").forword(request,response);

![image-20231124102036652](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124102036652.png)

## 2、请求转发与重定向的区别

请求转发对于客户端浏览器而言是在一次请求与响应中完成，而重定向是在两次请求两次响应中完成。

请求转发并不会改变客户端浏览器的地址栏中的内容。而重定向会改变客户端浏览器地址栏中的内容。

请求转发可以使用 request 对象传递数据，而重定向不能使用 request 对象传递数据。

如果是处理的 DML 操作，建议使用重定向方式为客户端浏览器产生响应，可以解决表单重复提交现象。

## 3、请求转发案例

需求：在 Servlet 中获取客户端浏览器所支持的语言，并通过 JSP 页面将客户端浏览器所支持的语言响应给客户端浏览器。

```java
//需求：在 Servlet 中获取客户端浏览器所支持的语言，
// 并通过 JSP 页面将客户端浏览器所支持的语言响应给客户端浏览器。
@WebServlet("/language.do")
public class LanguageServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
    }

@Override
protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String header = req.getHeader("Accept-Language");
    req.setAttribute("key",header);
    req.getRequestDispatcher("showMsg.jsp").forward(req,resp);
}
}
```

showMsg.jsp:

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>

<head>
    <title>Title</title>
</head>

<body>
        <%
        String value = (String)request.getAttribute("key");
        %>
        当前支持的语言为:<%= value%>
</body>
</html>
```



运行结果：

![image-20231124102559995](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124102559995.png)

# 六、JSP 中的四大作用域对象

作用域：“数据共享的范围”，也就是说数据能够在多大的范围内有效。

|  对象名称   |     作用范围     |
| :---------: | :--------------: |
| application |  整个应用都有效  |
|   session   | 在当前会话中有效 |
|   request   | 在当前请求中有效 |
|    page     |  在当前页面有效  |

# 七、JSTL 标签库

## 1、什么是 JSTL 标签库

JSTL（Java server pages standarded tag library，即 JSP 标准标签库）JSTL 标签是基于 JSP页面的。这些标签可以插入在 JSP 代码中，本质上 JSTL 也是提前定义好的一组标签，这些标签封装了不同的功能，在页面上调用标签时，就等于调用了封装起来的功能。JSTL 的目标是使 JSP 页面的可读性更强、简化 JSP 页面的设计、实现了代码复用、提高效率。
在 JSP2.0 版本后开始支持 JSTL 标签库。在使用 JSTL 标签库时需要在 JSP 中添加对应的taglib 指令标签。

```
<%@ taglib prefix=“c” uri=“http://java.sun.com/jsp/jstl/core” %>
```

## 2、JSTL 标签分类

根据 JSTL 标签所提供的功能，可以将其分为 5 个类别。

## 1、核心标签


2、格式化标签



3、SQL标签


4、XML标签



5、JSTL标签

# 八、EL 表达式

## 1、什么是 EL 表达式

EL（Expression Language）是一种表达式语言。是为了使 JSP 写起来更加简单，减少 java代码，可以使得获取存储在 Java 对象中的数据变得非常简单。在 JSP2.0 版本后开始支持 EL表达式。

## 2、语法结构

```
${表达式}
${对象.属性名}
```

## 3、EL 表达式中的操作符

![image-20231124103226427](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124103226427.png)

## 4、EL 表达式的隐含对象

![image-20231124103245637](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124103245637.png)

## 5、使用 EL 表达式取出作用域中的值

```
${pageScope.name}
${requestScope.name}
${sessionScope.name}
${applicationScope.name}
```

获取作用域属性中的数据时，也可以只写属性名，EL 表达式会按照 pageScope、requestScope、sessionScope、applicationScope 的顺序查找该属性的值。

```
${name}
```

# 九、JSTL 标签库与 EL 表达式的使用

## 1、JSTL 标签库的使用步骤

1. 添加 jstl.jar 与 standard.jar

   ![image-20231124103432959](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124103432959.png)

2. 在 Idea 中添加 JSTL 标签的约束文件(DTD)

   ![image-20231124103453711](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124103453711.png)

3. 
   在 JSP 页面中添加 taglib 指令标签


```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

## 2、 JSTL 核心标签的使用

```
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

## 3、 <c:if>

**标签判断表达式的值，如果表达式的值为 true 则执行其主体内容。**

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>

<head>
    <title>Title</title>
</head>

<body>
        <c:if test="${1==1}">
            执行了
        </c:if>
</body>
</html>
```




4、<c:choose>, <c:when>, <c:otherwise>
<c:choose>标签与 Java switch 语句的功能一样，用于在众多选项中做出选择。
switch 语句中有 case，而<c:choose>标签中对应有<c:when>，switch 语句中有 default，而<c:choose>标签中有<c:otherwise>。

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>

<head>
    <title>Title</title>
</head>

<body>
<c:choose>
    <c:when test="${1==1}">
        when1执行了
    </c:when>
    <c:when test="${1==1}">
        when2执行了
    </c:when>
    <c:otherwise>
        otherwise执行了
    </c:otherwise>
</c:choose>
</body>
</html>
```

![image-20231124103645716](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124103645716.png)

## 5、<c:forEach>

迭代器，用于迭代集合。

![image-20231124103713426](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124103713426.png)

- varStatus 属性
- current: 当前这次迭代的（集合中的）项
- index: 当前这次迭代从 0 开始的迭代索引
- count: 当前这次迭代从 1 开始的迭代计数
- first: 用来表明当前这轮迭代是否为第一次迭代的标志
- last: 用来表明当前这轮迭代是否为最后一次迭代的标志
- begin: 属性值
- end: 属性值
- step: 属性值

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>

<head>
    <title>Title</title>
</head>

<body>
<c:forEach begin="0" end="9" step="2" varStatus="var">
    ForEach.... ${var.count},${var.first},${var.last},${var.current} <br/>
</c:forEach>
</body>
</html>
```

![image-20231124103746786](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124103746786.png)

## 6、使用 ForEach 迭代 List

需求：
创建 Users 对象，含有 userid，username 属性。
创建一个 Servlet，在 Servlet 中创建多个 Users 对象并放到 List 集合中，在 showUsers.jsp
的页面中显示所有的 Users对象信息。

### 1、创建 Users 对象，含有 userid，username 属性:

```java
//创建 Users 对象，含有 userid，username 属性。
public class Users {
    private Integer userid;
    private String username;

    public Users() {
    }
    
    public Users(Integer userid, String username) {
        this.userid = userid;
        this.username = username;
    }
    
    public Integer getUserid() {
        return userid;
    }
    
    public void setUserid(Integer userid) {
        this.userid = userid;
    }
    
    public String getUsername() {
        return username;
    }
    
    public void setUsername(String username) {
        this.username = username;
    }

}
```

### 2、创建一个 Servlet，在 Servlet 中创建多个 Users 对象并放到 List 集合中

```java
//创建一个 Servlet，在 Servlet 中创建多个 Users 对象并放到 List 集合中
@WebServlet("/findUser.do")
public class FindUsersServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
}

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        List<Users> list = new ArrayList<>();
        Users users1 = new Users(1,"kangkang");
        Users users2 = new Users(2,"Corey");
        list.add(users1);
        list.add(users2);
        req.setAttribute("list",list);
        req.getRequestDispatcher("showUsers.jsp").forward(req,resp);
    }

}
```

### 3、在 showUsers.jsp 的页面中显示所有的 Users对象信息。

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>

<head>
    <title>Title</title>
</head>

<body>
    <table border="1" align="center">
        <tr>
            <th>用户ID</th>
            <th>用户名</th>
        </tr>
        <c:forEach items="${list}" var="user">
            <tr>
                <td>${user.userid}</td>
                <td>${user.username}</td>
            </tr>
        </c:forEach>
    </table>
</body>
</html>
```


运行结果：

![image-20231124104024897](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124104024897.png)

## 7、使用 ForEach 迭代 Map

需求：
创建 Users 对象，含有 userid，username 属性。
创建一个 Servlet，在 Servlet 中创建多个 Users 对象并放到 Map 集合中，在 showUsers2.jsp
的页面中显示所有的 Users 对象的信息。

1、创建一个 Servlet，在 Servlet 中创建多个 Users 对象并放到 Map 集合中：

```java
//创建一个 Servlet，在 Servlet 中创建多个 Users 对象并放到 Map 集合中
@WebServlet("/findUser2.do")
public class FindUsers2Servlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        this.doPost(req, resp);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Map<String , Users> map = new HashMap<>();
        Users users1 = new Users(1,"kangkang");
        Users users2 = new Users(2,"Corey");
        map.put("users1",users1);
        map.put("users2",users2);
        req.setAttribute("map",map);
        req.getRequestDispatcher("showUsers2.jsp").forward(req,resp);
    }

}
```

### 2、在 showUsers2.jsp的页面中显示所有的 Users 对象的信息：

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>

<head>
    <title>Title</title>
</head>

<body>

<table border="1" align="center">
    <tr>
        <th>Map的key</th>
        <th>用户ID</th>
        <th>用户名</th>
    </tr>
    <c:forEach items="${map}" var="map">
        <tr>
            <td>${map.key}</td>
            <td>${map.value.userid}</td>
            <td>${map.value.username}</td>
        </tr>
    </c:forEach>
</table>

</body>
</html>
```


运行结果：

![image-20231124104204737](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124104204737.png)

# 十、JSTL 格式化标签的使用

```
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
```

**对日期的格式化处理**

```
<fmt:formatDate value="${data}" pattern=“yyyy-MM-dd”/>
```

**对数字的格式化处理**

```
<fmt:formatNumber value="${balance}" type=“currency”/>
```

```
@WebServlet("/format.do")
public class FormatServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.setAttribute("date",new Date());
        req.setAttribute("balance",2323234.236);
        req.getRequestDispatcher("format.jsp").forward(req,resp);
    }
}
```

```
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>
<html>

<head>
    <title>Title</title>
</head>

<body>
        <fmt:formatDate value="${date}" pattern="yyyy-MM-dd"/>
        <fmt:formatNumber value="${balance}" type="currency" />
</body>
</html>
```

# 十一、MVC 模式

## 1、什么是 MVC 模式

MVC 模式：Model、View、Controller 即模型、视图、控制器。是软件的一种架构模式（Architecture pattern）。MVC 要实现的目标是将软件的用户界面和业务逻辑分离，可提高代码可扩展性、可复用性、可维护性、以及灵活性。
View(视图)：用户的操作界面。如：html、jsp。
Model(模型)：具体的业务模型与数据模型。如：service、dao、pojo。
Controller(控制)：处理从视图层发送的请求，并选取模型层的业务模型完成响应的业务实现，并产生响应。如：Servlet。

![image-20231124104357862](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124104357862.png)

## 2、MVC 模式与应用程序分层的区别

MVC 模式是一种软件的架构方式，而应用程序分层这是一种代码的组织方式。MVC 模式与应用程序分层的目标都是一致的：为了解耦和、提高代码复用性。

![image-20231124104348027](C:\Users\22939\AppData\Roaming\Typora\typora-user-images\image-20231124104348027.png)