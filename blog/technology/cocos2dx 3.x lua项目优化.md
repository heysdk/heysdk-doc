cocos2dx升级到3.x以后，cpp的adt项目是几乎可以直接编译的，但lua项目貌似还是有些问题*(新版本其实是希望大家用cocos ide或者cocos命令行编译，但cocos ide不太好用，像我们有大量的本地代码的，如果不用ide修改和查看.cpp或者.mk之类的很麻烦，所以一个基本完整的adt项目还是必须的)*，这里介绍一下怎么快速的把lua项目快速配置好

1、首先，我们手动编辑`.project`文件，在`projectDescription`节点最后加入下面一段

``` xml
  <linkedResources>
    <link>
      <name>Classes</name>
      <type>2</type>
      <locationURI>$%7BPARENT-1-PROJECT_LOC%7D/Classes</locationURI>
    </link>
    <link>
      <name>cocos2d</name>
      <type>2</type>
      <locationURI>$%7BPARENT-2-PROJECT_LOC%7D/cocos2d-x</locationURI>
    </link>
    <link>
      <name>libcocos2d</name>
      <type>2</type>
      <locationURI>PARENT-2-PROJECT_LOC/cocos2d-x/cocos/platform/android/java/src</locationURI>
    </link>
  </linkedResources>
```

2、在`.classpath`文件里，添加以下内容

``` xml
<classpathentry kind="src" path="libcocos2d"/>
```

3、接下来，我们要为项目添加native编译，右键点击 `项目 -> Properties -> New -> Convert to a C/C++ Project(Adds C/C++ Nature)`，在打开的界面里，`ToolChains` 选 `Android GCC` 即可。

4、继续，右键点击 `项目 -> Properties -> C/C++ Build`在`Builder Settings`页面里，取消单选`Use default build command`，并修改`Build command`为`${NDK_ROOT}/ndk-build.cmd`。

5、修改 `jin -> Android.mk` 文件，在 `include $(CLEAR_VARS)` 下面加入

``` make
$(call import-add-path,$(LOCAL_PATH)/../../../cocos2d-x)
$(call import-add-path,$(LOCAL_PATH)/../../../cocos2d-x/external)
$(call import-add-path,$(LOCAL_PATH)/../../../cocos2d-x/cocos)
```

6、在cocos2dx 3.3下，还有个bug，就是复制库的时候，curl少复制了一批文件，但其实引擎目录中有，如果你用的是cocos2dx 3.3，将curl从引擎代码目录复制一份过去吧。

7、如果你使用了ndk r10，到现在的r10d，其实都没办法正常的用lua项目（有解决方案，但要加动态库），换r9d吧，[Compiling and linking error when using NDK r10 to build cocos2d-x v3.2](http://www.cocos2d-x.org/news/307)。