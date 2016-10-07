## 图像

### 3.1图像_UIL 
* 主页: [https://github.com/nostra13/Android-Universal-Image-Loader](https://github.com/nostra13/Android-Universal-Image-Loader)
* 使用步骤:
	1. 添加依赖: compile 'com.nostra13.universalimageloader:universal-image-loader:1.9.5'
	2. 添加权限:
	
		-　<uses-permission android:name="android.permission.INTERNET" />
		
		-　<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	3. 在Application或Activity中进行初始化配置
	
			// ImageLoaderConfiguration 详细配置
			File cacheDir = StorageUtils.getOwnCacheDirectory(getApplicationContext(), "imageloader/Cache"); // 自定义缓存文件夹
			ImageLoaderConfiguration config = new ImageLoaderConfiguration.Builder(context)
			     .memoryCacheExtraOptions(480, 800) // 指定缓存到内存时图片的大小,默认是屏幕尺寸的长宽
			     .diskCacheExtraOptions(480, 800, null) // 指定缓存到硬盘时图片的大小,并不建议使用
			     .taskExecutor(new Executor()) // 自定义一个线程来加载和显示图片
			     .taskExecutorForCachedImages(new Executor())// 自定义一个线程来缓存图片
			     .threadPoolSize(3) // default, 指定线程池大小
			     .threadPriority(Thread.NORM_PRIORITY - 2) // default ,指定线程优先级 
			     .tasksProcessingOrder(QueueProcessingType.FIFO) // default , 指定加载显示图片的任务队列的类型
			     .denyCacheImageMultipleSizesInMemory() // 禁止在内存中缓存同一张图片的多个尺寸类型
			     .memoryCache(new LruMemoryCache(2 * 1024 * 1024)) // 指定内存缓存的大小,默认值为1/8 应用的最大可用内存
			     .memoryCacheSize(2 * 1024 * 1024) 
			     .memoryCacheSizePercentage(13) // default
			     .diskCache(new UnlimitedDiskCache(cacheDir)) // default , 指定硬盘缓存的地址
			     .diskCacheSize(50 * 1024 * 1024) // 指定硬盘缓存的大小
			     .diskCacheFileCount(100) // 指定硬盘缓存的文件个数
			     .diskCacheFileNameGenerator(new HashCodeFileNameGenerator()) // default , 指定硬盘缓存时文件名的生成器
			     .imageDownloader(new BaseImageDownloader(context)) // default , 指定图片下载器
			     .imageDecoder(new BaseImageDecoder()) // default , 指定图片解码器
			     .defaultDisplayImageOptions(DisplayImageOptions.createSimple()) // default , 指定图片显示的配置
			     .writeDebugLogs() // 是否显示Log
			     .build();

			// ImageLoaderConfiguration 简单初始化
			ImageLoaderConfiguration configuration = ImageLoaderConfiguration.createDefault(this);
			// 初始化配置
			ImageLoader.getInstance().init(configuration);  

	4. DisplayImageOptions 参数详解:

			DisplayImageOptions options = new DisplayImageOptions.Builder()
				.showImageOnLoading(R.drawable.ic_stub) // 图片正在加载时显示的图片资源ID
				.showImageForEmptyUri(R.drawable.ic_empty) // URI为空时显示的图片资源ID
				.showImageOnFail(R.drawable.ic_error) // 图片加载失败时显示的图片资源ID
				.resetViewBeforeLoading(false)  // default 图片在下载前是否重置,复位
				.delayBeforeLoading(1000) // 图片开始加载前的延时.默认是0
				.cacheInMemory(false) // default , 是否缓存在内存中, 默认不缓存
				.cacheOnDisk(false) // default , 是否缓存在硬盘 , 默认不缓存
				.preProcessor(new BitmapProcessor) // 设置图片缓存在内存前的图片处理器
				.postProcessor(new BitmapProcessor) // 设置图片在缓存到内存以后 , 显示在界面之前的图片处理器
				.extraForDownloader(...) // 为图片下载设置辅助参数
				.considerExifParams(false) // default , 设置是否考虑JPEG图片的EXIF参数信息,默认不考虑
				.imageScaleType(ImageScaleType.IN_SAMPLE_POWER_OF_2) // default , 指定图片缩放的方式,ListView/GridView/Gallery推荐使用此默认值
				.bitmapConfig(Bitmap.Config.ARGB_8888) // default , 指定图片的质量,默认是 ARGB_8888
				.decodingOptions(...) // 指定图片的解码方式
				.displayer(new SimpleBitmapDisplayer()) // default , 设置图片显示的方式,用于自定义
				.handler(new Handler()) // default ,设置图片显示的方式和ImageLoadingListener的监听, 用于自定义
				.build();

	5. 显示图片的方法:

			ImageLoader.getInstance().loadImage(String uri, ImageLoadingListener listener)  
			
				displayImage(String uri, ImageView imageView)
				displayImage(String uri, ImageView imageView, DisplayImageOptions options)
				displayImage(String uri, ImageView imageView, DisplayImageOptions options,
					ImageLoadingListener listener, ImageLoadingProgressListener progressListener) 
	6. 特殊用法:
		1. 显示圆形图片.使用该效果,必须显式指定图片的宽高

				DisplayImageOptions options = new DisplayImageOptions.Builder()
				 		.displayer(new CircleBitmapDisplayer())
				 		.build();
		2. 显示圆角图片.使用该效果,必须显式指定图片的宽高
		
		        DisplayImageOptions options = new DisplayImageOptions.Builder()
		                .displayer(new RoundedBitmapDisplayer(90))
		                .build();
		3. 显示圆角缩放图片.使用该效果,必须显式指定图片的宽高

		        DisplayImageOptions options = new DisplayImageOptions.Builder()
		                .displayer(new RoundedVignetteBitmapDisplayer(90,180))
		                .build();
		4. 显示渐显图片

		        DisplayImageOptions options = new DisplayImageOptions.Builder()
		                .displayer(new FadeInBitmapDisplayer(3000))
		                .build();

### 3.2图像_Fresco	
* 主页: [https://github.com/facebook/fresco](https://github.com/facebook/fresco)
* 中文文档: [http://fresco-cn.org/docs/index.html](http://fresco-cn.org/docs/index.html)
* 使用步骤
	1. 添加依赖: compile 'com.facebook.fresco:fresco:0.9.0+'
	2. 添加权限 

			<uses-permission android:name="android.permission.INTERNET"/>
	3. 在Application初始化或在Activity 的setContentView()方法之前，进行初始化

        	Fresco.initialize(this);
	4. 在布局文件中添加图片控件.宽高必须显示指定,否则图片无法显示.

		    <com.facebook.drawee.view.SimpleDraweeView
		        android:id="@+id/my_image_view"
		        android:layout_width="200dp"
		        android:layout_height="200dp"
		        fresco:placeholderImage="@mipmap/ic_launcher" />
	5. 在Java代码中指定图片的路径.显示图片.SimpleDraweeView接收的路径参数为URI,所以需要一次转换.

	        Uri uri = Uri.parse(URL_IMG2);
	        SimpleDraweeView view = (SimpleDraweeView) findViewById(R.id.my_image_view);
	        view.setImageURI(uri);

	6. XML方式配置参数.除图片地址以外,其他所有显示选项都可以在布局文件中指定

		    <com.facebook.drawee.view.SimpleDraweeView
		        android:id="@+id/my_image_view"
		        android:layout_width="20dp"
		        android:layout_height="20dp"
		        fresco:actualImageScaleType="focusCrop"// 图片的缩放方式.
		        fresco:backgroundImage="@color/blue" //背景图.不支持缩放.XML仅能指定一张背景图.如果使用Java代码指定的话,可以指定多个背景,显示方式类似FrameLayout,多个背景图按照顺序一级一级层叠上去.
		        fresco:fadeDuration="300" // 渐显图片的时间
		        fresco:failureImage="@drawable/error" // 图片加载失败显示的图片
		        fresco:failureImageScaleType="centerInside" //// 图片加载失败显示的图片的缩放类型
		        fresco:overlayImage="@drawable/watermark" // 层叠图,最后叠加在图片之上.不支持缩放.XML仅能指定一张.如果使用Java代码指定的话,可以指定多个,显示方式类似FrameLayout,多个图按照顺序一级一级层叠上去.
		        fresco:placeholderImage="@color/wait_color"  // 图片加载成功之前显示的占位图
		        fresco:placeholderImageScaleType="fitCenter" // 图片加载成功之前显示的占位图的缩放类型
		        fresco:pressedStateOverlayImage="@color/red" // 设置按压状态下的层叠图.不支持缩放.
		        fresco:progressBarAutoRotateInterval="1000" // 进度条图片旋转显示时长
		        fresco:progressBarImage="@drawable/progress_bar" // 进度条图片
		        fresco:progressBarImageScaleType="centerInside" //进度条图片的缩放类型
		        fresco:retryImage="@drawable/retrying" // 当图片加载失败的时候,显示该图片提示用户点击重新加载图片
		        fresco:retryImageScaleType="centerCrop" // 提示图片的缩放类型
		        fresco:roundAsCircle="false" // 显示圆形图片
		        fresco:roundBottomLeft="false" // roundedCornerRadius属性设置后,四个角都会有圆角,如果左下角不需要设置为false.
		        fresco:roundBottomRight="true" // roundedCornerRadius属性设置后,四个角都会有圆角,如果右下角不需要设置为false.
		        fresco:roundTopLeft="true" // roundedCornerRadius属性设置后,四个角都会有圆角,如果左上角不需要设置为false.
		        fresco:roundTopRight="false" // roundedCornerRadius属性设置后,四个角都会有圆角,如果右上角不需要设置为false.
		        fresco:roundWithOverlayColor="@color/corner_color" // 设置图片圆角后空出区域的颜色.如示例图中的红色部分
		        fresco:roundedCornerRadius="1dp" // 设置图片圆角角度,设置该属性后四个角都会生效
		        fresco:roundingBorderColor="@color/border_color" // 设置圆角后,边框的颜色.
		        fresco:roundingBorderWidth="2dp" /> // 设置圆角后,外边框的宽高

![image](https://github.com/jaysonn/open-source-framework/blob/master/picture/57dba894318622563b000005.png)


	7. Java代码配置参数.
	
		        GenericDraweeHierarchy hierarchy = GenericDraweeHierarchyBuilder
		                .newInstance(getResources())
		                .setRetryImage(getResources().getDrawable(R.mipmap.ic_launcher))
		                .build();
		
		        imageivew.setHierarchy(hierarchy);

	8. 特殊用法:
	
		1. 显示渐进式JPEG图片

		        ProgressiveJpegConfig pjpegConfig = new ProgressiveJpegConfig() {
		            @Override
		            // 返回下一个需要解码的扫描次数
		            public int getNextScanNumberToDecode(int scanNumber) {
		                return scanNumber + 2;
		            }
		
		            // 确定多少个扫描次数之后的图片才能开始显示
		            public QualityInfo getQualityInfo(int scanNumber) {
		                boolean isGoodEnough = (scanNumber >= 5);
		                return ImmutableQualityInfo.of(scanNumber, isGoodEnough, false);
		            }
		        };
		        // ImagePipelineConfig配置如何加载图像
		        ImagePipelineConfig config = ImagePipelineConfig.newBuilder(this)
		                .setProgressiveJpegConfig(pjpegConfig)
		                .build();
		
		        img_uri = Uri.parse(URL_IMG2);
		        //  显式地指定允许渐进式JPEG图片加载
		        ImageRequest request = ImageRequestBuilder
		                .newBuilderWithSource(img_uri)
		                .setProgressiveRenderingEnabled(true)
		                .build();
		        // 构建显示图片所用到的DraweeController
		        DraweeController controller = Fresco.newDraweeControllerBuilder()
		                .setImageRequest(request)
		                .setOldController(simpleDraweeView.getController())
		                .build();
		
		        simpleDraweeView.setController(controller);

		2. 显示GIF图片.Fresco 支持 GIF 和 WebP 格式的动画图片.如果你希望图片下载完之后自动播放，同时，当View从屏幕移除时，停止播放，只需要在 image request 中简单设置，示例代码:

		        DraweeController controller = Fresco.newDraweeControllerBuilder()
		                .setUri(URL_GIF)
		                .setAutoPlayAnimations(true)
		                .build();
		        simpleDraweeView.setController(controller);

### 3.3图像_Picasso	
* 主页: [https://github.com/square/picasso](https://github.com/square/picasso)
* 使用步骤
	1. 添加依赖 compile 'com.squareup.picasso:picasso:2.5.2'
	2. 添加权限: 

			<uses-permission android:name="android.permission.INTERNET"/>
	3. 加载图片,示例代码:

			Picasso
	                .with(this)// 指定Context
	                .load(URL_IMG3) //指定图片URL
	                .placeholder(R.mipmap.ic_launcher) //指定图片未加载成功前显示的图片
	                .error(R.mipmap.ic_launcher)// 指定图片加载失败显示的图片
	                .resize(300, 300)// 指定图片的尺寸
	                .fit()// 指定图片缩放类型为fit
	                .centerCrop()// 指定图片缩放类型为centerCrop
	                .centerInside()// 指定图片缩放类型为centerInside
	                .memoryPolicy(MemoryPolicy.NO_CACHE, MemoryPolicy.NO_STORE)// 指定内存缓存策略
	                .priority(Picasso.Priority.HIGH)// 指定优先级
	                .into(imageView); // 指定显示图片的ImageView

	4. 显示圆形图片.示例代码:

		        // 自定义Transformation
		        Transformation transform = new Transformation() {
		            @Override
		            public Bitmap transform(Bitmap source) {
		                int size = Math.min(source.getWidth(), source.getHeight());
		                int x = (source.getWidth() - size) / 2;
		                int y = (source.getHeight() - size) / 2;
		                Bitmap squaredBitmap = Bitmap.createBitmap(source, x, y, size, size);
		                if (squaredBitmap != source) {
		                    source.recycle();
		                }
		                Bitmap bitmap = Bitmap.createBitmap(size, size, source.getConfig());
		                Canvas canvas = new Canvas(bitmap);
		                Paint paint = new Paint();
		                BitmapShader shader = new BitmapShader(squaredBitmap,
		                        BitmapShader.TileMode.CLAMP, BitmapShader.TileMode.CLAMP);
		                paint.setShader(shader);
		                paint.setAntiAlias(true);
		                float r = size / 2f;
		                canvas.drawCircle(r, r, r, paint);
		                squaredBitmap.recycle();
		                return bitmap;
		            }
		
		            @Override
		            public String key() {
		                return "circle";
		            }
		        };
		        Picasso
		                .with(this)// 指定Context
		                .load(URL_IMG2) //指定图片URL
		                .transform(transform) // 指定图片转换器
		                .into(imageView); // 指定显示图片的ImageView

	5. 显示圆角图片

			class RoundedTransformation implements com.squareup.picasso.Transformation {
			    private final int radius;
			    private final int margin;  // dp
			
			    // radius is corner radii in dp
			    // margin is the board in dp
			    public RoundedTransformation(final int radius, final int margin) {
			        this.radius = radius;
			        this.margin = margin;
			    }
			
			    @Override
			    public Bitmap transform(final Bitmap source) {
			        final Paint paint = new Paint();
			        paint.setAntiAlias(true);
			        paint.setShader(new BitmapShader(source, Shader.TileMode.CLAMP, Shader.TileMode.CLAMP));
			
			        Bitmap output = Bitmap.createBitmap(source.getWidth(), source.getHeight(), Bitmap.Config.ARGB_8888);
			        Canvas canvas = new Canvas(output);
			        canvas.drawRoundRect(new RectF(margin, margin, source.getWidth() - margin, source.getHeight() - margin), radius, radius, paint);
			
			        if (source != output) {
			            source.recycle();
			        }
			
			        return output;
			    }
			
			    @Override
			    public String key() {
			        return "rounded(radius=" + radius + ", margin=" + margin + ")";
			    }
			}
	        Picasso
	                .with(this)// 指定Context
	                .load(URL_IMG2) //指定图片URL
	                .transform(new RoundedTransformation(360,0)) // 指定图片转换器
	                .into(imageView); // 指定显示图片的ImageView
### 3.4图像_Glide	
* 主页: [https://github.com/bumptech/glide](https://github.com/bumptech/glide)
* 中文文档: [http://mrfu.me/2016/02/27/Glide_Getting_Started/](http://mrfu.me/2016/02/27/Glide_Getting_Started/)
* 使用步骤
	1. 添加依赖 compile 'com.github.bumptech.glide:glide:3.7.0' , 同时还依赖于supportV4.如果没有请自行添加
	2. 添加权限: 

			<uses-permission android:name="android.permission.INTERNET"/>

	3. 加载图片.示例代码:

	        Glide
	                .with(this) // 指定Context
	                .load(URL_GIF)// 指定图片的URL
	                .placeholder(R.mipmap.ic_launcher)// 指定图片未成功加载前显示的图片
	                .error(R.mipmap.ic_launcher)// 指定图片加载失败显示的图片
	                .override(300, 300)//指定图片的尺寸
	                .fitCenter()//指定图片缩放类型为fitCenter
	                .centerCrop()// 指定图片缩放类型为centerCrop
	                .skipMemoryCache(true)// 跳过内存缓存
	                .diskCacheStrategy(DiskCacheStrategy.NONE)//跳过磁盘缓存
	                .diskCacheStrategy(DiskCacheStrategy.SOURCE)//仅仅只缓存原来的全分辨率的图像
	                .diskCacheStrategy(DiskCacheStrategy.RESULT)//仅仅缓存最终的图像
	                .diskCacheStrategy(DiskCacheStrategy.ALL)//缓存所有版本的图像
	                .priority(Priority.HIGH)//指定优先级.Glide 将会用他们作为一个准则，并尽可能的处理这些请求，但是它不能保证所有的图片都会按照所要求的顺序加载。优先级排序:IMMEDIATE > HIGH > NORMAL >　LOW
	                .into(imageView);//指定显示图片的ImageView
	4. 显示圆形图片

			class GlideCircleTransform extends BitmapTransformation {
			    public GlideCircleTransform(Context context) {
			        super(context);
			    }
			
			    @Override
			    protected Bitmap transform(BitmapPool pool, Bitmap toTransform, int outWidth, int outHeight) {
			        return circleCrop(pool, toTransform);
			    }
			
			    private static Bitmap circleCrop(BitmapPool pool, Bitmap source) {
			        if (source == null) return null;
			
			        int size = Math.min(source.getWidth(), source.getHeight());
			        int x = (source.getWidth() - size) / 2;
			        int y = (source.getHeight() - size) / 2;
			
			        // TODO this could be acquired from the pool too
			        Bitmap squared = Bitmap.createBitmap(source, x, y, size, size);
			
			        Bitmap result = pool.get(size, size, Bitmap.Config.ARGB_8888);
			        if (result == null) {
			            result = Bitmap.createBitmap(size, size, Bitmap.Config.ARGB_8888);
			        }
			
			        Canvas canvas = new Canvas(result);
			        Paint paint = new Paint();
			        paint.setShader(new BitmapShader(squared, BitmapShader.TileMode.CLAMP, BitmapShader.TileMode.CLAMP));
			        paint.setAntiAlias(true);
			        float r = size / 2f;
			        canvas.drawCircle(r, r, r, paint);
			        return result;
			    }
			
			    @Override
			    public String getId() {
			        return getClass().getName();
			    }
			}

	        Glide
	                .with(this) // 指定Context
	                .load(URL_GIF)// 指定图片的URL
	                .transform(new GlideCircleTransform(this)) // 指定自定义BitmapTransformation
	                .into(imageView);//指定显示图片的ImageView

	5. 显示圆角图片

			class GlideRoundTransform extends BitmapTransformation {
			
			    private static float radius = 0f;
			
			    public GlideRoundTransform(Context context) {
			        this(context, 4);
			    }
			
			    public GlideRoundTransform(Context context, int dp) {
			        super(context);
			        this.radius = Resources.getSystem().getDisplayMetrics().density * dp;
			    }
			
			    @Override protected Bitmap transform(BitmapPool pool, Bitmap toTransform, int outWidth, int outHeight) {
			        return roundCrop(pool, toTransform);
			    }
			
			    private static Bitmap roundCrop(BitmapPool pool, Bitmap source) {
			        if (source == null) return null;
			
			        Bitmap result = pool.get(source.getWidth(), source.getHeight(), Bitmap.Config.ARGB_8888);
			        if (result == null) {
			            result = Bitmap.createBitmap(source.getWidth(), source.getHeight(), Bitmap.Config.ARGB_8888);
			        }
			
			        Canvas canvas = new Canvas(result);
			        Paint paint = new Paint();
			        paint.setShader(new BitmapShader(source, BitmapShader.TileMode.CLAMP, BitmapShader.TileMode.CLAMP));
			        paint.setAntiAlias(true);
			        RectF rectF = new RectF(0f, 0f, source.getWidth(), source.getHeight());
			        canvas.drawRoundRect(rectF, radius, radius, paint);
			        return result;
			    }
			
			    @Override public String getId() {
			        return getClass().getName() + Math.round(radius);
			    }
			}

	        Glide
	                .with(this) // 指定Context
	                .load(URL_GIF)// 指定图片的URL
	                .transform(new GlideRoundTransform(this,30)) // 指定自定义BitmapTransformation
	                .into(imageView);//指定显示图片的ImageView

	6. 更改Glide默认配置的步骤:
		1. 创建一个GlideModule的实现类,并在其中更改自己需要的设置.示例代码:

				public class SimpleGlideModule implements GlideModule {
				    @Override
				    public void applyOptions(Context context, GlideBuilder builder) {
				        // 更改Bitmap图片压缩质量为8888,默认为565
				        builder.setDecodeFormat(DecodeFormat.PREFER_ARGB_8888);
				    }
				
				    @Override
				    public void registerComponents(Context context, Glide glide) {
				        // todo
				    }
				}
		2. 在manifet/Application中添加一个meta-data节点.name值为刚刚创建的GlideModule实现类的完整包名+类名,value值为GlideModule.示例代码:

		        <meta-data
		            android:name="com.alpha.glidedemo.SimpleGlideModule"
		            android:value="GlideModule" />
		3. 之后Glide加载图片的时候将会按照新的设置加载.

###图像库对比
* 快速加载图片推荐Glide
* 对图片质量要求较高推荐Picasso
* 如果应用加载的图片很多,推荐Fresco > Glide > Picasso

![image](https://github.com/jaysonn/open-source-framework/blob/master/picture/57dba8c0318622563b000006.png)
