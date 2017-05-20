# android-point
Android从启动到程序运行发生的事情:http://blog.csdn.net/jonstank2013/article/details/51118563（重要，需要多看看）
Android内存泄露  http://blog.csdn.net/gemmem/article/details/13017999
ANT打包android http://blog.csdn.net/liuhe688/article/details/6679879
 
 
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



4.PMS用来管理所有的package信息，包括安装、卸载、更新以及解析AndroidManifest.xml以组织相应的数据结构，


5.android事件

（1）public boolean dispatchTouchEvent(MotionEvent ev)  这个方法用来分发TouchEvent，返回true，事件传递，返回false，不传
（2）public boolean onInterceptTouchEvent(MotionEvent ev) 这个方法用来拦截TouchEvent，默认返回false，返回true表示拦截。
（3）public boolean onTouchEvent(MotionEvent ev) 这个方法用来处理TouchEvent


6.1. 什么情况下会发生anr

(1). KeyDispatchTimeout(5 seconds) --主要类型按键或触摸事件在特定时间内无响应
(2). BroadcastTimeout(10 seconds) --BroadcastReceiver在特定时间内无法处理完成
(3). ServiceTimeout(20 seconds) --小概率类型 Service在特定的时间内无法处理完成
 


7.理解Activity，View,Window三者关系

这个问题真的很不好回答。所以这里先来个算是比较恰当的比喻来形容下它们的关系吧。Activity像一个工匠（控制单元），Window像窗户（承载模型），View像窗花（显示视图）LayoutInflater像剪刀，Xml配置像窗花图纸。
1：Activity构造的时候会初始化一个Window，准确的说是PhoneWindow。
2：这个PhoneWindow有一个“ViewRoot”，这个“ViewRoot”是一个View或者说ViewGroup，是最初始的根视图。
3：“ViewRoot”通过addView方法来一个个的添加View。比如TextView，Button等
4：这些View的事件监听，是由WindowManagerService来接受消息，并且回调Activity函数。比如onClickListener，onKeyDown等。




