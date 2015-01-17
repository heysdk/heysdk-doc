cocos2dx升级到3.x以后，整个项目结构调整很多，个人觉得改得很不错的，就项目层面来说，主要有几点：

1、不需要引入libcocos2dx的lib项目了，很多团队用cocos2dx，开几个项目，牵扯到多个cocos2dx版本的时候，这个库项目就很折腾，在3.x下，用链接src目录解决了这个问题。

2、不是所有的静态库都强制完整链接，一定程度上会减小目标包。

3、大部分地方都用了相对目录，2.x下很多东西都依赖于一些全局宏，在处理多版本时也非常痛苦。

4、将cocos引擎代码放到项目里面了，其实我们很多项目都是这样做的，引擎代码和项目代码放在一起，也是为多项目开发时，不会因为某个项目更新引擎而影响其他的项目，但，cocos工具复制代码这个步骤太痛苦了，其实这点完全可以项目组解决掉的......不过也还算能接受了，复制代码的好处也是有的，就是项目目录结构会明确下来，很多事也方便很多。

现在还是有一些团队会使用2.x的版本，其实2.x的项目调整一下，引入3.x的一些特性还是很容易的，下面就大概的列一下：

1、导入自动生成的项目到ADT里面。

2、导入引擎的提供的src，具体操作是：

ADT中`右击工程名->Properties->Java Build Path->Source->Link Source->Browse`。

找到Cocos2d-x引擎根目录下`cocos/platform/android/java/src`，导入，名字给libcocos2dx，点击finish，OK。

3、如果在windows下，用NDK编译，需要改Build command，具体操作是：`ADT中右击工程名->Properties->C/C++ Build->Builder Settings->Build command`，给NDK目录下的ndk-build.cmd即可，

`${NDK_ROOT}/ndk-build.cmd`

4、找到 jni下面的 Android.mk文件，增加本地项目目录：
```make
$(call import-add-path,$(LOCAL_PATH)/../../../../)

include $(BUILD_SHARED_LIBRARY)[/code]
```
5、静态库不强制全部链接，还是修改 Android.mk 文件，把 `LOCAL_WHOLE_STATIC_LIBRARIES` 改成 `LOCAL_STATIC_LIBRARIES`，但是记住，**如果有引用一些其它库，而且其它库有必须要导出的Native代码，譬如给java调用的JNI代码，就不能这样改了**。

实际测试下来，这样改了以后减小包大小比较有限*（我们项目的.so文件大概减小了10%-20%）*，cocos2dx 2.x版本代码耦合度还是太高了，要深度挖掘才行。

6、把项目里面的 Classes、cocos2dx、extensions几个目录删掉吧，自己添加一下：

`C/C++ General -> Paths and Symbols -> Source Location -> Link Folder`

Folder name 给 classes，Link to folder in the file system勾上，把项目的 classes 绝对路径填上。

7、就目前的cocos2dx情况来看，建议android sdk的版本安装一下，8、18，就只需要装 SDK Platform即可。

8、由于在第2步里面，我们把libcocos2dx直接加到项目里面了，所以可以到项目配置里面，把libcocos2dx的Library删掉了，这个项目对于机器里面有多个cocos2dx版本的人来说最痛苦了，直接加到代码里面是最省事的做法。

`Properties -> Android`

**注意：不是所有的library项目都能这样的，只有纯代码的项目能这样处理哦。**

9、c++代码如果在Eclipse里打开，还是会报一堆错，我看path什么的都是设置的对的，暂时没特别好的解决方案，简单点的处理就是把c/c++的代码分析关掉。

`Properties -> C/C++ General -> Code Analysis`

选择 `Use project settings`，然后把下面的全部多选框都关上。

步骤还是有点多的，可以试试我们的[heysdktools](https://github.com/heysdk/heysdktools)工具包，执行 `proccc2proj.cmd` 或者 `proccc2proj.sh` 可以一键搞定项目。