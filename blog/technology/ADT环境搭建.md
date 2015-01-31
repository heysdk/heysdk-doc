google的android studio正式版出了，所以adt就没有提供整合包，现在需要自己下载eclipse从头搭建环境，其实google官方文档说得很清楚了，一步步的来做没啥问题的，这里简单列一下吧。

1、下载eclipse，eclipse支持的环境太多了，我建议是不同的开发环境干脆用单独的包*（相对独立的环境太重要了，沙箱啊）*，所以不要在现有的eclipse下折腾了，重新下载一个吧，说是3.7.2以上即可，我下载的是最新的4.4.1*（在mac下，建议还是用3.7.2吧，4.4.1折腾了好久，什么都装完了，但CDT就是不能用T_T）*，**Eclipse IDE for Java Developers**即可

2、打开eclipse，workspace也单独给一个目录吧，我用的workspace-adt

3、如果机器里面以前装过ADT、Android Studio之类的，可能已经有一个很完整的 AndroidSDK了，这时不建议重新配置，虽然建议eclipse单独，但androidSDK，建议还是配在一起，

`Window -> Perferences -> Android -> SDK Location`，配置你本地的即可

4、eclipse里面，`Help -> Install New Software`，点击 `Add`，这里可以直接在线安装，也可以使用本地已经下载好的zip包。

直接在线安装的话，增加 `ADT`，`url`给`https://dl-ssl.google.com/android/eclipse/`，确定即可。

也可以去[官网](http://developer.android.com/sdk/installing/installing-adt.html)找到最新的ADT独立安装包，目前最新的是23.0.4，下载好以后，还是在上面那个`Add`对话框里，点击`Archive`，然后选中刚才下载好的文件就好了。

5、等更新内容显示出来以后，全选，安装即可

注意：国内的用户可能会遇到google连接不了导致无法更新的问题，除了VPN以外，还可以通过修改hosts的方法来解决掉，就是修改hosts文件，

windows的在 `C:\Windows\System32\drivers\etc\host`

linux 的在 `/etc/hosts`

修改完，关闭文件就生效了。

给个[不断更新hosts的页面](href="http://www.360kb.com/kb/2_122.html)吧，感谢辛苦维护的站长。

6、安装过程中，可能会提示`security warning`，这时可以不用管，直接点`OK`，但我看了一下，确实是`NDT`的哪一组有问题，所以我的mac在4.4.1下始终装不好，但windows是好的。

7、接下来可以下载`NDK`，[官网](http://developer.android.com/tools/sdk/ndk/index.html)，最新的r10(一直到r10d)都有bug，`luajit`编译有些问题，当然也有解决方案，可以看看[Compiling and linking error when using NDK r10 to build cocos2d-x v3.2](http://www.cocos2d-x.org/news/307)，个人还是建议用r9d吧。