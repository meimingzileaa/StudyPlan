# This is my WorkNote

***

## 4月


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
