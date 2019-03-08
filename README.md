### forked from  
[WrBug/FrenziedProguard](https://github.com/WrBug/FrenziedProguard/）
[RockyQu/ProguardDictionary](https://github.com/RockyQu/ProguardDictionary/）
合并了README说明及混淆字典配置文件


# 丧心病狂的Android混淆文件生成器


## 效果

混淆前

![](/1.png)

混淆后

![](/luyten.png)

![](/jd.png)

## 使用

### 获取混淆文件

#### 自己生成规则

使用intellij idea 打开 [proguard-creater](/proguard-creater) 工程
编辑 Main.java 根据提示填写相应参数运行即可


#### 使用已有规则

前往[proguard-file](/proguard-file) 下载对应的文件即可


### Android工程配置

    
1.  开启混淆
    
```
    
   buildTypes {
   release {
       minifyEnabled true
       proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
   }
}
    
```
2.  将混淆文件导入到 *proguard-rules.pro* 同一目录下
3. 编辑*proguard-rules.pro*,添加如下内容

```
# ----------------------------------------------------------------------------
# 混淆的压缩比例，0-7
-optimizationpasses 5
# 指定不去忽略非公共的库的类的成员
-dontskipnonpubliclibraryclassmembers
# 指定混淆是采用的算法
-optimizations !code/simplification/arithmetic,!code/simplification/cast,!field/*,!class/merging/*
# 指定外部模糊字典 proguard-chinese.txt 改为混淆文件名，下同
-obfuscationdictionary proguard-chinese.txt
# 指定class模糊字典
-classobfuscationdictionary proguard-chinese.txt
# 指定package模糊字典
-packageobfuscationdictionary proguard-chinese.txt

```

更多精彩内容请关注博客：[https://www.wrbug.com](https://www.wrbug.com)


# ProguardDictionary
混淆配置与字典文件

## Usage
把 proguard-dictionary.txt 文件放到 App Module 根目录下，将下面参数加入到 proguard-rules.pro 里
```
# 指定一个文本文件用来生成混淆后的名字。默认情况下，混淆后的名字一般为 a、b、c 这种。
# 通过使用配置的字典文件，可以使用一些非英文字符做为类名。成员变量名、方法名。字典文件中的空格，标点符号，重复的词，还有以'#'开头的行都会被忽略。
# 需要注意的是添加了字典并不会显著提高混淆的效果，只不过是更不利与人类的阅读。正常的编译器会自动处理他们，并且输出出来的jar包也可以轻易的换个字典再重新混淆一次。
# 最有用的做法一般是选择已经在类文件中存在的字符串做字典，这样可以稍微压缩包的体积。
# 查找了字典文件的格式：一行一个单词，空行忽略，重复忽略
-obfuscationdictionary proguard-dictionary.txt

# 指定一个混淆类名的字典，字典格式与 -obfuscationdictionary 相同
-classobfuscationdictionary proguard-dictionary.txt
# 指定一个混淆包名的字典，字典格式与 -obfuscationdictionary 相同
-packageobfuscationdictionary proguard-dictionary.txt
```

## Analyze APK
打包好的 APK 使用 Android Studio 的 Analyze APK 能够看到混淆后的结果
![](https://github.com/RockyQu/ProguardDictionary/blob/master/ImageFolder/proguard1.png "")

## Dictionary Rules
字典规则：一行一个单词，空行忽略，重复忽略  
你可以修改文件添加你自己的字典规则，甚至可以添加中文  
相关教程 [Android 混淆技术全面整理](https://rockycoder.cn/android/2018/03/15/Android-proguard-rules.html)
