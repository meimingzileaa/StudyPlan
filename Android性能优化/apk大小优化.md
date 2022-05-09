
## 为什么apk瘦身
1. 提高下载转化率
2. 减少rom占用
3. 优化运行时内存占用
4. 缩短apk安装时间

## Apk内部组成
1.内部组成
>1. 代码部分（classes.dex） --- java编译后的class文件打包
>2. 资源部分（res asserts resouces） --- xml layout color asset string array bool等
>3. so相关 --- lib目录下动态链接库
>4. 配置文件（meta-inf）--- MANIFEST.MF CERT.SF CERT.RSA

2.反编译工具
>1. apktool
>2. Analyze APK AndroidStudio自带

## 优化方向
1. 代码优化
> 1. 代码混淆 --> 瘦身 安全
> 2. R8优化
> 3. Redex处理  
     >   减少跨dex的冗余
> >1. 代码混淆 ：压缩 优化 混淆  
> >*  minifyEanabled -->混淆开启  
> >*  zipAlignEanabled --> 资源4字节对齐  
> >*  shrinkResources --> 移除无用resource资源  
> >*  Preguard-rules.pro --> 混淆配置文件  
> >2. keep --> 保持命令  
> >* AndroidManifest.xml引用的类。  
> >* JNI调用的方法。  
> >* 反射用到的类。  
> >* WebView中JavaScript使用的类。  
> >* Layout文件引用的自定义View。
> >3. 启用R8或ProGuard构建项目后会在模块下的build\outputs\mapping\release文件夹下输出下列文件：  
>>* dump.txt：说明 APK 中所有类文件的内部结构。  
>>* mapping.txt：提供原始与混淆过的类、方法和字段名称之间的转换。  
>>* seeds.txt：列出未进行混淆的类和成员。  
>>* usage.txt：列出从 APK 移除的代码。

2. 资源优化
> 1. png jpg压缩  选择适合的图片格式
> 2. 资源混淆
> 3. 资源分包
3. so优化
> 1. so最小化  多个平台的so cpu兼容性

***
更多好文：
* https://juejin.cn/post/7095565884122464292/