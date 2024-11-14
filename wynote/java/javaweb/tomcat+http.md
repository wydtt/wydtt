###### tomcat目录结构
![](images/tomcat目录结构.png)

###### tomcat常见错误
![](images/tomcat常见错误.png)

###### tomcat解压版安装&安全配置

![](images/tomcat安装&安全配置.png)
###### javaweb项目结构

根目录代表web项目的根

![](images/javaweb项目结构动态&静态.png)

###### eclipse手动搭建纯javaweb项目

![](images/eclipse手动搭建web项目.png)

###### eclipse 搜tomcat插件
可以启动，停止，重启tomcat，加上下面配置，用快捷键atl+t重启
![](images/eclipse-tomcat插件.png)

###### 部署web项目

告诉tomcat去部署指定路径的项目

在conf/server.xml文件最下面修改Context path

```xml
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
               prefix="localhost_access_log" suffix=".txt"
               pattern="%h %l %u %t &quot;%r&quot; %s %b" />
		
	<Context docBase="/home/slociv/Documents/learn/Java/webdemo/webapp" path="/pss"/>
      </Host>

```

![](images/tomcat部署web项目.png)


###### http协议

###### 请求消息
掌握mime 在tomcat安装webxml中查找
![](images/http-请求消息.png)

###### 响应消息

![](images/http-响应消息.png)

###### get和post请求的区别
![](images/get和post请求的区别.png)