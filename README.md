# android-point

1.MiniSdkVersion小于 13 时候：

（1）不设置Activity的android:configChanges时，切屏会重新调用各个生命周期，切横屏时会执行一次，切竖屏时会执行两次
（2）设置Activity的android:configChanges="orientation"时，切屏还是会重新调用各个生命周期，切横、竖屏时只会执行一次
（3）设置Activity的android:configChanges="orientation|keyboardHidden"时，切屏不会重新调用各个生命周期，只会执行onConfigurationChanged方法


2.从系统运行的角度看，AmS可以分为Client端和Service端：Client端运行在各个app进程，app进程实现了具体的Activity，Service等，告诉系统我有那些Activity，Service等，并且调用系统接口来完成显示;Service端运行在SystemServer进程，是系统级别的ActivityManagerService的具体实现，其响应Client端的系统调用请求，并且管理Client端各个app进程的生命周期。
AMS提供的功能主要包括以下几个方面：
   
   (1)对于Android四大组件（activity service broadcast content provider）的管理，包括启动，生命周期管理等
   (2)进程OOM adj以级LRU weight管理



3.WMS为所有窗口分配Surface(Surface是一块画布)，掌管Surface的显示顺序（Z-order）以及位置尺寸，控制窗口动画，并且还是输入系统的一重要的中转站。
本章将深入分析WMS的两个基础子系统的工作原理：
·  布局系统（Layout System），计算与管理窗口的位置、层次。
·  动画系统（Animation System），根据布局系统计算的窗口位置与层次渲染窗口动画。
