# android知识点从浅到深梳理
* 今天开始使用Github，便有个想把android知识点从浅到深慢慢梳理的想法，平时太忙，不能天天更新，但每天都会记录，然后周末找时间敲出来，上传到Github，顺便熟悉熟悉Github。
## day_01
* 对于新人来说，最开始的应该就是安装各种运行环境了吧，这点就不再梳理的范围之内了。接下来便是知道android四层架构（重点）![](http://i.imgur.com/RgfQuwP.png)
 * APPLICATIONS（应用层）：
	java语言写的程序
 * APPLICATION FRAMEWORK（应用框架层）：
 	编写核心应用时所使用的API框架。开发人员可以根据这些框架来开发自己的应用程序。
 * LIBRARIES + ART(运行库层):
	各宗使用android应用框架时，所调用的各种类库。
 * LINUX KERNEL(LINUX 内核层):
 	里面存放着各种android系统中与移动设备相关的驱动程序。显示驱动，键盘驱动，相机驱动。蓝牙驱动等。
* 光认识框架还不够的，此外还理论与实操相结合，写了helloworld项目。并分析了项目的结构
 * src： 源代码，存放java写的源代码。
 * gen： 自动产生的java文件，子目录R存放着各种资源的id。
 * libs：存放第三方类库。
 * assets：存放一些单个文件大小不超过1m的
 * bin：存放的是二进制文件产生的app。
 * res：存放各种资源其中此类内的图片之类的资源，与R文件类内的资源是一一对应，也就是说每一个资源都有自己独一无二的id，方便开发者的调用读取。
## day_02
* android中的五大布局
	* LinearLayout 线性布局
	* RelativeLayout 相对布局
	* FrameLayout 帧布局
	* AbsoluteLayout 绝对布局
	* TableLayout 表格布局 
* 第一个控件 TextView
	* 实现跑马灯效果
    ```javascript
android:singleLine="true" 
android:ellipsize="marquee" 
android:focusable="true"
 android:focusableInTouchMode="true"
```
* LinearLayout(开发中使用较多)
	* 默认方向水平方向
	* orientation指定相关方向
	* 必须自己指定方向，不然易报错（ADT中）。
	* layout_gravity指的是当前的控件在父容器中的相对位置。
	* gravity指的是控件当中内容在控件中的相对位置。
	* layoutweight  权重 指的是当前控件所占剩下的比例。配合layout_width或者layout_height使用，可以达到评分父容器的效果。
	* layout_alignBaseline 基线对齐。类似于字与字对齐。
##day_03
* button控件的四种监听模式
	* onclikc属性（使用较多）
	* 匿名内部类（使用最多）
	* 内部类
	* 让类实现onClickListener接口（使用最多）
* EditText
	* 注册登录和用户交互的时候使用
	* hint起提示作用
	* inputtype 输入的类型。限制输入类型的
	* textPassword 输入的是密码，在密码框使用，效果就是平时使用的输入密码时，会变成星号。
	* singleLine单行输入
	* lines指定行数，一般和gravity配合使用，控制文本显示的位置
	* android：backgrroud = “@null”去掉系统的样式的时候这样写
#day_04
* 
Activity的生命周期：
	* onCreate：初始化工作，比如说setContentView，使用findVIewByid找到控件，添加监听，完成全局变量的设置，开启下载线程。
	* onStart的时候不可见，完成一些可见的准备工作，注册广播，经常调用。
	* onResume 对用户可见，非常频繁的调用（清凉级别的操作，弹出一个对话框，只需要借用一个boolean变量，首次进入的时候弹出）
	* onPause 失去焦点的时候调用，onPause中保存重要的数据（这是android最后一个安全的方法）
	* onStop 长时间不可见，解除注册广播
	* onDestory 销毁的时候调用，释放系统资源，停止下载线程（按下返回键的调用）
	* 一个完整的生命周期：oncreate-》onstart-》onResume-》onPause-》onstop-》ondestory
	* 一个可见的生命周期：onstart -》 onresume -》 onpause -》onstop
	* 一个前台的生命周期：onresume->onpause.
* activity的四种状态：
 * 活动状态或者运行状态（onresume之后）
 * 暂停状态（onpause之后）在极端内存不够的情况下会被系统杀死。
 * 停止状态（当一个activity完全覆盖另一个activity）onstop方法之后，变量的信息依然存在，onstop之后，经常会被系统杀死。
 * 销毁状态 ondestory销毁activity，当内存足够又会重启，并恢复之前的状态（被系统杀死）（被用户杀死不会重启）
* intent意图和abd很像
	* intent是连接四大组件的桥梁。（activity可以通过intent连接activity）
	* 栈  先进后出。
* 创建activity的步骤
	* 建一个类，继承activity
	* 创建布局文件
	* 绑定布局文件
	* 在清单文件中配置 
* 关于从另一个activity返回值
	* 注意requestcode和resultcode
	#day_05
* 显示启动
	* 显示启动自己的activity直接指定目的地，所到达的activity，直接指定类名（）
	* 显示启动（第三方）其他应用的activity（重点，，尤其在5.0的server中）
* 隐士启动（启动系统的activity）启动所有满足条件的activity，只要和其中一种同时匹配就可以
* <uses-permission android:name="android.permission.CALL_PHONE"/>给调用拨打电话，赋予权限。 
* 横竖屏切换声明周期（重点）
	* 横屏切换竖屏走一遍声明周期
	* 竖屏切换横屏走一遍生命周期
* 横竖屏切换会造成数据丢失，为什么：
	* 生命周期重新走一遍，所以都会丢失。
* 写死横竖屏 
	* android：configChanges=“keyboardHidden|screenSize|orientation”
	* 键盘隐藏，屏幕的大小，方向都会造成一件事（activity宽度和高度发生了改变）
	* 当写死之后，只会走onConfigurationChanged
	* android：screenOrientation=“portrait”写死竖屏
	* android：screenOrientation=“landscape”写死横屏
* 启动模式
	* 标准启动模式 standard启动之后activity放在了任务栈里面的stack里面
	* slinge Top一个栈里面不能有连续两个activity，但是可以有不连续的好多个activity。 跳转到登陆activity的时候，将loginactivity设置为singeTop（为了方式用户多点击好多次）
	* singeTask 任务栈里同一个activity只能有一个
	* ，如果启动它的话，会把上面的全部都弹走，主页面所在的activity全都设置为singeTask
	* singeinstance 会使得一个activity中只单独存在一个activity。（用于支付，分享等）
* intent的7种属性
	* action
	* category（对activity分类）
	* data
	* type
	* extra（存放数据）
	* ComponentName里面真正的封装了从哪里到哪里（重点）
	* flags设置启动模式  intent.FLAGACTIVITYNEW_TASK新开一个任务栈（重点）