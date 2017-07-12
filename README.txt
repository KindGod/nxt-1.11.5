运行Nxt软件：

依赖关系：需要首先安装Java 8或更高版本。 Oracle JVM给出
更好的性能和更多的测试，但也支持OpenJDK。


使用安装程序：

提供了基于IzPack的安装包。点击相应的
jar / exe / dmg包，或者运行“java -jar nxt-client.jar”启动
安装程序。有关更多信息，请参阅https://bitbucket.org/JeanLucPicard/nxt/issues/283
关于IzPack安装程序的详细信息。安装后，使用快捷方式或
桌面图标启动Nxt服务器。


使用nxt-client.zip包：

打开nxt-client.zip包的包装，并在结果的nxt中打开一个shell
目录。如果使用Linux或BSD run.bat，请执行run.sh或start.sh脚本
如果使用Windows或run.command如果使用Mac。

在Unix上，run.sh脚本必须从安装目录中运行，
并使用此目录搜索配置文件，存储日志和for
nxt_db块链接数据库。 start.sh脚本可以从任何一个运行
目录，它在后台启动java进程，并使用〜/ .nxt
配置文件，日志和nxt_db数据库。不像run.sh，start.sh
使用桌面模式，创建桌面托盘图标并打开JavaFX UI
支持的。

初始化需要几秒钟。当它准备好了，你应该看到
控制台日志中的消息“Nxt server 1.x.x started successfully”。如果运行
桌面模式下，JavaFX窗口将自动打开。否则，打开一个
浏览器，不停止java进程，并转到http：// localhost：7876，
Nxt UI现在应该可用。

要停止应用程序，请在控制台窗口中键入Ctrl-C，或使用
stop.sh脚本，如果以start.sh开头。

警告：最好只使用拉丁字符，而不使用路径中的空格
到Nxt安装目录，因为可能会导致使用特殊字符
在权限中拒绝浏览器中的错误，这是一个已知的码头问题。


定制：

有许多可以更改的配置参数，但是默认值
设置为通常您可以在拆包后立即运行程序，
没有任何额外的配置。要查看有什么选项，请打开
conf / nxt-default.properties文件。列出所有可能的设置
详细说明。如果您决定更改任何设置，请勿编辑
nxt-default.properties直接，但创建一个新的conf / nxt.properties文件
并且只添加与默认值不同的属性
值。您不需要从nxt-default.properties中删除默认值
nxt.properties中的设置会覆盖nxt-default.properties中的设置。这条路，
升级软件时，您可以安全地覆盖nxt-default.properties
使用新包中的更新文件，而您的自定义仍然保留
在nxt.properties文件中安全。


如何贡献？

有很多方法为Nxt贡献。这里有些例子：

 *创建拉请求
 *审查拉请求
 *审查现有的代码
 *创建问题（又名特征想法，错误报告，文档等）
 *回答问题


技术细节：

Nxt软件是一个客户端 - 服务器应用程序。它由一个java服务器组成
进程，由run.sh脚本启动，一个javascript用户界面
在浏览器中运行JavaFX UI也可以自动启动
支持的配置。运行节点，伪造，更新块链，进行交互
与同行，只有java进程需要运行，所以你可以注销和
关闭浏览器，但保持java进程运行。如果你想保持
锻造时，请注意在注销时不要点击“停止锻造”。您可以
也只是关闭浏览器而不注销。

The java process communicates with peers on port 7874 tcp by default. If you are
behind a router or a firewall and want to have your node accept incoming peer
connections, you should setup port forwarding. The server will still work though
even if only outgoing connections are allowed, so opening this port is optional.

The user interface is available on port 7876. This port also accepts http API
requests which other Nxt client applications could use.

The blockchain is stored on disk using the H2 embedded database, inside the
nxt_db directory. When upgrading, you should not delete the old nxt_db
directory, upgrades always include code that can upgrade old database files to
the new version whenever needed. But there is no harm if you do delete the
nxt_db, except that it will take some extra time to download the blockchain
from scratch.

The default Nxt client does not store any wallet-type file on disk. Unlike
bitcoin, your password is the only thing you need to get access to your account,
and is the only piece of data you need to backup or remember. This also means
that anybody can get access to your account with only your password - so make
sure it is long and random. A weak password will result in your funds being
stolen immediately.

The java process logs its activities and error messages to the standard output
which you see in the console window, but also to a file nxt.log, which gets
overwritten at restart. In case of an error, the nxt.log file may contain
helpful information, so include its contents when submitting a bug report.

In addition to the default user interface at http://localhost:7876 , the
following urls are available:

http://localhost:7876/test - a list of all available http API requests, very
useful for client developers and for anyone who wants to execute commands
directly using the http interface without going through the browser UI.

http://localhost:7876/test?requestType=<specificRequestType> - same as above,
but only shows the form for the request type specified.

http://localhost:7876/doc - a javadoc documentation for client developers who
want to use the Java API directly instead of going through the http interface.


Compiling:

The source is included in the src subdirectory. To compile it on unix, just run
the enclosed compile.sh script. This will compile all java classes and put them
under the classes subdirectory, which is already in the classpath used by the
run.sh startup script. The compiled class files can optionally be packaged in a
nxt.jar file using the enclosed jar.sh script, and then nxt.jar should be
included in the classpath instead of the classes subdirectory.

