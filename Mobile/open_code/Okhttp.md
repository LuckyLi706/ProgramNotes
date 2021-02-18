# Okhttp

## 集成
```
implementation 'com.squareup.okhttp3:okhttp:3.10.0'
```

## 官方资源
- [github地址](https://github.com/square/okhttp)
- [官方文档](hhttps://square.github.io/okhttp/)

## 使用步骤
### 1、创建OkHttpClient实例
三种方法：
- 创建一个默认配置OkHttpClient，可以使用默认的构造函数。
- 通过new OkHttpClient.Builder()方法来一步一步配置一个OkHttpClient实例。
- 如果要求使用现有的实例，可以通过newBuilder()方法来进行构造
```
//配置说明
Dispatcher dispatcher;          // 分发
Proxy proxy;                    // 代理
List<Protocol> protocols;
List<ConnectionSpec> connectionSpecs;
final List<Interceptor> interceptors = new ArrayList<>(); // 拦截器
final List<Interceptor> networkInterceptors = new ArrayList<>(); // 网络拦截器
ProxySelector proxySelector;
CookieJar cookieJar;
Cache cache;    // 缓存
InternalCache internalCache;
SocketFactory socketFactory;
SSLSocketFactory sslSocketFactory;
HostnameVerifier hostnameVerifier;
CertificatePinner certificatePinner;
Authenticator proxyAuthenticator;   // 代理证书
Authenticator authenticator;        // 证书
ConnectionPool connectionPool;
Dns dns;        // DNS
boolean followSslRedirects;
boolean followRedirects;
boolean retryOnConnectionFailure;
int connectTimeout;  //连接超时时间
int readTimeout;     //读取超时时间
int writeTimeout;    //写入超时时间
```

### 2、创建Request请求(默认为GET请求)
```
//最简单的构造Request实例
Request request = new Request.Builder()
      .url(url)
      .build();
```
```
// 其他配置
url(String url);  //url地址
addHeader(String name, String value);  //添加请求头
removeHeader(String name) //移除某个请求头
headers(Headers headers)  //添加请求头,通过Headers来构造
post(RequestBody body)   //使用post来请求,通过RequestBody来构造入参
...
```
#### 创建RequestBody
```
//传递json
MediaType JSON =MediaType.parse("application/json;charset=utf-8");
RequestBody requestBody=RequestBody.create(JSON,jsonString);

```

### 3、发送请求
#### 3.1、添加请求
```
Call call=okHttpClient.newCall(request);
```
#### 3.2、获取结果
```java
1、异步(结果都在子线程种)
call.enqueue(new Callback() {
            @Override
            public void onFailure(Call call, IOException e) {

            }

            @Override
            public void onResponse(Call call, Response response) throws IOException {
                response.body().string();  //获取返回的结果
            }
        });
        
2、同步(运行在当前线程,需要开启子线程)
try {
            Response response = call.execute();
            String string = response.body().string();  //返回结果
        } catch (IOException e) {
            e.printStackTrace();
}
```

## WebSocket创建

```java
package com.shoukong.umpsky.manager.net.websocket;

import com.shoukong.umpsky.Constants;
import com.shoukong.umpsky.listener.WebSocketEventListener;
import com.shoukong.umpsky.utils.LogUtil;

import java.util.Objects;
import java.util.concurrent.TimeUnit;

import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;
import okhttp3.WebSocket;
import okhttp3.WebSocketListener;
import okhttp3.logging.HttpLoggingInterceptor;
import okio.ByteString;

//参考 https://github.com/fomin-zhu/websocket
public class WebSocketManager {

    private static final WebSocketManager webSocketManager = new WebSocketManager();

    private WebSocketManager() {

    }

    private HttpLoggingInterceptor loggingInterceptor = new HttpLoggingInterceptor(message -> LogUtil.e("WebSocket请求日志:" + message)).setLevel(HttpLoggingInterceptor.Level.BODY);

    public static WebSocketManager getInstance() {
        return webSocketManager;
    }

    private OkHttpClient client;
    private Request request;
    private WebSocketEventListener webSocketEventListener;
    private WebSocket mWebSocket;

    private boolean isConnect = false;

    public void init(WebSocketEventListener message) {
        loggingInterceptor.setLevel(HttpLoggingInterceptor.Level.BODY);
        client = Objects.requireNonNull(new OkHttpClient.Builder()
                .writeTimeout(30, TimeUnit.SECONDS))
                .readTimeout(30, TimeUnit.SECONDS)
                .connectTimeout(30, TimeUnit.SECONDS)
                .addInterceptor(loggingInterceptor)
                .build();
        request = new Request.Builder().url(Constants.WEBSOCKET_URL).build();
        webSocketEventListener = message;
        connect();
    }

    /**
     * 连接
     */
    public void connect() {
        if (isConnect()) {
            LogUtil.e("web socket connected");
            return;
        }
        client.newWebSocket(request, createListener());
    }

    /**
     * 是否连接
     */
    public boolean isConnect() {
        return mWebSocket != null && isConnect;
    }

    /**
     * 发送消息
     *
     * @param text 字符串
     * @return boolean
     */
    public boolean sendMessage(String text) {
        if (!isConnect()) return false;
        return mWebSocket.send(text);
    }

    /**
     * 发送消息
     *
     * @param byteString 字符集
     * @return boolean
     */
    public boolean sendMessage(ByteString byteString) {
        if (!isConnect()) return false;
        return mWebSocket.send(byteString);
    }

    /**
     * 关闭连接
     */
    public void close() {
        if (isConnect()) {
            mWebSocket.cancel();
            mWebSocket.close(1001, "客户端主动关闭连接");
        }
    }

    private WebSocketListener createListener() {
        return new WebSocketListener() {
            @Override
            public void onOpen(WebSocket webSocket, Response response) {
                super.onOpen(webSocket, response);
                LogUtil.e("open:" + response.toString());
                mWebSocket = webSocket;
                isConnect = response.code() == 101;
                if (!isConnect) {
                    //reconnect();
                } else {
                    LogUtil.e("connect success.");
                    if (webSocketEventListener != null) {
                        webSocketEventListener.onConnectSuccess();
                    }
                }
            }

            @Override
            public void onMessage(WebSocket webSocket, String text) {
                super.onMessage(webSocket, text);
                if (webSocketEventListener != null) {
                    webSocketEventListener.onMessage(text);
                }
            }

            @Override
            public void onMessage(WebSocket webSocket, ByteString bytes) {
                super.onMessage(webSocket, bytes);
                if (webSocketEventListener != null) {
                    webSocketEventListener.onMessage(bytes.base64());
                }
            }

            @Override
            public void onClosing(WebSocket webSocket, int code, String reason) {
                super.onClosing(webSocket, code, reason);
                mWebSocket = null;
                isConnect = false;
                if (webSocketEventListener != null) {
                    webSocketEventListener.onClose();
                }
            }

            @Override
            public void onClosed(WebSocket webSocket, int code, String reason) {
                super.onClosed(webSocket, code, reason);
                mWebSocket = null;
                isConnect = false;
                if (webSocketEventListener != null) {
                    webSocketEventListener.onClose();
                }
            }

            @Override
            public void onFailure(WebSocket webSocket, Throwable t, Response response) {
                super.onFailure(webSocket, t, response);
                if (response != null) {
                    LogUtil.e("connect failed：" + response.message());
                }
                LogUtil.e("connect failed throwable：" + t.getMessage());
                isConnect = false;
                if (webSocketEventListener != null) {
                    webSocketEventListener.onConnectFailed();
                }
            }
        };
    }
}

```

