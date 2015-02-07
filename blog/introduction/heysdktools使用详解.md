heysdktools使用详解
===

**heysdktools**是**[HeySDK](http://www.heysdk.com)**提供的一套对接工具，除了能快速对接**[HeySDK](http://www.heysdk.com)**外，还能自动优化一些通用引擎项目(*cocos2d-x*等)。

一般来说，我们可以通过*npm*来获取**heysdktools**。

```
npm install -g heysdktools
```

这样我们就可以在命令行直接使用**heysdk**命令了，当我们从后台创建好项目，导出项目配置文件后，直接命令下面的命令，就可以创建一个基本的对接项目了。

```
heysdk init proj.csv
```

后面如果需要更多的渠道配置，也一样的执行

```
heysdk init 360.csv
heysdk init uc.csv
...
```

就可以在本地自动创建项目，一般来说，只有最基本的heysdk对接项目才需要提交代码管理，未来的开发，也建议在heysdk基本项目的基础上来进行，而第三方渠道的项目，建议是只提交项目配置文件，需要出包的时候再生成项目直接出包即可。