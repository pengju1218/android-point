# android-point

1.MiniSdkVersion小于 13 时候：

（1）不设置Activity的android:configChanges时，切屏会重新调用各个生命周期，切横屏时会执行一次，切竖屏时会执行两次
（2）设置Activity的android:configChanges="orientation"时，切屏还是会重新调用各个生命周期，切横、竖屏时只会执行一次
（3）设置Activity的android:configChanges="orientation|keyboardHidden"时，切屏不会重新调用各个生命周期，只会执行onConfigurationChanged方法


2.从系统运行的角度看，AmS可以分为Client端和Service端：Client端运行在各个app进程，app进程实现了具体的Activity，Service等，告诉系统我有那些Activity，Service等，并且调用系统接口来完成显示;Service端运行在SystemServer进程，是系统级别的ActivityManagerService的具体实现，其响应Client端的系统调用请求，并且管理Client端各个app进程的生命周期。
AMS提供的功能主要包括以下几个方面：
   
   (1)对于Android四大组件（activity service broadcast content provider）的管理，包括启动，生命周期管理等
   (2)进程OOM adj以级LRU weight管理
