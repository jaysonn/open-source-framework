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
