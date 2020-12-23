---
title: React-native中iOS获取IDFA方法与Android获取IMEI方法
date: 2018/06/06 18:45:21
---
# React-native中iOS获取IDFA方法与Android获取IMEI方法

# iOS获取IDFA

``` bash

npm install react-native-idfa —save

``` 
然后将其中android文件夹删去否则会报错
在使用页面引入 
``` bash

import { IDFA } from ‘react-native-idfa’;

```
``` bash

IDFA.getIDFA()

```
Ios14版本以上需要用户开启跟踪权限才可以获取到

# Android获取IMEI
在Android原生文件中书写原生代码
``` bash

@ReactMethod
public void getIMEI(Promise promise) {
    String imei = “”;
    try {
        TelephonyManager telephonyManager = (TelephonyManager) mContext.getSystemService(Context.TELEPHONY_SERVICE);
        if (Build.VERSION.SDK_INT >= _29_) {
            imei = “null”;
        } else if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            imei = telephonyManager.getImei();
        } else {
            imei = telephonyManager.getDeviceId();
        }
    } catch (Exception e) {
        e.printStackTrace();
    }

    String androidId = Settings.System.getString(mContext.getApplicationContext().getContentResolver(), Settings.System.ANDROID_ID);

    WritableMap map = Arguments.createMap();
    map.putString(“muId”, imei);  imei
    map.putString(“androidId”, androidId);  ANDROID_ID

     callback.invoke(map.toString());
    promise.resolve(map);
}

```
Android10以上获取不到IMEI用AndroidID代替
