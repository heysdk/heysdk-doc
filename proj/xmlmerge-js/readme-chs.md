xmlmerge-js
===========

**mlmerge-js** ��һ���ϲ�xml�Ĺ��߿⡣

�������Ŀ���������ϲ�����xml�����ļ��ģ�Ʃ��**AndroidManifest.xml**��

    <?xml version="1.0" encoding="utf-8"?>
    
    <manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.heysdk.demo" android:versionCode="1" android:versionName="1.0" android:installLocation="auto">  
      <uses-sdk android:minSdkVersion="14"/>  
      <uses-feature android:glEsVersion="0x00020000"/>  
      <application android:label="@string/app_name" android:icon="@drawable/icon"> 
        <activity android:name=".heysdkdemo" android:label="@string/app_name" android:screenOrientation="landscape" android:theme="@android:style/Theme.NoTitleBar.Fullscreen" android:configChanges="orientation"> 
          <intent-filter> 
            <action android:name="android.intent.action.MAIN"/>  
            <category android:name="android.intent.category.LAUNCHER"/> 
          </intent-filter> 
        </activity> 
      </application>  
      <supports-screens android:largeScreens="true" android:smallScreens="true" android:anyDensity="true" android:normalScreens="true"/>  
      <uses-permission android:name="android.permission.INTERNET"/> 
    </manifest>


����һ����ͨ��**AndroidManifest.xml**��������Ϊ������һ������

    <?xml version="1.0" encoding="utf-8"?>

    <manifest xmlns:android="http://schemas.android.com/apk/res/android">  
      <application> 
        <activity android:name="com.qvod.pay.ChargeActivity" android:configChanges="keyboardHidden|orientation|screenSize"></activity>  
        <activity android:name="com.unionpay.uppay.PayActivityEx" android:configChanges="orientation|keyboardHidden|screenSize" android:excludeFromRecents="true" android:label="@string/app_name" android:screenOrientation="portrait" android:windowSoftInputMode="adjustResize"/> 
      </application>  
      <uses-permission android:name="android.permission.INTERNET"/>  
      <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>  
      <uses-permission android:name="android.permission.CALL_PHONE"/>  
      <uses-permission android:name="android.permission.READ_PHONE_STATE"/>  
      <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>  
      <uses-permission android:name="android.permission.READ_PHONE_STATE"/> 
    </manifest>
    
��ʵ���ǽ���2��xml�ϲ���һ��Ϊ�˷���ĺϲ�xml��������Ҫһ���򵥵����ã�Ʃ�����**mlmerge-js** *manifest* �� *application* ��ֱ��ƥ��ģ�����Ҫƥ���κ����ԣ���*activity* �� *uses-permission* ����Ҫƥ�� *android:name* �ģ����������ظ�������ԣ���ô�����ṩ��һ��csv�������ļ���

    nodename,attrname
    manifest,*
    application,*
    activity,android:name
    uses-permission,android:name

������**mlmerge-js**������ȷ�ĺϲ�2��xml�ˣ�������£�

    <?xml version="1.0" encoding="utf-8"?>

    <manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.heysdk.demo" android:versionCode="1" android:versionName="1.0" android:installLocation="auto">  
      <uses-sdk android:minSdkVersion="14"/>  
      <uses-feature android:glEsVersion="0x00020000"/>  
      <application android:label="@string/app_name" android:icon="@drawable/icon"> 
        <activity android:name=".heysdkdemo" android:label="@string/app_name" android:screenOrientation="landscape" android:theme="@android:style/Theme.NoTitleBar.Fullscreen" android:configChanges="orientation"> 
          <intent-filter> 
            <action android:name="android.intent.action.MAIN"/>  
            <category android:name="android.intent.category.LAUNCHER"/> 
          </intent-filter> 
        </activity>  
        <activity android:name="com.qvod.pay.ChargeActivity" android:configChanges="keyboardHidden|orientation|screenSize"/>  
        <activity android:name="com.unionpay.uppay.PayActivityEx" android:configChanges="orientation|keyboardHidden|screenSize" android:excludeFromRecents="true" android:label="@string/app_name" android:screenOrientation="portrait" android:windowSoftInputMode="adjustResize"/>  
        <activity android:name="com.unionpay.uppay.PayActivity" android:configChanges="orientation|keyboardHidden|screenSize" android:excludeFromRecents="true" android:screenOrientation="portrait" android:theme="@style/Theme.UPPay"/> 
      </application>  
      <supports-screens android:largeScreens="true" android:smallScreens="true" android:anyDensity="true" android:normalScreens="true"/>  
      <uses-permission android:name="android.permission.INTERNET"/>  
      <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>  
      <uses-permission android:name="android.permission.CALL_PHONE"/>  
      <uses-permission android:name="android.permission.READ_PHONE_STATE"/>  
      <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/> 
    </manifest>

**mlmerge-js**��������*samples*��*test.js*��

    var xmlmerge = require('../xmlmerge.js');
    var fs = require('fs');
    var csv2obj = require("../csv2obj");

    fs.readFile('samples/AndroidManifest.xml', function(err, data) {
        var str1 = data.toString();

        fs.readFile('samples/kuaiwan.xml', function(err, data) {
            var str2 = data.toString();

            fs.readFile('samples/AndroidManifest.csv', function(err, data) {

                config = csv2obj.csv2obj(data.toString());

                xmlmerge.merge(str1, str2, config, function (xml) {
                    fs.writeFile('samples/output.xml', xml, function (err) {

                    });
                });
            });
        });
    });
