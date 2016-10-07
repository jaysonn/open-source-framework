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



