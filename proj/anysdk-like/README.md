anysdk-like
===========

**AnySDK**��**����**��Ʒ��**����SDK�������**�������з���ֻ��Ҫ����**AnySDK**�����ɺ�̨�������SDK��������ô�������أ�

��ʵ����android��Ϥ��ͬѧ��Ӧ��֪����apk�ļ���ʵ����һ��zip��������Ҳ�к຺ܶ�����������̳̣�����ֱ���޸�apk����ʵ�ֵģ�����**AnySDK**����ʵ�������Լ���apk������apk֮�����һ��ͨ�ò㣬�ټ���java����⿪�󶼻��ǰ�class�ֿ��ģ�������������������ҪԴ���룬ֱ��ͨ���޸�apk�������Դ��class�ļ���ʵ�ֳ���ͬ����APK�İ汾��

��ǰ**umeng**������һ��ר���޸�����id��apk������ߣ���ʵҲ��һ����ԭ�����������°����������ֱ�ӽ���gradle�ˣ�˵��google�����µĴ����ʽ������������ʹ�õ�apktool��������ʵӰ�첻����Ȼ��������ʹ�ã���Ȼ������ԭ��û̫�о���

������һ�����ļ򵥵��ֶ�ʵ��һ�����������Ӱɡ�

���ȣ����������µ�**cocos2dx**Ϊ���ӣ�����һ��**cocos2dx**��Ŀ����һ�㣬��cpp�İ�

Ȼ������Լ���SDK����࣬�ͽ�**HeySDK**�ɣ��������£�

    package com.heysdk.lib;

    import android.content.Context;

    public class HeySDK {
     public static Context mContext;
 
     public static void init(Context context) {
      mContext = context;
     }
 
     // �Զ���½������Ϸ���ؽ�����ü���
     public static void autologin() {
     }
    }

����activity���棬�����ʼ������

    protected void onCreate(Bundle savedInstanceState){
      super.onCreate(savedInstanceState);
 
      HeySDK.init(this);
     }

java����������ˣ���������c++����ɣ���Ϊ�����ӣ����Ǿͼ�һ�㣬�� `HelloWorldScene.cpp` �����һ���򵥵ĺ��������ø�д��java����ɣ���ס��ü���androud�Ļ�����顣

���һ��include

    #include "platform/android/jni/JniHelper.h"

Ȼ�����autologin����

    static int autologin()
    {
     cocos2d::JniMethodInfo minfo;
     bool isHave = cocos2d::JniHelper::getStaticMethodInfo(minfo, "com.heysdk.lib.HeySDK", "autologin", "()V");
     if(isHave)
     {
      minfo.env->CallStaticObjectMethod(minfo.classID, minfo.methodID);
     }
    }

����� `HelloWorld::init()` ��󷵻�true��ǰ�������Զ���½�ĵ��á�

    autologin();

ʵ��һ�� `autologin` ��������һ�㣬�����ȳ�һ��ʲô�������İ汾��Ȼ���һ��apk�������ǽ��� src �ɡ�

�ٶԽ�һ��sdk�����������ÿ��������ӣ����Խ���һ�¿��棬Ȼ���ٳ�һ���������ǽ��� kuaiwan ���ˡ�

2�����������Ժ���ȥ `http://code.google.com/p/android-apktool/` ����һ�����µ�apktool��һ�㽨���������µ�jar���ɣ����°���µ�SDK���֧�ֵø��ã�������2.0RC3��

    java -jar apktool_2.0.0rc3.jar d heysdkdemo-cc2.apk
    java -jar apktool_2.0.0rc3.jar d heysdkdemo-cc2-kuaiwan.apk

�⿪apk�Ժ�

assetsĿ¼����ԴĿ¼��һ����˵��SDK����������Ŀ¼��
lib��nativeĿ¼�������sdk��.so�ļ�����Ҫ���Ƶ����Ŀ¼���棬kuaiwan��һ��libentryex.so�����������Ҫ���ƽ�ȥ
resĿ¼���кܶණ����Ҫͬ����ȥ
smaliĿ¼����ʵ����java��չ���Ĵ���Ŀ¼�ˣ�kuaiwan�����Ҫͬ������

    com.alipay
    com.qvod
    com.UCMobile
    com.unionpay

Ȼ���ǵ�����heysdk�Ĵ�����ʵҲ���޸��ˣ�����com.heysdk.libҲҪͬ��һ��

`AndroidManifest.xml`�ļ���Ҫ�ϲ������������ṩ��һ���򵥵�xml�ϲ����ߣ������Զ��ϲ�xml

��apktools�ֱ�2�������⿪��smaliĿ¼���棬�ѿ�����Ҫ�����ݸ��Ƶ�src���棬�ѿ�����Ҫ��resҲ�滻��ȥ��Ȼ��� `AndroidManifest.xml` �༭�ԣ������Ȼ��ǩ�����ͺ���

�ǲ��Ǻܼ��أ�

ԭ������ʵ����ô���ˣ�ûɶ̫�ѵģ�����Ҫ����֧�ֺܶ�SDK��Ҳ����Ҫ��һЩ�����İ���û��ô���׵ġ�

���ǵ�HeySDK�ڵ�һ���汾Ҳ�ǰ����˼·ȥ���ģ�������������Ѿ����������ˣ���Ϊ�������Լ�ʹ����˵������������Ǻܷ��������ң��������������ֻ��������android��ipa��ȻҲ��һ��zip�ļ���������ߵ���oc�ı������ӣ�û�취ʵ����Դ�����

�ټ�������ʵ��ʹ����������һЩ����SDK���Ե�ʱ�򣬻��ǿ��ܳ�һЩ���������⣬û�д��������£�ä�⻹�Ǻܲ�����ģ������⣬Ҳֻ�����м�SDK�������CP����Ŀ�Ŀɿ���̫�����ˣ��������ǲŵ�������������վ�ڿ����߽Ƕȣ��Ƴ��������Լ���HeySDK�����׿�Դ�����뱾����Ŀ�������ã�IOS��Androidͳһһ�׷�ʽ���������ǲ��Ǻ�ˬ�أ����������ڿ�ʼ�����ڲ�Ŷ������ҳ������