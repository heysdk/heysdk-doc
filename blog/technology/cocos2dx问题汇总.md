cocos2dx问题解决汇总
===

1、明明环境变量里有`NDK_ROOT`，但依然提示

```
NDK_ROOT not defined. Please define NDK_ROOT in your environment
```

**解决方法**：

首先，`项目 -> Properties -> C/C++ Build -> Environment -> Add`，在弹出的对话框里，`Name`里填`NDK_ROOT`，点击 `Variables`，选择`NDK_ROOT`，顺便选中 `Add to all configurations`即可。

2、连接错误 `error: relocation overflow in R_ARM_THM_CALL`

如果是`js`项目，
```
Solution: 
Add 
LOCAL_ARM_MODE := arm
to files
/runtime-scr/proj.android/jni/Android.mk 
/js-bindings/bindings/Android.mk
```
如果是`lua`项目，需要修改`lua-bindings`的`Android.mk`文件。

3、在mac或linux下，可能会出现`permission denied`的错误，一般会出现在`cocos`命令上，如果单单把这个文件处理了，后面可能还会有一堆错误，所以建议把整个目录权限给对，在终端里面，改变`cocos2d-console`的权限即可。

```
chmod -R 777 cocos2d-console
```

4、如果是自解压的引擎代码，PATH设置对以后，cocos命令可能会提示命令不存在，类似`command not found`这样的，需要给cocos加运行权限。
```
chmod +x cocos
```

