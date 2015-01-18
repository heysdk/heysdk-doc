google的android studio正式版出了，所以adt就没有提供整合包，现在需要自己下载eclipse从头搭建环境，其实google官方文档说得很清楚了，一步步的来做没啥问题的，这里简单列一下吧。

1、下载eclipse，eclipse支持的环境太多了，我建议是不同的开发环境干脆用单独的包*（相对独立的环境太重要了，沙箱啊）*，所以不要在现有的eclipse下折腾了，重新下载一个吧，说是3.7.2以上即可，我下载的是最新的4.4.1，**Eclipse IDE for Java Developers**即可

2、打开eclipse，workspace也单独给一个目录吧，我用的workspace-adt

3、如果机器里面以前装过ADT、Android Studio之类的，可能已经有一个很完整的 AndroidSDK了，这时不建议重新配置，虽然建议eclipse单独，但androidSDK，建议还是配在一起，

`Window -> Perferences -> Android -> SDK Location`，配置你本地的即可

4、eclipse里面，`Help -> Install New Software`，点击 `Add`，增加 `ADT`，`url`给`https://dl-ssl.google.com/android/eclipse/`，确定即可。

5、等更新内容显示出来以后，全选，安装即可

注意：国内的用户可能会遇到google连接不了导致无法更新的问题，除了VPN以外，还可以通过修改hosts的方法来解决掉，就是修改hosts文件，

windows的在 `C:\Windows\System32\drivers\etc\host`

linux 的在 `/etc/hosts`

修改完，关闭文件就生效了。

给个[不断更新hosts的页面](href="http://www.360kb.com/kb/2_122.html)吧，感谢辛苦维护的站长。