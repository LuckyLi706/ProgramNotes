# Volley

## 使用

```java
package com.lucky.newsandroid.network;

import android.content.Context;
import android.graphics.Bitmap;
import android.util.LruCache;
import android.widget.ImageView;

import com.android.volley.AuthFailureError;
import com.android.volley.DefaultRetryPolicy;
import com.android.volley.RequestQueue;
import com.android.volley.Response;
import com.android.volley.VolleyError;
import com.android.volley.toolbox.ImageLoader;
import com.android.volley.toolbox.ImageRequest;
import com.android.volley.toolbox.JsonObjectRequest;
import com.android.volley.toolbox.StringRequest;
import com.android.volley.toolbox.Volley;
import com.lucky.newsandroid.R;

import org.json.JSONObject;

import java.util.Map;

/**
 * 作者：jacky on 2019/9/24 12:23
 * 邮箱：jackyli706@gmail.com
 */
public class VolleyManager {

    private static VolleyManager volleyManager;
    private int timeout = 2000;
    private int maxretry = 0;
    private float backoff = 0f;
    private Map<String, String> map;
    private boolean isCahce;

    private RequestQueue queue;

    private VolleyManager() {
    }

    public static VolleyManager getInstance() {
        if (volleyManager == null) {
            synchronized (VolleyManager.class) {
                if (volleyManager == null) {
                    volleyManager = new VolleyManager();
                }
            }
        }
        return volleyManager;
    }

    //初始化Volley
    public void initVolley(Context context) {
        queue = Volley.newRequestQueue(context.getApplicationContext());
    }

    //设置超时策略
    public void setRetry(int timeout, int maxretry, float backoff) {
        this.timeout = timeout;
        this.maxretry = maxretry;
        this.backoff = backoff;
    }

    //设置请求头
    public void setHeader(Map<String, String> map) {
        this.map = map;
    }

    //设置缓存
    public void setShouldCache(boolean isCache) {
        this.isCahce = isCache;
    }

    //请求字符串数据
    public void getString(int method, String url, Result<String> result) {
        StringRequest stringRequest = new StringRequest(method, url, new Response.Listener<String>() {
            @Override
            public void onResponse(String response) {
                result.onSuccess(response);
            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                result.onError(error);
            }
        }) {
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {
                return map;
            }
        };
        stringRequest.setRetryPolicy(new DefaultRetryPolicy(timeout, maxretry, backoff));
        stringRequest.setShouldCache(isCahce);
        queue.add(stringRequest);
    }

    //请求Json数据
    public void getJson(int method, String url, String requestBody, Result<JSONObject> result) {

        JsonObjectRequest jsonObjectRequest = new JsonObjectRequest(method, url, requestBody, new Response.Listener<JSONObject>() {
            @Override
            public void onResponse(JSONObject response) {
                result.onSuccess(response);
            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                result.onError(error);
            }
        }) {
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {
                return map;
            }
        };
        jsonObjectRequest.setRetryPolicy(new DefaultRetryPolicy(timeout, maxretry, backoff));
        jsonObjectRequest.setShouldCache(isCahce);
        queue.add(jsonObjectRequest);
    }

    //请求图片数据
    public void getImage(String url, Result<Bitmap> result) {

        ImageRequest imageRequest = new ImageRequest(url, new Response.Listener<Bitmap>() {
            @Override
            public void onResponse(Bitmap response) {
                result.onSuccess(response);
            }
        }, 0, 0, Bitmap.Config.RGB_565, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                result.onError(error);
            }
        }) {
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {
                return map;
            }
        };
        imageRequest.setRetryPolicy(new DefaultRetryPolicy(timeout, maxretry, backoff));
        imageRequest.setShouldCache(isCahce);
        queue.add(imageRequest);
    }

    /**
     * ImageLoader的内部使用ImageRequest来实现，
     * 它的构造器可以传入一个ImageCache缓存形参，
     * 实现了图片缓存的功能，同时还可以过滤重复链接，
     * 避免重复发送请求
     *
     * @param url
     */
    public void useImageLoader(String url, ImageView imageView) {
        ImageLoader imageLoader = new ImageLoader(queue, new BitmapCache());
        ImageLoader.ImageListener listener = ImageLoader.getImageListener(imageView, R.mipmap.ic_launcher, R.mipmap.ic_launcher);
        imageLoader.get(url, listener);
    }

    /**
     * NetworkImageView是一个自定义控件，继承自ImageView，封装了请求网络加载图片的功能。
     * 先在布局中引用：
     * <com.android.volley.toolbox.NetworkImageView
     * android:id="@+id/nv_image"
     * android:layout_width="200dp"
     * android:layout_height="200dp"
     * android:layout_centerHorizontal="true"
     * android:layout_below="@id/iv_image"
     * android:layout_marginTop="20dp"
     * ></com.android.volley.toolbox.NetworkImageView>
     * 代码中使用:
     * iv_image = (ImageView) this.findViewById(R.id.iv_image);
     * RequestQueue mQueue = Volley.newRequestQueue(getApplicationContext());
     * ImageLoader imageLoader = new ImageLoader(mQueue, new BitmapCache());
     * nv_image.setDefaultImageResId(R.drawable.ico_default);
     * nv_image.setErrorImageResId(R.drawable.ico_default);
     * nv_image.setImageUrl("http://img.my.csdn.net/uploads/201603/26/1458988468_5804.jpg",
     * imageLoader);
     * NetworkImageView并没有提供设置最大宽度和高度的方法，根据我们设置控件的宽和高结合网络图片的宽和高内部会自动去实现压缩，
     * 如果我们不想要压缩可以设置NetworkImageView控件的宽和高都为wrap_content。
     */

    private class BitmapCache implements ImageLoader.ImageCache {

        LruCache<String, Bitmap> cache;
        int max = 10 * 1024 * 1024;

        BitmapCache() {
            cache = new LruCache<String, Bitmap>(max) {
                @Override
                protected int sizeOf(String key, Bitmap value) {
                    return value.getRowBytes() * value.getHeight();
                }
            };
        }

        @Override
        public Bitmap getBitmap(String url) {
            return cache.get(url);
        }

        @Override
        public void putBitmap(String url, Bitmap bitmap) {
            cache.put(url, bitmap);
        }
    }

    public void cancelAllRequest() {
        queue.cancelAll(this);
    }

    public interface Result<T> {

        void onSuccess(T response);

        void onError(Exception e);
    }
}

```

## 源码解析

### 结构图
![image](https://s2.ax1x.com/2019/05/29/VuBtde.png)
从上图可以看到Volley分为三个线程，分别是主线程、缓存调度线程、和网络调度线程，首先请求会加入缓存队列，如果发现可以找到相应的缓存结果就直接读取缓存并解析，然后回调给主线程；如果在缓存中没有找到结果，则将这条请求加入到网络队列中，然后发送HTTP请求，解析响应并写入缓存，并回调给主线程。

### 从RequestQueue入手
我们都知道使用Volley之前首先要创建RequestQueue：
```
RequestQueue mQueue = Volley.newRequestQueue(getApplicationContext());
```
这也是volley运作的入口，看看newRequestQueue：
```
 public static RequestQueue newRequestQueue(Context context) {
        return newRequestQueue(context, (HttpStack)null);
    }

public static RequestQueue newRequestQueue(Context context, HttpStack stack) {
        return newRequestQueue(context, stack, -1);
    }
```
连续调用了两个重载函数，最终调用的是：
```
public static RequestQueue newRequestQueue(Context context, HttpStack stack, int maxDiskCacheBytes) {
        File cacheDir = new File(context.getCacheDir(), "volley");
        String userAgent = "volley/0";

        try {
            String network = context.getPackageName();
            PackageInfo queue = context.getPackageManager().getPackageInfo(network, 0);
            userAgent = network + "/" + queue.versionCode;
        } catch (NameNotFoundException var7) {
            ;
        }

        if(stack == null) {
            if(VERSION.SDK_INT >= 9) {
                stack = new HurlStack();
            } else {
                stack = new HttpClientStack(AndroidHttpClient.newInstance(userAgent));
            }
        }

        BasicNetwork network1 = new BasicNetwork((HttpStack)stack);
        RequestQueue queue1;
        if(maxDiskCacheBytes <= -1) {
            queue1 = new RequestQueue(new DiskBasedCache(cacheDir), network1);
        } else {
            queue1 = new RequestQueue(new DiskBasedCache(cacheDir, maxDiskCacheBytes), network1);
        }

        queue1.start();
        return queue1;
    }
```
可以看到如果android版本大于等于2.3则调用基于HttpURLConnection的HurlStack，否则就调用基于HttpClient的HttpClientStack。并创建了RequestQueue，调用了start()方法：
```
public void start() {
      this.stop();
      this.mCacheDispatcher = new CacheDispatcher(this.mCacheQueue, this.mNetworkQueue, this.mCache, this.mDelivery);
      this.mCacheDispatcher.start();

      for(int i = 0; i < this.mDispatchers.length; ++i) {
          NetworkDispatcher networkDispatcher = new NetworkDispatcher(this.mNetworkQueue, this.mNetwork, this.mCache, this.mDelivery);
          this.mDispatchers[i] = networkDispatcher;
          networkDispatcher.start();
      }

  }
```
CacheDispatcher是缓存调度线程，并调用了start()方法，在循环中调用了NetworkDispatcher的start()方法，NetworkDispatcher是网络调度线程，默认情况下mDispatchers.length为4，默认开启了4个网络调度线程，也就是说有5个线程在后台运行并等待请求的到来。接下来我们创建各种的Request，并调用RequestQueue的add()方法：
```
public <T> Request<T> add(Request<T> request) {
       request.setRequestQueue(this);
       Set var2 = this.mCurrentRequests;
       synchronized(this.mCurrentRequests) {
           this.mCurrentRequests.add(request);
       }

       request.setSequence(this.getSequenceNumber());
       request.addMarker("add-to-queue");
       //如果不能缓存，则将请求添加到网络请求队列中
       if(!request.shouldCache()) {
           this.mNetworkQueue.add(request);
           return request;
       } else {
           Map var8 = this.mWaitingRequests;
           synchronized(this.mWaitingRequests) {
               String cacheKey = request.getCacheKey();
       
      //之前是否有执行相同的请求且还没有返回结果的，如果有的话将此请求加入mWaitingRequests队列，不再重复请求
               if(this.mWaitingRequests.containsKey(cacheKey)) {
                   Object stagedRequests = (Queue)this.mWaitingRequests.get(cacheKey);
                   if(stagedRequests == null) {
                       stagedRequests = new LinkedList();
                   }

                   ((Queue)stagedRequests).add(request);
                   this.mWaitingRequests.put(cacheKey, stagedRequests);
                   if(VolleyLog.DEBUG) {
                       VolleyLog.v("Request for cacheKey=%s is in flight, putting on hold.", new Object[]{cacheKey});
                   }
               } else {
  //没有的话就将请求加入缓存队列mCacheQueue，同时加入mWaitingRequests中用来做下次同样请求来时的重复判断依据
                   this.mWaitingRequests.put(cacheKey, (Object)null);
                   this.mCacheQueue.add(request);
               }

               return request;
           }
       }
   }
```
通过判断request.shouldCache()，来判断是否可以缓存，默认是可以缓存的，如果不能缓存，则将请求添加到网络请求队列中，如果能缓存就判断之前是否有执行相同的请求且还没有返回结果的，如果有的话将此请求加入mWaitingRequests队列，不再重复请求；没有的话就将请求加入缓存队列mCacheQueue，同时加入mWaitingRequests中用来做下次同样请求来时的重复判断依据。
从上面可以看出RequestQueue的add()方法并没有做什么请求网络或者对缓存进行操作。当将请求添加到网络请求队列或者缓存队列时，这时在后台的网络调度线程和缓存调度线程轮询各自的请求队列发现有请求任务则开始执行，我们先看看缓存调度线程。

### CacheDispatcher缓存调度线程
CacheDispatcher的run()方法：

```java
public void run() {
    if(DEBUG) {
        VolleyLog.v("start new dispatcher", new Object[0]);
    }
    //线程优先级设置为最高级别
    Process.setThreadPriority(10);
    this.mCache.initialize();

    while(true) {
        while(true) {
            while(true) {
                while(true) {
                    try {
                    //获取缓存队列中的一个请求
                        final Request e = (Request)this.mCacheQueue.take();
                        e.addMarker("cache-queue-take");
                        //如果请求取消了则将请求停止掉
                        if(e.isCanceled()) {
                            e.finish("cache-discard-canceled");
                        } else {
                        //查看是否有缓存的响应
                            Entry entry = this.mCache.get(e.getCacheKey());
                            //如果缓存响应为空，则将请求加入网络请求队列
                            if(entry == null) {
                                e.addMarker("cache-miss");
                                this.mNetworkQueue.put(e);
                            //判断缓存响应是否过期    
                            } else if(!entry.isExpired()) {
                                e.addMarker("cache-hit");
                                //对数据进行解析并回调给主线程
                                Response response = e.parseNetworkResponse(new NetworkResponse(entry.data, entry.responseHeaders));
                                e.addMarker("cache-hit-parsed");
                                if(!entry.refreshNeeded()) {
                                    this.mDelivery.postResponse(e, response);
                                } else {
                                    e.addMarker("cache-hit-refresh-needed");
                                    e.setCacheEntry(entry);
                                    response.intermediate = true;
                                    this.mDelivery.postResponse(e, response, new Runnable() {
                                        public void run() {
                                            try {
                                                CacheDispatcher.this.mNetworkQueue.put(e);
                                            } catch (InterruptedException var2) {
                                                ;
                                            }

                                        }
                                    });
                                }
                            } else {
                                e.addMarker("cache-hit-expired");
                                e.setCacheEntry(entry);
                                this.mNetworkQueue.put(e);
                            }
                        }
                    } catch (InterruptedException var4) {
                        if(this.mQuit) {
                            return;
                        }
                    }
                }
            }
        }
    }
}

static {
    DEBUG = VolleyLog.DEBUG;
}
```

看到四个while循环有些晕吧，让我们挑重点的说，首先从缓存队列取出请求，判断是否请求是否被取消了，如果没有则判断该请求是否有缓存的响应，如果有并且没有过期则对缓存响应进行解析并回调给主线程。接下来看看网络调度线程。

### NetworkDispatcher网络调度线程
NetworkDispatcher的run()方法：

```java
public void run() {
       Process.setThreadPriority(10);

       while(true) {
           long startTimeMs;
           Request request;
           while(true) {
               startTimeMs = SystemClock.elapsedRealtime();

               try {
               //从队列中取出请求
                   request = (Request)this.mQueue.take();
                   break;
               } catch (InterruptedException var6) {
                   if(this.mQuit) {
                       return;
                   }
               }
           }

           try {
               request.addMarker("network-queue-take");
               if(request.isCanceled()) {
                   request.finish("network-discard-cancelled");
               } else {
                   this.addTrafficStatsTag(request);
                   //请求网络
                   NetworkResponse e = this.mNetwork.performRequest(request);
                   request.addMarker("network-http-complete");
                   if(e.notModified && request.hasHadResponseDelivered()) {
                       request.finish("not-modified");
                   } else {
                       Response volleyError1 = request.parseNetworkResponse(e);
                       request.addMarker("network-parse-complete");
                       if(request.shouldCache() && volleyError1.cacheEntry != null) {                         
                           //将响应结果存入缓存
                           this.mCache.put(request.getCacheKey(), volleyError1.cacheEntry);
                           request.addMarker("network-cache-written");
                       }

                       request.markDelivered();
                       this.mDelivery.postResponse(request, volleyError1);
                   }
               }
           } catch (VolleyError var7) {
               var7.setNetworkTimeMs(SystemClock.elapsedRealtime() - startTimeMs);
               this.parseAndDeliverNetworkError(request, var7);
           } catch (Exception var8) {
               VolleyLog.e(var8, "Unhandled exception %s", new Object[]{var8.toString()});
               VolleyError volleyError = new VolleyError(var8);
               volleyError.setNetworkTimeMs(SystemClock.elapsedRealtime() - startTimeMs);
               this.mDelivery.postError(request, volleyError);
           }
       }
   }
```

网络调度线程也是从队列中取出请求并且判断是否被取消了，如果没取消就去请求网络得到响应并回调给主线程。请求网络时调用this.mNetwork.performRequest(request)，这个mNetwork是一个接口，实现它的类是BasicNetwork，我们来看看BasicNetwork的performRequest()方法：

```java
public NetworkResponse performRequest(Request<?> request) throws VolleyError {
        long requestStart = SystemClock.elapsedRealtime();

        while(true) {
            HttpResponse httpResponse = null;
            Object responseContents = null;
            Map responseHeaders = Collections.emptyMap();

            try {
                HashMap e = new HashMap();
                this.addCacheHeaders(e, request.getCacheEntry());
                httpResponse = this.mHttpStack.performRequest(request, e);
                StatusLine statusCode1 = httpResponse.getStatusLine();
                int networkResponse1 = statusCode1.getStatusCode();
                responseHeaders = convertHeaders(httpResponse.getAllHeaders());
                if(networkResponse1 == 304) {
                    Entry requestLifetime2 = request.getCacheEntry();
                    if(requestLifetime2 == null) {
                        return new NetworkResponse(304, (byte[])null, responseHeaders, true, SystemClock.elapsedRealtime() - requestStart);
                    }

                    requestLifetime2.responseHeaders.putAll(responseHeaders);
                    return new NetworkResponse(304, requestLifetime2.data, requestLifetime2.responseHeaders, true, SystemClock.elapsedRealtime() - requestStart);
                }


...省略
```

从上面可以看到在12行调用的是HttpStack的performRequest()方法请求网络，接下来根据不同的响应状态码来返回不同的NetworkResponse。另外HttpStack也是一个接口，实现它的两个类我们在前面已经提到了就是HurlStack和HttpClientStack。让我们再回到NetworkDispatcher，请求网络后，会将响应结果存在缓存中，如果响应结果成功则调用this.mDelivery.postResponse(request, volleyError1)来回调给主线程。来看看Delivery的postResponse()方法：

```java
public void postResponse(Request<?> request, Response<?> response, Runnable runnable) {
       request.markDelivered();
       request.addMarker("post-response");
       this.mResponsePoster.execute(new ExecutorDelivery.ResponseDeliveryRunnable(request, response, runnable));
   }
```

来看看ResponseDeliveryRunnable里面做了什么：

```java
private class ResponseDeliveryRunnable implements Runnable {
       private final Request mRequest;
       private final Response mResponse;
       private final Runnable mRunnable;

       public ResponseDeliveryRunnable(Request request, Response response, Runnable runnable) {
           this.mRequest = request;
           this.mResponse = response;
           this.mRunnable = runnable;
       }

       public void run() {
           if(this.mRequest.isCanceled()) {
               this.mRequest.finish("canceled-at-delivery");
           } else {
               if(this.mResponse.isSuccess()) {
                   this.mRequest.deliverResponse(this.mResponse.result);
               } else {
                   this.mRequest.deliverError(this.mResponse.error);
               }

               if(this.mResponse.intermediate) {
                   this.mRequest.addMarker("intermediate-response");
               } else {
                   this.mRequest.finish("done");
               }

               if(this.mRunnable != null) {
                   this.mRunnable.run();
               }

           }
       }
   }
```

第17行调用了this.mRequest.deliverResponse(this.mResponse.result)，这个就是实现Request抽象类必须要实现的方法，我们来看看StringRequest的源码：

```java
public class StringRequest extends Request<String> {
    private final Listener<String> mListener;

    public StringRequest(int method, String url, Listener<String> listener, ErrorListener errorListener) {
        super(method, url, errorListener);
        this.mListener = listener;
    }

    public StringRequest(String url, Listener<String> listener, ErrorListener errorListener) {
        this(0, url, listener, errorListener);
    }

    protected void deliverResponse(String response) {
        this.mListener.onResponse(response);
    }

 ...省略
}
```

在deliverResponse方法中调用了this.mListener.onResponse(response)，最终将response回调给了Response.Listener的onResponse()方法。我们用StringRequest请求网络的写法是这样的：

```java
RequestQueue mQueue = Volley.newRequestQueue(getApplicationContext());
        StringRequest mStringRequest = new StringRequest(Request.Method.GET, "http://www.baidu.com",
                new Response.Listener<String>() {
                    @Override
                    public void onResponse(String response) {
                        Log.i("wangshu", response);
                    }
                }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                Log.e("wangshu", error.getMessage(), error);
            }
        });
        //将请求添加在请求队列中
        mQueue.add(mStringRequest);
```