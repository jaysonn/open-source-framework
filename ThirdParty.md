## 第三方分享

### 6.1第三方分享_Mob	
* 主页: [http://www.mob.com/](http://www.mob.com/)
* 用途:第三方分享
* 使用步骤
	1. 访问[http://dashboard.mob.com/#/share/index](http://dashboard.mob.com/#/share/index)注册应用获取AppKey
	2. 访问[http://www.mob.com/#/downloadDetail/ShareSDK/android](http://www.mob.com/#/downloadDetail/ShareSDK/android)下载SDK
	3. 解压下载回来的SDK,打开ShareSDK for Android中的QuickIntegrater.jar,填入应用的名称和包名,让工具生成相关的资源文件.并拷贝到工程当中
![image](https://github.com/jaysonn/open-source-framework/blob/master/picture/57dbb020318622563b00000c.png)
	4. 配置权限
	
			<uses-permission android:name="android.permission.GET_TASKS" />
			<uses-permission android:name="android.permission.INTERNET" />
			<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
			<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
			<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
			<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
			<uses-permission android:name="android.permission.READ_PHONE_STATE" />
			<uses-permission android:name="android.permission.MANAGE_ACCOUNTS"/>
			<uses-permission android:name="android.permission.GET_ACCOUNTS"/>
			<!-- 蓝牙分享所需的权限 -->
			<uses-permission android:name="android.permission.BLUETOOTH" />
			<uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
	5. 添加Activity信息

			<activity
			     android:name="com.mob.tools.MobUIShell"
			     android:theme="@android:style/Theme.Translucent.NoTitleBar"
			     android:configChanges="keyboardHidden|orientation|screenSize"
			     android:screenOrientation="portrait"
			     android:windowSoftInputMode="stateHidden|adjustResize" >
			
			     <intent-filter>
					<!-- tencent后面的appid要保持和您配置的QQ的appid一致 -->
			         <data android:scheme="tencent100371282" />
			         <action android:name="android.intent.action.VIEW" />
			         <category android:name="android.intent.category.BROWSABLE" />
			         <category android:name="android.intent.category.DEFAULT" />
			     </intent-filter>
			
			    <!-- 调用新浪原生SDK，需要注册的回调activity -->
			    <intent-filter>
			        <action android:name="com.sina.weibo.sdk.action.ACTION_SDK_REQ_ACTIVITY" />
			        <category android:name="android.intent.category.DEFAULT" />
			    </intent-filter>
			</activity>

	6. 如果您集成了微信，易信，新浪微博支付宝还需要添加下面回调的activity处理

				<!--微信分享回调 -->
				 <activity
				     android:name=".wxapi.WXEntryActivity"
				     android:theme="@android:style/Theme.Translucent.NoTitleBar"
				     android:configChanges="keyboardHidden|orientation|screenSize"
				     android:exported="true"
				     android:screenOrientation="portrait" /> 
				
				<!--易信分享回调 -->
				 <activity
				     android:name=".yxapi.YXEntryActivity"
				     android:theme="@android:style/Theme.Translucent.NoTitleBar"
				     android:configChanges="keyboardHidden|orientation|screenSize"
				     android:exported="true"
				     android:screenOrientation="portrait" />
				
				 <!-- 支付宝分享回调 -->
				<activity
				    android:name=".apshare.ShareEntryActivity"
				    android:theme="@android:style/Theme.Translucent.NoTitleBar"
				    android:configChanges="keyboardHidden|orientation|screenSize"
				    android:exported="true"/>

	7. 更改assets/ShareSDK中的配置信息.根据自己的实际情况更改每一个平台的信息
	8. 分享.示例代码:

			private void showShare() {
			 ShareSDK.initSDK(this);
			 OnekeyShare oks = new OnekeyShare();
			 //关闭sso授权
			 oks.disableSSOWhenAuthorize(); 
			
			// 分享时Notification的图标和文字  2.5.9以后的版本不调用此方法
			 //oks.setNotification(R.drawable.ic_launcher, getString(R.string.app_name));
			 // title标题，印象笔记、邮箱、信息、微信、人人网和QQ空间使用
			 oks.setTitle(getString(R.string.share));
			 // titleUrl是标题的网络链接，仅在人人网和QQ空间使用
			 oks.setTitleUrl("http://sharesdk.cn");
			 // text是分享文本，所有平台都需要这个字段
			 oks.setText("我是分享文本");
			 // imagePath是图片的本地路径，Linked-In以外的平台都支持此参数
			 //oks.setImagePath("/sdcard/test.jpg");//确保SDcard下面存在此张图片
			 // url仅在微信（包括好友和朋友圈）中使用
			 oks.setUrl("http://sharesdk.cn");
			 // comment是我对这条分享的评论，仅在人人网和QQ空间使用
			 oks.setComment("我是测试评论文本");
			 // site是分享此内容的网站名称，仅在QQ空间使用
			 oks.setSite(getString(R.string.app_name));
			 // siteUrl是分享此内容的网站地址，仅在QQ空间使用
			 oks.setSiteUrl("http://sharesdk.cn");
			
			// 启动分享GUI
			 oks.show(this);
			 }
			 
### 6.2第三方分享_友盟
* 主页: [http://www.umeng.com/social](http://www.umeng.com/social)

----------


## 数据统计

### 7.1数据统计_百度统计
* 主页: [http://mtj.baidu.com/web/sdk/index](http://mtj.baidu.com/web/sdk/index)
* 开发文档: [http://developer.baidu.com/wiki/index.php?title=%E5%B8%AE%E5%8A%A9%E6%96%87%E6%A1%A3%E9%A6%96%E9%A1%B5/%E7%99%BE%E5%BA%A6%E7%A7%BB%E5%8A%A8%E7%BB%9F%E8%AE%A1API/%E7%99%BE%E5%BA%A6%E7%A7%BB%E5%8A%A8%E7%BB%9F%E8%AE%A1_Android%E7%89%88SDK](http://developer.baidu.com/wiki/index.php?title=%E5%B8%AE%E5%8A%A9%E6%96%87%E6%A1%A3%E9%A6%96%E9%A1%B5/%E7%99%BE%E5%BA%A6%E7%A7%BB%E5%8A%A8%E7%BB%9F%E8%AE%A1API/%E7%99%BE%E5%BA%A6%E7%A7%BB%E5%8A%A8%E7%BB%9F%E8%AE%A1_Android%E7%89%88SDK)
* 配置: 将下载回来的jar放在libs目录.并添加到依赖中
* 用途: 
	* 分析流量来源: 渠道流量对比、细分渠道分析，准确监控不同推广位数据，实时获知渠道贡献。
	* 分析用户:基于百度的海量数据积累，多维度分析并呈现用户画像信息。
	* 分析终端:设备分布一目了然（设备型号、品牌、操作系统、分辨率、联网方式、运营商等）。
* 使用步骤
	1. 登录[http://mtj.baidu.com/web/dashboard](http://mtj.baidu.com/web/dashboard)注册应用并获取appkey
	2. 在manifest文件中添加权限
	
		    <uses-permission android:name="android.permission.INTERNET" />
		    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
		    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
		    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
		    <uses-permission android:name="android.permission.WRITE_SETTINGS" />
		    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
		    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
		    <uses-permission android:name="android.permission.GET_TASKS" />
		    <uses-permission android:name="android.permission.BLUETOOTH" />
		    <!--（蓝牙为手表统计必填）-->
		    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
		    <!--（3.7.1 新增）-->
		    <uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
		    <!--可选的权限-->
		    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" /> 
	3. 在manifest文件的application节点添加相应的参数.根据实际业务需求选择
	
	        <!--您从百度网站获取的 APP  KEY-->
	        <meta-data
	            android:name="BaiduMobAd_STAT_ID"
	            android:value="08fbd2c8ce" />
	        <!--渠道商编号,根据实际情况自行填写-->
	        <meta-data
	            android:name="BaiduMobAd_CHANNEL"
	            android:value="Baidu Market" />
	        <!--是否开启错误日志统计，默认为 false-->
	        <meta-data
	            android:name="BaiduMobAd_EXCEPTION_LOG"
	            android:value="false" />
	        <!--日志发送策略， 可选值： APP_START、 ONCE_A_DAY、 SET_TIME_INTERVAL，
	        默认为 APP_START-->
	        <meta-data
	            android:name="BaiduMobAd_SEND_STRATEGY"
	            android:value="APP_START" />
	        <!--日志发送策略  为 SET_TIME_INTERVAL 时，需设定时间间隔.取值为 1-­‐24 的整数，默认为 1,单位为小时-->
	        <meta-data
	            android:name="BaiduMobAd_TIME_INTERVAL"
	            android:value="1" />
	        <!--日志仅在 wifi 网络下发送，默认为 false-->
	        <meta-data
	            android:name="BaiduMobAd_ONLY_WIFI"
	            android:value="false" />
	        <!--是否获取基站位置信息  ,默认为 true-->
	        <meta-data
	            android:name="BaiduMobAd_CELL_LOCATION"
	            android:value="true" />
	        <!--是否获取 GPS 位置信息，默认为 true-->
	        <meta-data
	            android:name="BaiduMobAd_GPS_LOCATION"
	            android:value="true" />
	        <!--是否获取 WIFI 位置信息，默认为 true-->
	        <meta-data
	            android:name="BaiduMobAd_WIFI_LOCATION"
	            android:value="true" />

	4. 在所有的Activity的onResume()和onPause()方法中调用StatService.onResume(Context  context) 和StatService.onPause  (Context  context)方法.所以最好创建一个BaseActiviy,并在其中实现这两个方法.出入的参数必须为this,不能是全局的Application Context.
	5. Fragment也是同理.在onResume()和onPause()方法中调用StatService.onResume(Context  context) 和StatService.onPause  (Context  context)方法

----------


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
