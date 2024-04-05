xmlmerge.js
===========

**xmlmerge.js** is a tool to merge xml files.

It was forked from [@heysdk](https://github.com/heysdk/xmlmerge-js/blob/master/xmlmerge.js), removed CSV dependency and added attribute merging on equal nodes.

Install it with:

    npm install --save https://github.com/EdenwareApps/xmlmerge.js

It was originally designed to merge the various xml configuration files, such as **AndroidManifest.xml**.

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


This is a simple **AndroidManifest.xml**, we want to add a set of properties

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
    

**xmlmerge.js** will be able to merge two xml correct, the results are as follows:

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

**xmlmerge.js** example:

    import XmlMerge from 'xmlmerge.js';
    XmlMerge.mergeWithFile(originalFilePath, mergingFilePath, resultFilePath, [
      {
          "nodename": "manifest",
          "attrname": "*"
      },
      {
          "nodename": "application",
          "attrname": "*"
      },
      {
          "nodename": "activity",
          "attrname": "*"
      },
      {
          "nodename": "uses-permission",
          "attrname": "android:name"
      },
      {
          "nodename": "uses-feature",
          "attrname": "android:name"
      },
      {
          "nodename": "service",
          "attrname": "android:name"
      }    
    ], () => console.log('DONE'))
    
