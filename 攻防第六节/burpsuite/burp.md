### burp简介

**Burp Suite**是Web应用程序测试的最佳工具之一，可以对请求的数据包进行拦截和修改,扫描常见的web安全漏洞，暴力破解登录表单、遍历数据等等。

### Burp所需环境

Burp Suite是Java编写的，所以在使用前需要安装Jdk环境，这里不进行具体讲解如何安装jdk,安装完成后将jdk相关目录添加到环境变量中。

### 主要功能

首先，我们看下burp都有哪些功能，并且都是用来做什么的。

* **proxy** – Burp Suite设置代理，抓取数据包。

* **Spider** – Burp Suite的蜘蛛功能是用来抓取Web应用程序的链接和内容等。

* **Scanner** – 是用来扫描Web应用程序漏洞的，可以发现常见的web安全漏洞，但会存在误报的可能。

* **Intruder** – 可进行Web应用程序模糊测试,进行暴力猜解等。

* **Repeater** – 对数据包进行重放，可分析服务器返回情况，判断修改参数的影响。

* **Sequencer** – 用来检查Web应用程序提供的会话令牌的随机性.并执行各种测试。

* **Decoder** – 对数据进行加解密操作，包含url、html、base64等等。

* **Comparer** – 此功能用来执行任意的两个请求,响应或任何其它形式的数据之间的比较。

* **extender** - 加载Burp Suite的扩展，使用你自己的或第三方代码来扩展Burp Suite的功能。

* **options** - 设置burp，字体，编码等等

* **alerts** - 是用来存放报错信息的，用来解决错误

### 功能介绍

本次我们主要学习如何使用burp抓取数据包的proxy功能。

首先，打开burp，并进入到proxy功能，可以看到`options`、`Histroy`、`intercept`、`websockets history`标签。

#### Intercept模块

**Intercept** - 控制抓取到的数据包，并可将数据包放行或舍弃，以及发送到其他功能中。

tutututututut

**Intercept**相关功能

* **Forward** - 将抓取或修改后的数据包发送到服务器端

* **Drop** - 丢弃抓取到的数据包，不与服务器端进行交互该数据包

* **Interceptionis on/off** - 是否拦截数据包，on表示拦截，off表示放行

tututututut

* **Action** - 可对该数据包做哪些操作，同样数据包处右击和action效果相同

tututututut

* **Commentfield** - 为请求包或响应包设置注释，并可选择相应的颜色，更容易在history中查找到

tutututu

* **？** - 查看帮助信息。可通过帮助信息查看功能的使用

tutututututu
 
同样，burp有四种消息类型显示数据包

**Raw** - 以纯文本形式显示数据包

tutututut

**Params** - 包含参数URL 查询字符串、cookies的请求，并可双机该请求进行修改 

tututututu

**Headers** - 以名称、值的形式显示获取的数据包。

tutututut

**Hex** - 可编辑数据包的二进制数据，在进行00截断时非常好用。

tutututut

同样，burp具有搜索功能，可以搜索当前数据包中你想要的内容，并且会显示符合内容的个数以及位置

tututututut

#### histroy模块

**Histroy** - 记录设置代理后浏览器访问的页面数据包，详细记录数据包的host、method、url、status、extension等等

tututututut

当我们选中某个请求时，可以看他的请求包信息，同样也可查看他的响应包信息

tututututut

请求数据包

tutututututut

同样，可以双机某个数据包即可打开详情,通过`Previous/next`功能切换到其他数据包，同时，也可将该数据包发送到其他功能模块当中，方便我们的使用

tutututututut

如果认为某个数据包比较重要，可将当前数据包设置某个醒目的颜色以提示他的重要性

tututututut

该模块下存在`filter`功能，有许多模块存在该功能，可使用该功能将认为无用的数据包隐藏，把需要的数据包显示到当前状态下。

点击filter功能会出现该功能的配置选项。

tutututututututututut

可以按照请求类型，请求的状态，mime类型、搜索关键字，文件后缀、监听的端口等等，按个人需求去缩小需要的范围

tututututututututut
 
#### options模块

**options** - 该选项主要用于设置代理监听、请求和响应，拦截反应等等。

**Proxy Listeners** - 设置监听

tututututututu

可以添加回环地址、所有的接口、具体的某个ip的地址

tutututututu

**Intercept Client Requests** - 配置拦截规则，设置拦截数据包的匹配规则。
规则可以是域名、IP、协议、HTTP方法、URL等等

tutututut

**Intercept Server Responses** - 配置拦截规则，设置拦截的匹配规则，基于服务器端的返回情况进行匹配

tututututtu
 
还有很多功能介绍proxy，我们会在以后的文章中结合具体的实例去讲解，这里只进行常用的某些功能进行介绍。

### 实战篇

#### burp代理设置

首先我们需要设置burp代理，这里我们将端口设置为8888

tutututututut
 
同时需要选中该复选框

tutututututut
 
#### 浏览器代理设置

##### 方法一

这里以chrome为例，选择“设置”

tututututut

找到“代理设置”
 
tututututututt

选择“连接”中的“局域网”

tututututut
 
设置代理地址和端口，要和burp的地址端口相同

tututututut
 
访问浏览器可抓取到数据包

tututututututut
 
##### 方法二

使用浏览器扩展代理工具，避免每次到设置中查找该工具。

tututututut
 
选择设置的代理

tututututu
 
#### 抓取数据包

tututututututut 

同样，可以在history中查看某些数据，当访问的数据包较多时，但我们只需要某些特征时，可进行筛选

tutututututututut

#### 筛选数据包

看到既有php,也有js的数据，我们可能只想看php的，可以在filter中选择隐藏某些后缀

tututututut
 
同样，可以设置只显示php、asp、jsp等后缀
 
tututututut

也可以选择某些特定状态的数据包，例如：status为200等等
 
tututututututtu
