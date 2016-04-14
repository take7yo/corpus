###JSP注释：
---
html注释，查看源码可看到内容：`<!— 注释语句[%=表达式%] -->`  
隐藏注释，查看源码看不到内容：`<%— 注释语句 --%>`

###JSP声明：
---
`<%! declaration; [declaration;] … %>`  
在一个JSP页面中可一次声明一个变量和方法，也可一次声明多个变量和方法，但是它们都只在当前页面中有效。

声明只在当前页面中有效，但是如果每个页面都用到一些相同的声明，可将它们写在一个单独的文件，然后用`<%@ include %>`或`<jsp:include>`元素包含进来。

声明不会在JSP页面内产生任何的输出，它的作用仅限于定义变量和方法，如果需要生成输出结果，可使用JSP表达式或脚本片段（Scriptlets）。

###JSP表达式
---
`<%= 表达式 %>`  
JSP表达式用来在JSP页面输出结果。  
表达式在运行后会被自动转换为字符串，然后插入到页面。

###JSP的3个编译指令
---
JSP的编译指令用于设置整个JSP页面相关的属性，比如页面的编码格式，所包含的文件等。

1. [page](#cpage)
2. [include](#cinclude)
3. [taglib](#ctaglib)

####[page指令](id:cpage)
page指令用于定义JSP页面中的全局属性，格式如下：

```
<%@ page
	[ language="java" ]
	[ extends="package.class" ]
	[ import="{package.class | package.*}, ..." ]
	[ session="true | false" ]
	[ buffer="none | 8kb | sizekb" ]
	[ autoFlush="true | false" ]
	[ isThreadSafe="true | false" ]
	[ info="text" ]
	[ errorPage="relativeURL" ]
	[ contentType="mimeType [ ;charset=characterSet ]" | "text/html; charset=ISO-8859-1" ]
	[ isErrorPage="true | false" ]
	[ pageEncoding="charset=characterSet | ISO-8859-1" ]
%>
```

| page指令属性   | 描述                                                  |
| :----------- | :---------------------------------------------------- |
| language     | 指定JSP脚本所采用的语言种类，目前仅支持Java，默认值为Java     |
| extends      | 定义当前JSP页面产生的Servlet继承哪个分类                   |
| import       | 定义当前JSP页面所使用的Java API，多个API之间用逗号分开       |
| session      | 指定当前JSP页面是否使用Session，默认值为true               |
| buffer       | 指定输出流缓存的大小，默认值为8kb                          |
| autoFlush    | 指定输出流缓冲区是否需要自动清除，默认值为true               |
| isThreadSafe | 指定当前JSP页面是否能处理多个线程的同步请求                  |
| info         | 指定当前JSP页面的相关信息                                 |
| errorPage    | 指定当前JSP页面发生错误时转向的错误页面                     |
| contentType  | 指定当前JSP页面mime类型的编码格式                          |
| isErrorPage  | 指定当前JSP页面是否为处理错误的页面                         |
| pageEncoding | 指定当前JSP页面编码的字符集，默认值为ISO-8859-1             |

page指令对整个页面有效，包括静态的包含文件，但page指令不能用于被动态包含的文件，例如使用<jsp:include>包含的文件。在一个JSP页面中可以使用多个page指令，但page指令中的属性只能出现一次（import属性除外）。

####[include指令](id:cinclude)
include指令用于在JSP页面中包含其他文件，语法格式如下：

```
<%@ include file="路径名" %>
```

include指令仅有一个属性file，其值为文件的相对路径。include指令包含的过程是静态的，包含的文件可以是JSP、HTML或者inc文件等。

####[taglib指令](id:ctaglib)
taglib指令允许用户使用标签库自定义新的标签，语法格式如下：

```
<%@ taglib uri="taglibURI" prefix="tabPrefix" %>
```

taglib指令中的uri属性用于根据标签的前缀对自定义的标签进行唯一的命名，其值可以是相对路径、绝对路径或标签库描述文件。属性prefix指定了标签的前缀。

###JSP的7个动作指令
---
JSP的动作指令和编译指令不同，编译指令用于设置整个JSP页面相关的属性，而动作指令则是用于运行脚本动作。

1. [jsp:include](#include)
2. [jsp:forward](#forward)
3. [jsp:useBean](#useBean)
4. [jsp:setProperty](#setProperty)
5. [jsp:getProperty](#getProperty)
6. [jsp:plugin](#plugin)
7. [jsp:param](#param)

####[jsp:include指令](id:include)
jsp:include指令用于在请求处理阶段包含来自一个Servlet或JSP页面的响应。和编译指令中的include指令不同，include指令只能包含静态页面，而jsp:include指令则可同时包含静态页面和动态页面。语法格式如下：

```
<jsp:include page="文件路径" />
```
或者：

```
<jsp:include page="文件路径">
	<jsp:param name="参数名1" value="参数值" />
	...
	<jsp:param name="参数名n" value="参数值" />
</jsp:include>
```
当不需要传递参数时，这两种使用的形式效果是一样的，如果要传递参数，就要使用第二种形式。

####[jsp:forward指令](id:forward)
jsp:forward指令用于执行页面转向，将请求的处理转发到下一页面。语法格式如下：

```
<jsp:forward page="文件路径" />
```
或者：

```
<jsp:forward page="文件路径">
	<jsp:param name="参数名1" value="参数值" />
	...
	<jsp:param name="参数名n" value="参数值" />
</jsp:forward>
```
如果要转向的页面为一个动态网页，则可使用第二种形式来传递参数。

####[jsp:useBean指令](id:useBean)
jsp:useBean指令用来在JSP页面内创建一个JavaBean实例。语法格式如下：

```
<jsp:useBean id="JavaBean的名称" scope="有效范围" class="包名.类名"></jsp:useBean>
```
其中id属性指定了JavaBean的名称，只要是在它的有效范围内，均可使用这个名称来调用它。scope属性为JavaBean的有效范围，它可接受4个值：request、session、page、application。scope属性的默认值为page。class属性指定了JavaBean所归属的类，如果类属于某个包，则类名的前面要加上包名。

####[jsp:setProperty指令](id:setProperty)
jsp:setProperty指令用来设置Bean属性值。语法格式如下：

```
<jps:setProperty name="JavaBean实例名"  property="*"/>
```
该形式是设置Bean属性的快捷方式。在Bean中属性的名字，类型必须和request对象中的参数名称相匹配。由于表单中传过来的数据类型都是String类型的，JSP内在机制会把这些参数转化成Bean属性对应的类型。  
`property="*"`表示所有名字和Bean属性名字匹配的请求参数都将被传递给相应的属性set方法。 

或：

```
<jsp:setProperty name="JavaBean实例名" property="属性名称" />
```
使用request对象中的一个参数值来指定Bean中的一个属性值。在这个语法中，property指定Bean的属性名，而且Bean属性和request参数的名字应相同。也就是说，如果在Bean中有setUserName(String userName)方法，那么，property的值就是"userName".这种形式灵活性较强,可以有选择的对Bean中的属性赋值。

或：

```
<jsp:setProperty name="JavaBean实例名" property="属性名称" param="参数名称" />
```
param指定用哪个请求参数作为Bean属性的值。Bean属性和request参数的名字可以不同。如果当前请求没有参数，则什么事情也不做，系统不会把null传递给Bean属性的set方法。因此，你可以让Bean自己提供默认属性值，只有当请求参数明确指定了新值时才修改默认属性值。

或：

```
<jsp:setProperty name="JavaBean实例名" property="属性名称" value="属性值" />
```
value用来指定Bean属性的值。字符串数据会在目标类中通过标准的valueOf方法自动转换成数字、boolean、Boolean、byte、Byte、char、Character。例如，boolean和Boolean类型的属性值（比如“true”）通过Boolean.valueOf转换，int和Integer类型的属性值（比如“42”）通过Integer.valueOf转换。

当property值为*时，表示保存用户在JSP输入的所有值，用于匹配Bean中的属性。  
当property有具体的值时，表示匹配的一个Bean的属性。  
param属性表示根据指定的request对象中的参数与属性匹配。  
value属性表示使用指定的值来设置属性。

####[jsp:getProperty指令](id:getProperty)
jsp:getProperty指令用来读取Bean的属性值，并将其转换为一个字符串在页面上输出。语法格式如下：

```
<jsp:getProperty name="JavaBean实例名" property="属性名称" />
```

####[jsp:plugin指令](id:plugin)
jsp:plugin指令用于下载服务器端的JavaBean或Applet到客户端执行。语法格式如下：

```
<jsp:plugin
	type="bean | applet"
	code="classFileName"
	codebase="classFileDirectoryName"
	[ name="instanceName" ]
	[ archive="URIToArchive, ..." ]
	[ align="bottom | top | middle | left | right" ]
	[ height="displayPixels" ]
	[ width="displayPixels" ]
	[ hspace="leftRightPixels" ]
	[ vspace="topBottomPixels" ]
	[ jreversion="JREVersionNumber | 1.1" ]
	[ nspluginurl="URLToPlugin" ]
	[ iepluginurl="URLToPlugin" ]>
	[ <jsp:params>
		[ <jsp:param name="parameterName" value="{parameterValue | <%= expression %>}" /> ]
	</jsp:params> ]+
	[ <jsp:fallback> text message for user </jsp:fallback> ]
</jsp:plugin>
```
例子

```
<jsp:plugin type=applet code="Molecule.class" codebase="/html">
	<jsp:params>
		<jsp:param name="molecule" value="molecules/benzene.mol" />
	</jsp:params>
	<jsp:fallback>
		<p>Unable to load applet</p>
	</jsp:fallback>
</jsp:plugin>
```

**描述**

<jsp:plugin>元素用于在浏览器中播放或显示一个对象（典型的就是Applet和Bean),而这种显示需要在浏览器的java插件。

当JSP文件被编译，送往浏览器时，<jsp:plugin>元素将会根据浏览器的版本替换成`<object>`或者`<embed>`元素。注意，`<object>`用于HTML4.0，`<embed>`用于HTML3.2。

一般来说，<jsp:plugin>元素会指定对象是Applet还是Bean,同样也会指定class的名字，还有位置，另外还会指定将从哪里下载这个Java插件。具体如下:

**属性**

* type="bean | applet"  
	将被执行的插件对象的类型，你必须得指定这个是Bean还是Applet，因为这个属性没有缺省值。
* code="classFileName"  
	将会被Java插件执行的Java Class的名字，必须以.class结尾。这个文件必须存在于codebase属性指定的目录中。
* codebase="classFileDirectoryName"  
	将会被执行的Java Class文件的目录（或者是路径)，如果你没有提供此属性，那么使用<jsp:plugin>的JSP文件的目录将会被使用。
* name="instanceName"  
	这个Bean或applet实例的名字，它将会在Jsp其它的地方调用。
* archive="URIToArchive, ..."  
	一些由逗号分开的路径名，这些路径名用于预装一些将要使用的class，这会提高applet的性能。
* align="bottom | top | middle | left | right"  
	图形，对象，Applet的位置，有以下值：
	- bottom
	- top  
	- middle  
	- left  
	- right  
* height="displayPixels" width="displayPixels"  
	Applet或Bean将要显示的长宽的值，此值为数字，单位为象素。
* hspace="leftRightPixels" vspace="topBottomPixels"  
	Applet或Bean显示时在屏幕左右，上下所需留下的空间，单位为象素。
* jreversion="JREVersionNumber | 1.1"  
	Applet或Bean运行所需的Java Runtime Environment (JRE) 的版本。缺省值是1.1。
* nspluginurl="URLToPlugin"  
	Netscape Navigator用户能够使用的JRE的下载地址，此值为一个标准的URL，如http://www.aspcn.com/jsp
* iepluginurl="URLToPlugin"  
	IE用户能够使用的JRE的下载地址，此值为一个标准的URL，如http://www.aspcn.com/jsp
* <jsp:params> [ <jsp:param name="parameterName" value="{parameterValue | <%= expression %>}" /> ]+ </jsp:params>  
	你需要向Applet或Bean传送的参数或参数值。
* <jsp:fallback> text message for user </jsp:fallback>  
	一段文字，用于Java插件不能启动时显示给用户的，如果插件能够启动而Applet或Bean不能，那么浏览器会有一个出错信息弹出。

####[jsp:param指令](id:param)
jsp:param指令用于设置参数值，它不能单独使用，主要用在jsp:include指令、jsp:forward指令和jsp:plugin指令中。

###JSP的9个内置对象
---
内置对象指不需要预先定义就可以在JSP页面中直接使用的对象。JSP共提供了9个内置对象。

1. [request](#request)
2. [response](#response)
3. [session](#session)
4. [out](#out)
5. [page](#page)
6. [application](#application)
7. [pageContext](#pageContext)
8. [config](#config)
9. [exception](#exception)

####[request对象](id:request)
request对象用于获取客户端提交的数据，这些数据包括头信息、客户端地址、请求方式等。

######request对象的常用方法
| 方法名                      | 描述                               |
| :------------------------- | :--------------------------------- |
| getParameter(String name)  | 获取表单提交的数据                    |
| getParameters()            | 获取客户端提交的所有参数名             |
| getAttribute(String name)  | 获取name指定的属性名                 |
| getAttributes()            | 获取request对象所有属性的名称集合      |
| getSession(Boolean create) | 获取HttpSession对象                 |
| getCookies()               | 获取Cookie对象                      |
| getProtocol()              | 获取客户使用的协议名称                |
| getServletPath()           | 获取客户端请求的脚本的相对路径          |
| getMethod()                | 获取客户端提交数据的方式，如GET、POST等 |
| getHeader()                | 获取文件头信息                       |
| getRemoteAddr()            | 获取客户端的IP地址                   |
| getServerName()            | 获取服务器名称                       |
| getRemoteHost()            | 获取客户端主机的名称                  |
| getServerPort()            | 获取服务端的端口号                    |

####[response对象](id:response)
response对象用于对客户端的请求作出动态的响应，向客户端发送数据。

######response对象的常用方法
| 方法名                         | 描述                          |
| :---------------------------- | :--------------------------- |
| getCharacterEncoding()        | 返回响应用的字符编码格式         |
| getOutputStream()             | 返回响应的输出流                |
| getWriter()                   | 返回可以向客户端输出字符的一个对象 |
| setContentLength(int length)  | 设置响应头的长度                |
| setContentType(String type)   | 设置响应的mime类型              |
| sendRedirect(String location) | 重新定向客户端的请求             |
| flushBuffer()                 | 强致把当前缓冲区的数据发送到客户端 |
| addCookie(Cookie cookie)      | 在客户端添加一个Cookie          |

####[session对象](id:session)
从一个客户打开浏览器并连接到服务器开始，到客户关闭浏览器离开这个服务器结束，整个阶段被称为会话。session对象可用来保存用户的会话信息和会话状态。

######session对象的常用方法
| 方法名                                | 描述                          |
| :----------------------------------- | :--------------------------- |
| getId()                              | 获取session的标识符            |
| setAttribute(String key, Object obj) | 将参数Object指定的对象obj添加到session对象中，并为添加的对象指定一个索引值 |
| getAttribute(String key)             | 获取session对象中含有关键字的对象 |
| isNew()                              | 判断用户是否参与了会话           |
| invalidate()                         | 是当前会话失效                  |
| removeAttribute(string name)         | 删除一个指定session的值         |
| getCreationTime()                    | 获取session对象创建的时间        |

####[out对象](id:out)
out对象用来向客户端输出各种数据。

######out对象的常用方法
| 方法名             | 描述                                 |
| :---------------- | :---------------------------------- |
| print()/println() | 输出各种类型数据                       |
| clearBuffer()     | 清除缓冲区的数据，并将数据写入客户端      |
| clear()           | 清除缓冲区的当前内容，但不将数据写入客户端 |
| flush()           | 输出缓冲区中的数据                     |
| newLine()         | 输出一个换行符号                       |
| close()           | 关闭输出流                            |

####[page对象](id:page)
page对象就是指当前JSP页面本身，类似于Java中的this。

######page对象的常用方法
| 方法名              | 描述                           |
| :----------------- | :---------------------------- |
| getClass()         | 获取page对象的类                |
| hashCode()         | 获取page对象的hash码            |
| equals(Object obj) | 判断page对象是否与参数中的obj相等 |
| copy(Object obj)   | 复制page对象到指定的Object对象中 |
| clone()            | 克隆当前的page对象              |
| toString()         | 把page对象转换成String类型的对象 |

####[application对象](id:application)
application对象实现了用户间数据的共享，可存放全局变量。

######application对象的常用方法
| 方法名                                | 描述                                  |
| :----------------------------------- | :----------------------------------- |
| setAttribute(String key, Object obj) | 将参数Object指定的对象obj添加到application对象中，并为添加的对象指定一个索引值 |
| getAttribute(String name)            | 获取指定的属性值                        |
| getAttributeNames()                  | 获取一个包含所有可用属性名的枚举           |
| removeAttribute(String name)         | 删除一个指定application的值             |
| getContext(String uripath)           | 获取指定WebApplication的application对象 |
| getResource(String path)             | 获取指定资源（文件及目录）的URL路径        |
| getResourceAsStream(String path)     | 获取指定资源的输入流                     |
| getServlet(String name)              | 返回指定的Servlet                      |
| log(String msg)                      | 把指定消息写入Session的日志文件          |

####[pageContext对象](id:pageContext)
pageContext对象用于管理对属于JSP中特殊可见部分中已经命名对象的访问。

######pageContext对象的常用方法
| 方法名                                       | 描述                           |
| :------------------------------------------ | :---------------------------- |
| setAttribute(String name, Object attribute) | 设置默认页面范围或特定对象范围之中的已命名对象 |
| getAttribute(String name[, int scope])      | 获取一个已命名为name的对象的属性，可选参数scope表示在特定范围内 |
| removeAttribute(String name[, int scope])   | 删除指定范围内的某个属性          |
| forward(String relativeUrlPath)             | 将当前页面重定向到其他的页面       |
| include(String relativeUrlPath)             | 在当前位置包含另一文件            |
| release()                                   | 释放pageContext对象所占用的资源   |
| getServletContext()                         | 获取当前页面的ServletContext对象 |
| getException()                              | 获取当前页的Exception对象        |

####[config对象](id:config)
config对象用来获取服务器初始化配置参数。

######config对象的常用方法
| 方法名                         | 描述                  |
| :---------------------------- | :------------------- |
| getServletContext()           | 获取当前的Servlet上下文 |
| getInitParameter(String name) | 获取指定的初始参数的值   |
| getInitParameterNames()       | 获取所有的初始参数的值   |
| getServletName()              | 获取当前的Servlet名称   |

####[exception对象](id:exception)
exception对象用于处理JSP页面中发生的错误和异常，可以帮助我们了解并处理页面中的错误信息。

######exception对象的常用方法
| 方法名                 | 描述                     |
| :-------------------- | :---------------------- |
| getMessage()          | 获取当前的错误信息         |
| getLocalizedMessage() | 获取本地化语言的异常错误    |
| printStackTrace()     | 输出一个错误和错误的堆栈跟踪 |
| fillInStackTrace()    | 重写异常的执行栈轨迹        |
| toString()            | 关于异常错误的简单信息描述   |

**PS：** exception对象只能在错误页面中使用。即：在使用exception对象的页面中将page指令的`isErrorPage`属性设置为`true`。例如：`<%@page isErrorPage="true"%>`










