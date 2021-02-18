# Retrofit

## 集成

```groovy
implementation 'com.squareup.retrofit2:retrofit:2.4.0'
implementation 'com.squareup.retrofit2:converter-gson:2.4.0'
implementation 'com.google.code.gson:gson:2.8.6'
implementation 'io.reactivex.rxjava2:rxandroid:2.1.0'
implementation 'com.squareup.okhttp3:logging-interceptor:3.11.0'
implementation 'com.squareup.retrofit2:adapter-rxjava2:2.4.0'
```
## 官网资源
- [github地址](https://github.com/square/retrofit)
- [官方文档](https://square.github.io/retrofit/)

## 使用步骤
### 1、建立接口
```
public interface RetService {

    @Headers({"","",""})
    @GET("/")
    Call<ResponseBody> getBaiduDu();
}
```

### 2、构建Retrofit对象
```
Retrofit retrofit=new Retrofit.Builder().baseUrl("https://www.baidu.com").build();
```

### 3、获取代理对象
```
RetService service = retrofit.create(RetService.class);
```
### 4、发起请求
```
Call<ResponseBody> baiduDu = service.getBaiduDu();
```
### 5、获取结果
```
// 1、异步
baiduDu.enqueue(new Callback<ResponseBody>() {
            @Override
            public void onResponse(Call<ResponseBody> call, Response<ResponseBody> response) {
                try {
                    Log.d("ddd",response.body().string());
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

            @Override
            public void onFailure(Call<ResponseBody> call, Throwable t) {

            }
        });
        
// 2、同步
Response<ResponseBody> execute = baiduDu.execute();
execute.body().string()
```

## 例子

### 初始化 

```java
package com.shoukong.umpsky.manager.net.http;

import com.shoukong.umpsky.Constants;
import com.shoukong.umpsky.utils.LogUtil;

import java.io.IOException;
import java.util.concurrent.TimeUnit;

import okhttp3.Interceptor;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import okhttp3.logging.HttpLoggingInterceptor;
import retrofit2.Retrofit;
import retrofit2.adapter.rxjava2.RxJava2CallAdapterFactory;
import retrofit2.converter.gson.GsonConverterFactory;

/**
 * author : lijie
 * date : 2019/12/5 10:24
 * e-mail : jackyli706@gmail.com
 * description :
 * <p>
 * 针对大图片或者大文件，使用拦截器拦截日志的话只保留header日志
 * 不然会导致OutOfMemory异常
 * 参考解决方案  https://blog.csdn.net/jklwan/article/details/101002449
 * <p>
 * 参考：https://www.jianshu.com/p/2e8b400909b7
 */
public class RetrofitManager {

    private static Retrofit retrofit;

    //Log日志
    private HttpLoggingInterceptor loggingInterceptor = new HttpLoggingInterceptor(new HttpLoggingInterceptor.Logger() {
        @Override
        public void log(String message) {
            LogUtil.e("HTTP请求日志:" + message);
        }
    }).setLevel(HttpLoggingInterceptor.Level.BODY);

    //Ok的拦截器
    private OkHttpClient okHttpClient() {
        loggingInterceptor.setLevel(HttpLoggingInterceptor.Level.BODY);

        return new OkHttpClient.Builder()
                .writeTimeout(3, TimeUnit.SECONDS)
                .connectTimeout(3, TimeUnit.SECONDS)
                .readTimeout(3, TimeUnit.SECONDS)
                .retryOnConnectionFailure(false)
                .addInterceptor(loggingInterceptor)
                //自定义连接池最大空闲连接数和等待时间大小，否则默认最大5个空闲连接
                // .connectionPool(new ConnectionPool(32, 5, TimeUnit.MINUTES))
//                .addInterceptor(new Interceptor() {
//                    @Override
//                    public Response intercept(Chain chain) throws IOException {
//                        Request request = chain.request()
//                                .newBuilder()
//                                // .addHeader("Content-Type", "application/x-www-form-urlencoded; charset=UTF-8")
//                                // .addHeader("Accept-Encoding", "gzip, deflate")
//                                .addHeader("Connection", "close")
//                                // .addHeader("Accept", "*/*")
//                                // .addHeader("Cookie", "add cookies here")
//                                .build();
//                        return chain.proceed(request);
//                    }
//                })
                .build();

        //Retrofit的使用
    }

    private RetrofitManager() {
        retrofit = new Retrofit.Builder()
                .addCallAdapterFactory(RxJava2CallAdapterFactory.create())
                .addConverterFactory(GsonConverterFactory.create())
                .baseUrl(Constants.HTTP_URL + "/")
                .client(okHttpClient())
                .build();
    }

    public static Retrofit get() {
        if (retrofit == null) {
            new RetrofitManager();
        }
        return retrofit;
    }

    public <T> T create(Class<T> clazz) {
        return retrofit.create(clazz);
    }

}
```

### ApiService

```java
/**
 * author : lijie
 * date : 2019/12/5 10:29
 * e-mail : jackyli706@gmail.com
 * description :
 */
public interface ApiService {
    
    /**
    普通POST请求（请求json的数据）
    请求数据：UMSIdentifyMsg为对象映射为json
    回复数据：json映射为ResponseMsg对象
    **/
    @POST("ums/UMSIdentify")
    @Headers("Content-Type:application/json; charset=utf-8")
    Call<ResponseMsg> umsIdentify(@Body UMSIdentifyMsg UMSIdentifyMsg);

    /**
    以下是RxJava+Retrofit
    **/
    //Get请求
    @GET("gds/GDSHeart")
    Observable<ResponseMsg> connectSaas();

    /**
     *  多张图片上传
       RequestBody requestBody[] = new RequestBody[picPath.length];
       for (int i = 0; i < picPath.length; i++) {
            requestBody[i] = RequestBody.create(MediaType.parse("multipart/form-data"), picPath[i]);
        }
        MultipartBody.Part[] part = new MultipartBody.Part[requestBody.length];
        for (int i = 0; i < requestBody.length; i++) {
            part[i] = MultipartBody.Part.createFormData("picture", picPath[i].getName(), requestBody[i]);
        }
        return RetrofitManager.get().create(ApiService.class).uploadPic(part);
     */
    @Multipart
    @POST("gds/GDSTaskPic")
        //防止乱码
    Observable<ResponseMsg> uploadPic(@Part MultipartBody.Part[] file);

    //Post请求
    @POST("gds/GDSTaskStart")
    @Headers("Content-Type:application/json; charset=utf-8")
        //防止乱码
    Observable<ResponseMsg> taskStart(@Body TaskStartMsg taskStartMsg);
    
    //在子线程网络请求主线程更新UI
    mainModel.connectSaas().subscribeOn(Schedulers.io())
                    .observeOn(AndroidSchedulers.mainThread())
                    .subscribe(responseMsg -> {
                        if (mView == null) {
                            LogUtil.d("connectSaas----Success" + ":" + "mView is NULL");
                            return;
                        }
                        mView.hideLoading();
                        mView.connectSaasSuccess(responseMsg);
                    }, throwable -> {
                        if (mView == null) {
                            LogUtil.d("connectSaas----Fail" + ":" + "mView is NULL");
                            return;
                        }
                        mView.hideLoading();
                        if (throwable == null) {
                            mView.connectSaasFail("展示数据失败");
                        } else {
                            mView.connectSaasFail(throwable.getMessage());
                        }
                    });

}
```

