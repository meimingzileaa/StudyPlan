# This is my WorkNote

***
## 8月
**0818**
1 manifest 合并冲突解决 mergemanifest 按钮可以查看
2 android 单测使用andriod 包内容需要增加RobolectricTestRunner （bundle 失效）
3 contentProvider acquireUnstableContentProviderClient 接口
4 Flow 流的了解

***
## 7月
**0718**
1 同名Provider 安装冲突
（1） 两个apk 引入相同的 module 安装冲突
（2） 查看报错 provider
（3） provider 使用了固定名称
（4） 多思考义下leakcanary怎么处理的？ provider名称与包名相关设计

***
## 6月

**0617**
1 String StringBuffer Stringbuilder  
String 不可变类 每次改变都会新生成一个对象  
StringBuffer则是可变类，任何对它所指代的字符串的改变都不会产生新的对象 线程安全  
Stringbuilder是可变类 线程不安全



**0616**
1 CountDownLatch  
https://www.jianshu.com/p/128476015902  
使用场景：某个线程等待其他线程程返回结果时。
CountDownLatch主要有两个方法：countDown()和await()。countDown()方法用于使计数器减一，其一般是执行任务的线程调用，await()方法则使调用该方法的线程处于等待状态，其一般是主线程调用。

2 Gradle依赖配置compile，implementation和api的区别   
api
当其他模块依赖于此模块时，此模块使用api声明的依赖包是可以被其他模块使用  
implementation  
当其他模块依赖此模块时，此模块使用implementation声明的依赖包只限于模块内部使用，不允许其他模块使用。  
compileOnly  
依赖会添加到编译路径中，但是不会打包到apk中，因此只能在编译时访问，且compileOnly修饰的依赖不会传递。  
runtimeOnly  
与compileOnly相反，它修饰的依赖不会添加到编译路径中，但是被打包到apk中，运行时使用。没有使用过。
annotationProcessor  
用于注解处理器的依赖配置。  
testCompile  
只在单元测试代码的编译以及最终打包测试apk时有效。  
debugCompile  
只在 debug 模式的编译和最终的 debug apk 打包时有效。  
Release compile  
仅仅针对 Release 模式的编译和最终的 Release apk 打包。  

3 DiskLruCache  磁盘缓存   
三级缓存
内存缓存
磁盘缓存
网络存储
  
4 Grpc  
gRPC 是 Google 开源的一个高性能的 RPC(Remote Procedure Call) 框架，它具有如下的优点：  
提供高效的进程间通信。gRPC 没有使用 XML 或者 JSON 这种文本格式，而是采用了基于 protocol buffers 的二进制协议；同时，gRPC 采用了 HTTP/2 做为通信协议，从而能够快速的处理进程间通信。  
简单且良好的服务接口和模式。gRPC 为程序开发提供了一种契约优先的方式，必须首先定义服务接口，才能处理实现细节。  
支持多语言。gRPC 是语言中立的，我们可以选择任意一种编程语言，都能够与 gRPC 客户端或者服务端进行交互。  
成熟并且已被广泛使用。通过在 Google 的大量实战测试，gRPC 已经发展成熟。   


**0606**    
1 ASM
是一个字节码操作库，它可以直接修改已经存在的class文件或者生成class文件。ASM提供了一些便捷的功能来操作字节码内容。

2 访问者模式

3 内存基础

***
## 5月

**0519**

**0518**
1 父类指向子类，会优先调用子类方法。

    open class father{
        open fun print(){
            Log.e("=====>father", "father")
        }
    }
    class son: father() {
        override fun print(){
            Log.e("=====>son", "son")
        }
    }
    private fun Test() {
        var p: father? = null
        p = son()
        p.print()
    }
    输出 ： Son

2  Collections.synchronizedMap 可以使map同步     
3  kotlin 扩展函数优先于原有函数 
## 4月


**0424**
Gradle构建 groovy语法
任务依赖
Activity onNewIntent

**0413**  
Hilt 依赖注入  
一些注解的含义  
快应用进程启动原理  
Activity启动模式



***
**0412**

Android 进程

> 1. Android进程实际上是Linux(类UNIX系统)进程，在Linux中所有的进程都是init进程的子孙进程，也就是说，所有的进程都是直接或者间接地由init进程fork出来的。
> 2. 默认情况下，同一应用的所有组件均在相同的进程中运行，且大多数应用都不会改变这一点。
> 3. android:process可以控制组件运行在不同进程中:
>    * 第一种形式如 android:process=":remote"，以冒号开头，冒号后面的字符串原则上是可以随意指定的。如果我们的包名为“com.example.processtest”，则实际的进程名为“com.example.processtest:remote”。
>      这种设置形式表示该进程为当前应用的私有进程，其他应用的组件不可以和它跑在同一个进程中。
>    * 第二种情况如 android:process="com.example.processtest.remote"，以小写字母开头，表示运行在一个以这个名字命名的全局进程中，其他应用通过设置相同的ShareUID可以和它跑在同一个进程。
> 4. 进程生命周期:https://developer.android.com/guide/components/activities/process-lifecycle
>    * 前台进程
>    * 可见进程
>    * 服务进程
>    * 缓存进程
> 5. 进程信息获取命令adb shell ps
>    android获取进程id： android.os.Process.myPid()
>    杀死进程： killProcess(pid)

[多进程会造成的问题](https://blog.csdn.net/u010844304/article/details/116789180?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-1.pc_relevant_default&spm=1001.2101.3001.4242.2&utm_relevant_index=4)

> 1. Android 为每一个进程分配一个独立的虚拟机，不同虚拟机在内存分配上有不同的地址空间，这就导致多进程下访问同一个类的对象会产生多分副本。所以在一个
>    进程中修改某个值，只会在当前进程有效，对其他进程不会造成任何影响。
> 2. 线程同步失效。
>    因为多进程的内存地址空间不同，锁的不是同一个对象，所以不管是锁对象还是锁全局对象都无法保证线程同步。
> 3. SharedPreference的可靠性下降。
>    因为SharedPrefercences底层通过读写xml实现，并发读写显示不是安全的操作，甚至会出现数据错乱。
> 4. Application会多次创建。
>    默认情况下，应用拥有一个主进程。组件被指定新进程之后，系统在启动这个组件的时候，是先创建这个进程，再创建该组件。打印出进程名称办法：重载Application类的onCreate方法即可

内存名词：

> VSS - Virtual Set Size 虚拟耗用内存（包含共享库占用的内存）
> RSS - Resident Set Size 实际使用物理内存（包含共享库占用的内存）
> PSS - Proportional Set Size 实际使用的物理内存（比例分配共享库占用的内存）
> USS - Unique Set Size 进程独自占用的物理内存（不包含共享库占用的内存）
> 大小规律：
> 一般来说内存占用大小有如下规律：VSS >= RSS >= PSS >= USS

Pid Uid

> * UID：一般理解为User Identifier,UID在linux中就是用户的ID，表明时哪个用户运行了这个程序，主要用于权限的管理。
>   Linux的uid是针对多用户操作系统中用于区分用户。
>   an系统中1999>uid>10000这个整数范围中的id号代表用户app的uid，同时gid是和uid对齐。 ps命令行的输出中有一列USER，代表的就是UID，如下图：
>   ![img.png](img.png)
>   app的uid/100000计算为userid为u0
>   app的uid减去10000为axx。
>   例如某个app的uid是10022，则uid字串就是u0_a22
> * PID：为Process Identifier，　PID就是各进程的身份标识,程序一运行系统就会自动分配给进程一个独一无二的PID。
