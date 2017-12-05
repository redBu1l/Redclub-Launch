
上节课，我们讲了如何使用burp抓取数据包，以及proxy的一些常用功能；这节课，我们主要学习`scanner`、`intruder`、`repeater`等等。

### intruder功能

标识符枚举用户名，ID和账户号码， 模糊测试SQL注入，跨站，目录遍历等等

首先，打开burp，并进入到proxy功能，可以看到“**target**”、“**positions**”、“**payloads**”、“**options**”标签

#### positions模块

* **Positions** - 选择攻击模式

* **sniper** - 对变量依次进行暴力破解。

* **battering ram** - 对变量同时进行破解。

* **pitchfork** - 每一个变量标记对应一个字典，一一对应进行破解。

* **cluster bomb** - 每个变量对应一个字典，并且进行交叉式破解，尝试各种组合。适用于用户名+密码的破解。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/1.png)
 
选择要进行暴力破解的参数，用$包含参数值，表示对该值进行枚举

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/2.png)
 
#### payloads模块

以简单模式为例，可选择对某个参数设置payload
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/3.png)

Payload类型可选择字典方式，爆破方式等等多总

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/4.png)
 
Payload进行编码、加密、截取等操作，例如暴力破解base64加密登录等等

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/5.png)
 
**Simple list** - 通过配置一个字符串列表作为Payload，也可以自定义添加或从加载文件夹，如下：
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/6.png)

**Runtime file** - 指定文件，作为相对应Payload位置上的Payload列表。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/7.png)
 
**Custom iterator** - 款功能强大的Payload，它共有8个占位，每一个占位可以指定简单列表的Payload类型，然后根据占位的多少，与每一个简单列表的Payload进行笛卡尔积，生成最终的Payload列表。
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/8.png)

#### options模块

**Request Engine**设置请求的线程数，超时重试时间
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/9.png)

**Grep Match** — 这个设置主要用来从响应包中提取某些结果，如果匹配成功，则在攻击结果中添加的新列中标明，便于排序和数据提取。比如说，在测试SQL注入漏洞，扫描包含“ODBC”，“错误”等消息，来识别可能存在注入漏洞的参数。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/10.png)
 
**Grep Extract** — 这些设置可用于提取响应消息中的有用信息。此选项是从返回包中提取有用的信息。例如，如果可通过ID的参数循环，可以提取每个文档寻找有趣的项目的页面标题。如果您发现返回的其他应用程序用户详细信息的功能，可以通过用户ID重复和检索有关用户管理帐户，忘记密码，邮箱等等。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/11.png) 

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/12.png)
 
**Grep Payloads** - 这些设置可用于提取响应消息中是否包含Payload的值，比如说，你想验证反射性的XSS脚本是否成功，可以通过此设置此项。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/13.png)
 
### scanner功能

在**Live Scanning**选项卡中，我们也可以对请求的域、路径、IP地址、端口、文件类型
进行控制，如下图：

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/14.png)
 
通过前几节的学习，我们已经知道Burp Scanner有主动扫描和被动扫描两个扫描方式，在
Options子选项卡中，主要是针对这两种扫描方式在实际扫描中的扫描动作进行设置。具体的

设置包含以下部分：

#### 攻击插入点设置（Attack Insertion Points）
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/15.png)

Burp Scanner在扫描中对请求数据包进行扫描，在每一个插入点构造测试语句，对参数值进行替换，从验证可能存在的安全漏洞。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/16.png)
 
#### 主动扫描（Active Scanning Engine）

主动扫描设置主要是用来设置控制主动扫描时的线程、失败重试间隔、失败重试次数、请求延迟等等。其中请求延迟设置（Throttle between requests）和其子选项延迟随机数 （Add random variations to throttle）在减少应用负荷，模拟人工测试，使得扫描更加隐蔽，而不易被网络安全设备检测出来。按自己的需求及配置情况设置线程数及延迟情况

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/17.png)
 
#### 主动扫描优化（Active Scanning Optimization）

此选项的设置主要是为了优化扫描的速度和准确率，尽量地提高扫描速度的同时降低漏洞的
误报率。 扫描速度（Scan speed）分三个选项，不同的选项对应于不同的扫描策略，当选择Thorough时，Burp会发送更多的请求，对漏洞的衍生类型会做更多的推导和验证。而当你选择Fast，Burp则只会做一般性的、简单的漏洞验证。
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/18.png)

#### 主动扫描范围设置（Active Scanning Areas）

在主动扫描过程中，根据扫描时间、重点等情况，选择不同的扫描范围。这里可选择的扫描范围有：SQL注入 -可以使不同的测试技术（基于错误，时间等），并且可按照特定数据库类型（MSSQL，Oracle和MySQL的）、反射式跨站点脚本、存储的跨站点脚本。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/19.png)
 
#### 被动扫描范围设置（Passive Scanning Areas）

因为被动扫描不会发送新的请求，只会对原有数据进行分析，其扫描范围主要是请求和应答消息中的如下参数或漏洞类型：`Headers`、`Forms`、`Links`、`Parameters`、`Cookies`、`MIME
type`、`Caching`、`敏感信息泄露`、`Frame框架点击劫持`、`ASP.NET ViewState`
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/20.png)

### repeater功能

通过修改请求包，查看服务器端响应情况。

在渗透测试过程中，我们经常使用Repeater来进行请求与响应的消息验证分析，比如修改请求参数，验证输入位置的漏洞；修改请求参数，验证逻辑越权；从拦截历史记录中对验证码，抓取进行重放。如下所示：

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/21.png)
 
其设置主要包括以下内容：

* **更新Content-Length** 这个选项是用于控制Burp是否自动更新请求消息头中的Content-Length

* **解压和压缩（Unpack gzip / deflate）** 这个选项主要用于控制Burp是否自动解压或压缩服务器端响应的内容

* **跳转控制（Follow redirections）** 这个选项主要用于控制Burp是否自动跟随服务器端作请求跳转，比如服务端返回状态码为302，是否跟着应答跳转到302指向的url地址。 它有4个选项，分别是永不跳转（Never），站内跳转（On-site only ）、目标域内跳转（Inscope
only）、始终跳转（Always），其中永不跳转、始终跳转比较好理解，站内跳转是指当前的同一站点内跳转；目标域跳转是指target scope中配置的域可以跳转；

* **跳转中处理Cookie（Process cookies in redirections）** 这个选项如果选中，则在跳转过程中设置的Cookie信息，将会被带到跳转指向的URL页面，可以进行提交。

* **视图控制（View）** 这个选项是用来控制Repeater的视图布局

* **其他操作（Action）** 通过子菜单方式，指向Burp的其他工具组件中。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/22.png)
 
### spider功能

爬取网站相关页面，通过HTML、js、提交的表单中的超链接、目录列表、注释，以及 robots.txt 文件。以树列表的形式详细的显示网站结构。在使用时要谨慎对有提交、删除等功能进行spider操作。
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/23.png)

### decoder功能

对左侧text中的值进行解密、加密、hash以text形式显示到下方，同样也可以进行显示hex值。

Burp Decoder的功能比较简单，作为Burp Suite中一款编码解码工具，它能对原始数据进行各种编码格式和散列的转换。其界面如下图，主要由输入域、输出域、编码解码选项三大部分组成。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/24.png)
 
同时，可对同一个值进行多次操作，如下

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/25.png)
 
### comparer功能

Burp Comparer在Burp Suite中主要提供一个可视化的差异比对功能，当服务器返回包过大时，可通过复制粘贴、加载文本方式添加对比，以words和bytes方式进行查看请求或数据包的不同，来查看服务器对某些请求的差异。例如：1.枚举用户名过程中，对比分析登陆成功和失败时，服务器状态的区别；2.使用 Intruder 进行攻击时，对于不同的服务器端响应，可以很快的分析出两次响应的区别在；3.进行SQL注入的盲注测试时，比较两次响应消息的差异，判断响应结果与注入条件的关联关系。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/26.png)
 
### extender功能

可通过商店添加某些插件，同样也可以添加自己或第三方的插件

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/27.png)
 
可添加java、Python、ruby类型的插件，若安装失败会提示异常情况
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/28.png)

同样burp提供了api接口，可创建自定义插件

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/29.png)
 
### 实战篇

#### Scanner实战
下面介绍几种对网站渗透时会用到的一些方法

在对系统做主动扫描时，当进行Burp Scanner。对下面的url进行扫描，如下：

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/30.png)
 
当我们在Burp Target 的站点地图上的某个URL执行`Actively scan this host`时，会自动弹出过滤设置

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/31.png)
 
优化扫描选项，我们可以对选项进行设置，指定哪些类型的文件不再扫描范围之内，如下：

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/32.png)
 
在这里，我们可以设置扫描时过滤某些类型，如：过滤js、css、图片等静态资源文件。
当我们点击【next】按钮，进入扫描路径分支的选择界面。如下图：

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/33.png)
 
以上是扫描开始前的一些相关设置，看个人需求进行设置，下面进入扫描阶段。
此时，在Scan queue队列界面，可以看到会显示扫描的进度、问题总数、请求数和错误统计等信息。

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/34.png)
 
同样，在Scan queue功能上，可以选中某个记录，在右击的弹出菜单中，对扫描进行控制。比如取消扫描、暂停扫描、恢复扫描、转发其他功能等等。如下：
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/35.png)

同时，在Results界面，自动显示队列中已经扫描完成的漏洞明细。
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/36.png)

#### intruder实战

登录框暴力破解

登录处不存在验证码和次数限制，首先我们会想到弱口令和暴力破解

下面我们看看如何对用户名和密码进行暴力破解

首先，我们尝试已知用户名，暴力破解密码，上一篇已经介绍了如何抓包，这里不在进行介绍。

##### 单个参数暴力破解

当我们将数据包发送到intruder功能时，会自动对某些参数标记 
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/37.png)

这里我们只对pass进行暴力破解，点击clear$清楚所有标记
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/38.png)

选择要进行暴力破解的参数值，点击add$，可以看到将pass参数选中，这里我们只对一个参数进行暴力破解，所以使用sniper即可

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/39.png)
 
下面我们选择要添加的字典

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/40.png)
 
同样也可以进行添加自己的字典，等等

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/41.png)
 
这里，我们选择自带的password字典进行暴力猜解
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/42.png)


由于字典有3000多条，不可能一条条获取，可以对status或length进行排序，可以看到找到了长度不一样的payload，说明很可能是要找的密码
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/43.png)

##### 多个参数暴力破解

同样，若用户名和密码都不知道，如何进行暴力破解

首先，按照上面的方式选中user和pass参数

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/44.png)
 
这里选择交叉式cluster bomb模式进行暴力破解，由于交叉式会进行n*m次所以这里只写几个payload进行演示
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/45.png)

首先，payload set选1,为第一个payload的值

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/46.png)
 
然后设置payload set为2，设置第二个值的payload，可以看到需要进行56次请求
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/47.png)

可以看到payload1、payload2的值均为test，猜解到正确的用户名密码
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/48.png)

我们可以看到存在登录框，但未不存在验证码和次数限制，首先我们会想到弱口令和暴力破解，同样payload参数有很多种方式数字、日期、自定义长度等等

##### Custom iterator方式生成字典

首先设置position1，为`aaa`

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/49.png)
 
设置position2为`$$$`
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/50.png)

设置position3为`passwords`

![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/51.png)
 
进行暴力破解时可以看到payload以`test`、`$$$`和`passwords`内容组成，可以方便我们对某些特定的类型进行暴力破解，例如邮箱`username@163.com`
 
![](https://raw.githubusercontent.com/redBu1l/Redclub-Launch/master/%E6%94%BB%E9%98%B2%E7%AC%AC%E5%85%AB%E8%8A%82/52.png)