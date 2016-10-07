## Bug追踪

### 9.1Bug追踪_Bugly
* 主页: [http://bugly.qq.com/](http://bugly.qq.com/)
* 功能:
	* 及时掌握App崩溃信息
	* 支持Android NDK 开发C/C++类型的异常上报
* 使用步骤
	1. 通过[http://bugly.qq.com/apps](http://bugly.qq.com/apps)注册应用
	2. 在module/build.gradle添加依赖
	
			android {
				defaultConfig {
					ndk {
						// 设置支持的SO库架构
						abiFilters 'armeabi' //, 'x86', 'armeabi-v7a', 'x86_6
						4', 'arm64-v8a'
					}
				}
			}
			dependencies {
				compile 'com.tencent.bugly:crashreport:latest.release' 
			}
	3. 在gradle.properties文件中添加:

			android.useDeprecatedNdk=true
	4. 添加权限

			<uses-permission android:name="android.permission.READ_PHONE_STATE"/>
			<uses-permission android:name="android.permission.INTERNET" />
			<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
			<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
			<uses-permission android:name="android.permission.READ_LOGS" />
	5. 在manifet文件的application节点配置相关参数

			<application
			<!-- 配置APP ID -->
			<meta-data
			android:name="BUGLY_APPID"
			android:value="<APP ID>" />
			<!-- 配置APP版本号 -->
			<meta-data
			android:name="BUGLY_APP_VERSION"
			android:value="<APP Version>" />
			<!-- 配置APP渠道号 -->
			<meta-data
			android:name="BUGLY_APP_CHANNEL"
			android:value="<APP Channel>" />
			<!-- 配置Bugly调试模式（true或者false）-->
			<meta-data
			android:name="BUGLY_ENABLE_DEBUG"
			android:value="<isDebug>" />
			</application>
	6. 在Application中初始化Bugly
	
			CrashReport.initCrashReport(getApplicationContext());

### BugTags
* 主页: [https://www.bugtags.com/](https://www.bugtags.com/)

### Testin
* 主页: [http://www.testin.cn/](http://www.testin.cn/)
