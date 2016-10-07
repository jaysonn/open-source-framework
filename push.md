##消息推送

### 8.1消息推送_个推
* 主页: [http://www.getui.com/](http://www.getui.com/)
* 开发文档: [http://docs.getui.com/pages/viewpage.action?pageId=589890](http://docs.getui.com/pages/viewpage.action?pageId=589890)
* 使用步骤:
	1. 访问[https://dev.getui.com/dos4.0/index.html#login](https://dev.getui.com/dos4.0/index.html#login)注册应用
	2. 下载SDK并解压
	3. 将SDK解压后的资源文件中的GetuiExt.jar和GetuiSDK.jar拷贝到项目中的libs,并添加到依赖
		* 因为Android Studio工程默认已经添加了supportV7的依赖,如果没有,请添加supportV4的依赖,否则会有异常
		* 如果需要armeabi-v7a和x86的so文件,请自行下载.默认下载回来SDK中并不包含.
		* 如果要添加so文件,需要自行在\app\src\main目录中新建文件夹**jniLibs(一个字都不能错!!L是大写的)**,然后把对应的so文件添加进去.示例图:
![image](https://github.com/jaysonn/open-source-framework/blob/master/picture/57dbb000318622563b00000b.png)
	4. 将SDK解压后的资源文件中的layout文件拷贝到项目的layout文件夹
	5. 为了修改通知栏提示图标，请在res/drawable-hdpi/、res/drawable-mdpi/、res/drawable-ldpi/等各分辨率资源目录下，放置相应尺寸的push.png图片。可将SDK解压后的Demo工程中的push图片拷贝进来
	6. 添加权限. 注意替换包名


			<!-- 解决Android L上通知显示异常问题，targetSdkVersion需要设置成22 -->
			<uses-sdk
			    android:minSdkVersion="9"
			    android:targetSdkVersion="22" />
			<!-- 个推SDK权限配置开始 -->
			<uses-permission android:name="android.permission.INTERNET" />
			<uses-permission android:name="android.permission.READ_PHONE_STATE" />
			<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
			<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
			<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
			<uses-permission android:name="android.permission.WAKE_LOCK" />
			<uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
			<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
			<uses-permission android:name="android.permission.VIBRATE" />
			<uses-permission android:name="android.permission.GET_TASKS" />
			<!-- ibeancon 需要蓝牙权限 -->
			<uses-permission android:name="android.permission.BLUETOOTH"/>  
			<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
			<!-- 支持个推3.0 电子围栏功能 -->
			<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
			<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
			<!-- 浮动通知权限 -->
			<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW"/>
			<!-- 自定义权限 -->  
			<uses-permission android:name="getui.permission.GetuiService.你的包名" /><!--替换为第三方应用的包名-->
			<permission
			    android:name="getui.permission.GetuiService.你的包名"
			    android:protectionLevel="normal" >
			</permission><!--替换为第三方应用的包名-->
			<!-- 个推SDK权限配置结束 -->

	7. 在manifest/Application节点添加以下信息.注意替换内容

			<!--个推SDK配置开始-->
			    <!-- 配置的第三方参数属性 -->
			    <meta-data
			        android:name="PUSH_APPID"
			        android:value="你的APPID" /><!--替换为第三方应用的APPID-->
			    <meta-data
			        android:name="PUSH_APPKEY"
			        android:value="你的APPKEY" /><!--替换为第三方应用的APPKEY-->
			    <meta-data
			        android:name="PUSH_APPSECRET"
			        android:value="你的APPSECRET" /><!--替换为第三方应用的APPSECRET-->
			    <!-- 配置SDK核心服务 -->
			    <service
			        android:name="com.igexin.sdk.PushService"
			        android:exported="true"
			        android:label="NotificationCenter"
			        android:process=":pushservice" />
			    <service
			        android:name="com.igexin.sdk.PushServiceUser"
			        android:exported="true"
			        android:label="NotificationCenterUser" />
			    <receiver android:name="com.igexin.sdk.PushReceiver" >
			        <intent-filter>
			            <action android:name="android.intent.action.BOOT_COMPLETED" />
			            <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
			            <action android:name="android.intent.action.USER_PRESENT" />
			            <action android:name="com.igexin.sdk.action.refreshls" />
			            <!-- 以下三项为可选的action声明，可大大提高service存活率和消息到达速度 -->
			            <action android:name="android.intent.action.MEDIA_MOUNTED" />
			            <action android:name="android.intent.action.ACTION_POWER_CONNECTED" />
			            <action android:name="android.intent.action.ACTION_POWER_DISCONNECTED" />
			        </intent-filter>
			    </receiver>
			     
			    <receiver
			        android:name="com.igexin.sdk.PushManagerReceiver"
			        android:exported="false" >
			        <intent-filter>
			            <action android:name="com.igexin.sdk.action.pushmanager" />
			        </intent-filter>
			    </receiver>
			    <activity
			        android:name="com.igexin.sdk.PushActivity"
			        android:excludeFromRecents="true"
			        android:exported="false"
			        android:process=":pushservice"
			        android:taskAffinity="com.igexin.sdk.PushActivityTask"
			        android:theme="@android:style/Theme.Translucent.NoTitleBar" />
			    <activity
			        android:name="com.igexin.sdk.GActivity"
			        android:excludeFromRecents="true"
			        android:exported="true"
			        android:process=":pushservice"
			        android:taskAffinity="com.igexin.sdk.PushActivityTask"
			        android:theme="@android:style/Theme.Translucent.NoTitleBar"/>
			 
			    <service
			        android:name="com.igexin.download.DownloadService"
			        android:process=":pushservice" />
			 
			    <receiver android:name="com.igexin.download.DownloadReceiver" >
			        <intent-filter>
			            <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
			        </intent-filter>
			    </receiver>
			 
			    <provider
			        android:name="com.igexin.download.DownloadProvider"
			        android:exported="true"
			        android:authorities="downloads.你的包名"
			        android:process=":pushservice" /><!--替换为第三方应用的包名-->
			 
			    <activity   
			        android:name="com.igexin.getuiext.activity.GetuiExtActivity"   
			        android:configChanges="orientation|keyboard|keyboardHidden"  
			        android:excludeFromRecents="true" 
			        android:exported="false" 
			        android:process=":pushservice"   
			        android:taskAffinity="android.task.myServicetask"   
			        android:theme="@android:style/Theme.Translucent.NoTitleBar" />
			     
			    <receiver
			        android:name="com.igexin.getuiext.service.PayloadReceiver"
			        android:exported="false" >
			        <intent-filter>
			            <action android:name="com.igexin.sdk.action.7fjUl2Z3LH6xYy7NQK4ni4" />
			            <action android:name="com.igexin.sdk.action.你的APPID" /><!--替换为第三方应用的APPID-->
			        </intent-filter>
			    </receiver>
			    <service
			        android:name="com.igexin.getuiext.service.GetuiExtService"
			        android:process=":pushservice" />
			 
			<!-- 个推SDK配置结束 -->

	8. 在Activity中初始化SDK

			PushManager.getInstance().initialize( this.getApplicationContext() );
		*　该方法必须在Activity或Service类内调用，一般情况下，可以在Activity的onCreate()方法中调用。由于应用每启动一个新的进程，就会调用一次Application的onCreate()方法，而个推SDK是一个独立的进程，因此如果在Application的onCreate()中调用intialize接口，会导致SDK初始化在一个应用中多次调用，所以不建议在Application继承类中调用个推SDK初始化接口。

	9. 在手机或模拟器上运行您的工程，查看Android Monitor信息，如图所示。在搜索框中输入“clientid”可以看到“clientid is xxx”，则意味则初始化SDK成功，并获取到相应的cid信息，恭喜你:-D，可以开始进行推送测试了。如图所示:
![image](https://github.com/jaysonn/open-source-framework/blob/master/picture/57dbaff0318622563b00000a.png)


### 友盟
* 主页: [http://www.umeng.com/push](http://www.umeng.com/push)

### 百度云推送
* 主页: [http://push.baidu.com/fc](http://push.baidu.com/fc)

### 腾讯信鸽
* 主页: [http://xg.qq.com/xg](http://xg.qq.com/xg)
