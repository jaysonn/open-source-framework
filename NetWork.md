## 网络

**使用网络库不要忘记添加网络权限**

### 2.1网络_Volley 

* 主页:[https://android.googlesource.com/platform/frameworks/volley/](https://android.googlesource.com/platform/frameworks/volley/ )

* 特点: 
	* 通信更快,更简单
	* 支持网络请求的排序,优先级处理
	* 支持网络请求的缓存
	* 多级别的取消请求
	* 扩展性强

* 使用步骤:
	1. 创建RequestQueue
	2. 创建Request
	3. 添加Request到RequestQueue
	
* 注意事项: 
	* 如果自己编译Volley的话,compileSdkVersion需要<=22,这是因为在Android6.0中Google移除了httpClient相关的API
	* Volley仅适合用于通信频繁数据量小的网络操作
	* 大数据量的网络操作并不适合Volley
	* 生成的jar文件地址:
		* \build\intermediates\bundles\release\classes.jar

	* 生成的aar文件地址:
		* \build\outputs\aar

* 工作原理图

![image](https://github.com/jaysonn/open-source-framework/blob/master/picture/57dba83e318622563b000003.png)

* 使用步骤:
	1. 创建RequestQueue
	2. 创建Request对象
	3. 添加Request对象到RequestQueue中

### 2.2网络_Okhttp	
* 主页: [https://github.com/square/okhttp](https://github.com/square/okhttp)
* 配置: 添加依赖 compile 'com.squareup.okhttp3:okhttp:3.2.0'
* 特点:
	* 支持HTTP/2 和 SPDY
	* 默认支持 GZIP 降低传输内容的大小
	* 支持网络请求的缓存
	* 当网络出现问题时,自动重试一个主机的多个 IP 地址
	
* 使用步骤:
	1. 创建OkHttpClient对象
	2. 创建Request对象
	3. 添加Request对象到OkHttpClient对象中并执行请求.示例代码:

				OkHttpClient client=new OkHttpClient();
                RequestBody body = new FormBody.Builder()
                        .add("phone", "13812345678")// 构造请求的参数
                        .add("key", "daf8fa858c330b22e342c882bcbac622")// 构造请求的参数
                        .build();
                Request post_request = new Request.Builder()
                        .url(URL_POST)// 指定请求的地址
                        .post(body)// 指定请求的方式为POST
                        .build();
                client.newCall(post_request).enqueue(new Callback() {
                    @Override
                    public void onFailure(Call call, IOException e) {
                        // 请求失败的处理
                    }

                    @Override
                    public void onResponse(Call call, Response response) throws IOException {	// 请求成功的处理
                        ResponseBody body = response.body();
                        String string = body.string();// 把返回的结果转换为String类型
						// body.bytes();// 把返回的结果转换为byte数组
						// body.byteStream();// 把返回的结果转换为流
                    }
                });
	

* 因为原生OkHttp的使用比较复杂,有一个包装过的工具项目okhttp-utils使用非常简单
	* 添加依赖: compile 'com.zhy:okhttputils:2.3.8'
	* 工具类简介:[https://github.com/hongyangAndroid/okhttp-utils](https://github.com/hongyangAndroid/okhttp-utils)

### 2.3网络_Retrofit	 
* 主页: [https://github.com/square/retrofit](https://github.com/square/retrofit)
* 注意: 使用Retrofit的前提是**服务器端代码遵循REST规范 !!!!!**
* 功能: 
	* 效率非常高
	* 可以直接将结果转换称Java类
	* 主要是配合RxJava一起使用
* 配置: 
	* 添加Retrofit依赖: compile 'com.squareup.retrofit2:retrofit:2.0.2'
	* 添加数据解析依赖,根据实际情况进行选择
		* Gson : com.squareup.retrofit2:converter-gson:2.0.2
		* Jackson : com.squareup.retrofit2:converter-jackson:2.0.2
		* Moshi : com.squareup.retrofit2:converter-moshi:2.0.2
		* Protobuf : com.squareup.retrofit2:converter-protobuf:2.0.2
		* Wire : com.squareup.retrofit2:converter-wire:2.0.2
		* Simple XML : com.squareup.retrofit2:converter-simplexml:2.0.2

* 使用步骤: 
	1. 利用[http://www.jsonschema2pojo.org/](http://www.jsonschema2pojo.org/)创建数据模型
	2. 创建REST API 接口
		* 常用注解:
			* 请求方法:@GET / @POST / @PUT / @DELETE / @HEAD
			* URL处理
				* @Path - 替换参数
				
						@GET("/group/{id}/users")
						public Call<List<User>> groupList(@Path("id") int groupId);
				* @Query - 添加查询参数
				
						@GET("/group/{id}/users")
						public Call<List<User>> groupList(@Path("id") int groupId, @Query("sort") String sort);
				* @QueryMap - 如果有多个查询参数，把它们放在Map中

						@GET("/group/{id}/users")
						public Call<List<User>> groupList(@Path("id") int groupId, @QueryMap Map<String, String> options);
		* 示例代码:

				public interface NetAPI {
				    @GET("/users/{user}")
				    public Call<GitModel> getFeed(@Path("user") String user);
				
				    @GET("/service/getIpInfo.php")
				    public Call<IPModel> getWeather(@Query("city")String city);
				}
	3. 创建Retrofit对象, 并发起请求.示例代码:

	        // 构建Retrofit实例
	        Retrofit retrofit = new Retrofit.Builder().
	                baseUrl(API2).
	                addConverterFactory(GsonConverterFactory.create()).
	                build();
	        // 构建接口的实现类
	        IpAPI weatherAPI = retrofit.create(IpAPI.class);
	        // 调用接口定义的方法
	        Call<IPModel> weatherCall = weatherAPI.getWeather("8.8.8.8");
	        // 异步执行请求
	        weatherCall.enqueue(new Callback<IPModel>() {
	            @Override
	            public void onResponse(Call<IPModel> call, Response<IPModel> response) {
	                IPModel model = response.body();
	                System.out.println("country:" + model.getData().getCountry());
	            }
	
	            @Override
	            public void onFailure(Call<IPModel> call, Throwable t) {
	                System.out.println(t.toString());
	            }
	        });

* 优点: 
![image](https://github.com/jaysonn/open-source-framework/blob/master/picture/57dba85f318622563b000004.png)
