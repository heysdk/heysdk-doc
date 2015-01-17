anysdk-like
===========

**AnySDK**是**触控**出品的**手游SDK打包工具**，手游研发商只需要接入**AnySDK**，即可后台打包所有SDK，它是怎么做到的呢？

其实，对android熟悉的同学都应该知道，apk文件其实就是一个zip包，网上也有很多汉化或者美化教程，都是直接修改apk包来实现的，接入**AnySDK**后，其实就是在自己的apk和最终apk之间加了一个通用层，再加上java代码解开后都还是按class分开的，这样很容易做到不需要源代码，直接通过修改apk里面的资源和class文件来实现出不同渠道APK的版本。

以前**umeng**还出过一个专门修改渠道id的apk打包工具，其实也是一样的原理，不过现在新版好像把这件事直接交给gradle了，说是google换了新的打包方式，不过就我们使用的apktool来看，其实影响不大，依然可以正常使用，当然，具体原因没太研究。

我们来一步步的简单的手动实现一个换包的例子吧。

首先，我们拿最新的**cocos2dx**为例子，建立一个**cocos2dx**项目，简单一点，给cpp的吧

然后加入自己的SDK框架类，就叫**HeySDK**吧，代码如下：

    package com.heysdk.lib;

    import android.content.Context;

    public class HeySDK {
     public static Context mContext;
 
     public static void init(Context context) {
      mContext = context;
     }
 
     // 自动登陆，在游戏加载界面调用即可
     public static void autologin() {
     }
    }

在主activity里面，加入初始化代码

    protected void onCreate(Bundle savedInstanceState){
      super.onCreate(savedInstanceState);
 
      HeySDK.init(this);
     }

java代码就这样了，接下来改c++代码吧，因为是例子，我们就简单一点，在 `HelloWorldScene.cpp` 里面加一个简单的函数，调用刚写的java代码吧，记住最好加上androud的环境检查。

添加一个include

    #include "platform/android/jni/JniHelper.h"

然后添加autologin函数

    static int autologin()
    {
     cocos2d::JniMethodInfo minfo;
     bool isHave = cocos2d::JniHelper::getStaticMethodInfo(minfo, "com.heysdk.lib.HeySDK", "autologin", "()V");
     if(isHave)
     {
      minfo.env->CallStaticObjectMethod(minfo.classID, minfo.methodID);
     }
    }

最后在 `HelloWorld::init()` 最后返回true以前，加上自动登陆的调用。

    autologin();

实现一个 `autologin` 函数，简单一点，我们先出一个什么都不做的版本，然后出一个apk包，我们叫它 src 吧。

再对接一个sdk，我们这里拿快玩做例子，所以接入一下快玩，然后再出一个包，我们叫它 kuaiwan 好了。

2个包都出好以后，先去 `http://code.google.com/p/android-apktool/` 下载一个最新的apktool，一般建议下载最新的jar即可，最新版对新的SDK打包支持得更好，现在是2.0RC3。

    java -jar apktool_2.0.0rc3.jar d heysdkdemo-cc2.apk
    java -jar apktool_2.0.0rc3.jar d heysdkdemo-cc2-kuaiwan.apk

解开apk以后

assets目录是资源目录，一般来说，SDK都不会管这个目录的
lib是native目录，如果有sdk有.so文件，需要复制到这个目录里面，kuaiwan有一个libentryex.so，所以这个需要复制进去
res目录会有很多东西需要同步过去
smali目录，其实就是java的展开的代码目录了，kuaiwan这里，需要同步的有

    com.alipay
    com.qvod
    com.UCMobile
    com.unionpay

然后考虑到我们heysdk的代码其实也被修改了，所以com.heysdk.lib也要同步一下

`AndroidManifest.xml`文件需要合并，这里我们提供了一个简单的xml合并工具，可以自动合并xml

用apktools分别将2个包都解开，smali目录里面，把快玩需要的内容复制到src里面，把快玩需要的res也替换过去，然后把 `AndroidManifest.xml` 编辑对，打包，然后签名，就好了

是不是很简单呢？

原理上其实就这么简单了，没啥太难的，不过要做到支持很多SDK，也还是要花一些精力的啊，没那么容易的。

我们的HeySDK在第一个版本也是按这个思路去做的，到今年年初就已经调整方向了，因为就我们自己使用来说，这样打包还是很繁琐，而且，这个方案基本上只能适用于android，ipa虽然也是一个zip文件，但最后走的是oc的编译链接，没办法实现无源打包，

再加上我们实际使用来看，和一些渠道SDK测试的时候，还是可能出一些其它的问题，没有代码的情况下，盲测还是很不方便的，有问题，也只能找中间SDK来解决，CP对项目的可控性太受限了，所以我们才调整方案，真心站在开发者角度，推出了我们自己的HeySDK，彻底开源，加入本地项目生成配置，IOS、Android统一一套方式，听起来是不是很爽呢，哈哈，现在开始限量内测哦，申请页面如下