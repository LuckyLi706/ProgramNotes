<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [App相关](#app%E7%9B%B8%E5%85%B3)
  - [安装App](#%E5%AE%89%E8%A3%85app)
  - [卸载App](#%E5%8D%B8%E8%BD%BDapp)
  - [启动App](#%E5%90%AF%E5%8A%A8app)
  - [获取App信息](#%E8%8E%B7%E5%8F%96app%E4%BF%A1%E6%81%AF)
- [网络相关](#%E7%BD%91%E7%BB%9C%E7%9B%B8%E5%85%B3)
    - [是否有网](#%E6%98%AF%E5%90%A6%E6%9C%89%E7%BD%91)
    - [网络类型](#%E7%BD%91%E7%BB%9C%E7%B1%BB%E5%9E%8B)
    - [无线网的ip](#%E6%97%A0%E7%BA%BF%E7%BD%91%E7%9A%84ip)
    - [移动网和有线网的ip](#%E7%A7%BB%E5%8A%A8%E7%BD%91%E5%92%8C%E6%9C%89%E7%BA%BF%E7%BD%91%E7%9A%84ip)
    - [获取周边无线网信息](#%E8%8E%B7%E5%8F%96%E5%91%A8%E8%BE%B9%E6%97%A0%E7%BA%BF%E7%BD%91%E4%BF%A1%E6%81%AF)
- [存储](#%E5%AD%98%E5%82%A8)
  - [存储路径](#%E5%AD%98%E5%82%A8%E8%B7%AF%E5%BE%84)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## App相关
### 安装App
```kotlin
//部分机型需要apk以及它的文件夹有777权限
fun installApk(context: Context, fileName: String) {
            val apkFile = File(fileName)
            if (!apkFile.exists()) {
                return
            }
            val intent = Intent(Intent.ACTION_VIEW)
            if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N) {
                intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
                val contentUri = FileProvider.getUriForFile(
                    context,
                    BuildConfig.APPLICATION_ID + ".FileProvider",
                    apkFile
                )
                intent.setDataAndType(contentUri, "application/vnd.android.package-archive")
                intent.addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION)
                intent.addFlags(Intent.FLAG_GRANT_WRITE_URI_PERMISSION)
            } else {
                // FIXME: 2018/8/2 Android 4.4 API 19 startActivityForResult 直接调用 onActivityResult
                intent.setDataAndType(
                    Uri.fromFile(apkFile),
                    "application/vnd.android.package-archive"
                );
                // intent.flags = Intent.FLAG_ACTIVITY_NEW_TASK;
                intent.flags = Intent.FLAG_ACTIVITY_NEW_TASK
            }
            context.startActivity(intent)
        }

//授予权限
class ShellUtil {
    companion object {
        const val PERM_FILE_COMMAND = "chmod 777 "    //给下载的apk以及apk路径授予权限，不然有的可能安装不了
        fun runCommand(command: String) {
            try {
                Runtime.getRuntime().exec(command)
            } catch (e: Exception) {
                LogUtil.d("runCommand:" + e.message)
            }
        }
    }
}        

/**
高版本需要授予其文件夹权限rc_file_path.xml

<?xml version="1.0" encoding="utf-8"?>
<paths>
    <files-path       //相当于/data/data/package/files
        name="files_path"     
        path="apk" />   //相当于/data/data/package/files/apk

    <external-files-path   //相当于/sdcard/Android/package/files
        name="external_files_path"
        path="apk" />    //这是文件夹名
</paths>
**/


/**
manifest的配置

<provider
            android:name="androidx.core.content.FileProvider"
            android:authorities="com.imi.gamestore.FileProvider"
            android:exported="false"
            android:grantUriPermissions="true">
            <meta-data
                android:name="android.support.FILE_PROVIDER_PATHS"
                android:resource="@xml/rc_file_path" />
        </provider>
**/
```
### 卸载App
```kotlin
fun uninstallApk(appPackageName: String)
            val packageURI = Uri.parse("package:$appPackageName")
            val uninstallIntent = Intent(Intent.ACTION_DELETE, packageURI)
            uninstallIntent.flags = Intent.FLAG_ACTIVITY_NEW_TASK
            context.startActivity(uninstallIntent)
```
### 启动App
```kotlin
//启动app(app包名和启动类的全称)
        fun startApp(appPackageName: String, startAppName: String): Boolean {
            val intent = Intent()
            intent.component = ComponentName(appPackageName, startAppName)
            intent.addFlags(Intent.FLAG_ACTIVITY_NEW_TASK)
            //intent.setData(Uri.parse("com.lucky.gamestoretest://main"))
            if (context.packageManager.resolveActivity(
                    intent,
                    PackageManager.MATCH_DEFAULT_ONLY
                ) != null     //判断是否存在这个App
            ) {
                context.startActivity(intent)
                return true
            } else {
                return false
            }
        }
```
### 获取App信息
```kotlin
///获取所有安装的app信息
        fun getInstallApps(): List<AppInfo> {
            val pm = context.packageManager
            val installedPackages = pm.getInstalledPackages(0) //获取所以已安装的包
            val list: ArrayList<AppInfo> = ArrayList<AppInfo>()
            for (packageInfo in installedPackages) {
//                pm.getLaunchIntentForPackage(packageInfo.packageName) ?: continue
                val info = AppInfo(packageInfo.packageName, packageInfo.versionName)
//                val applicationInfo = packageInfo.applicationInfo //应用信息
//                info.name = applicationInfo.loadLabel(pm).toString()
//                info.icon = applicationInfo.loadIcon(pm) //状态机,通过01状态来表示是否具备某些属性和功能
//                val packageName = packageInfo.packageName
//                info.versionName = packageInfo.versionName
//                info.versionCode = packageInfo.versionCode
//                val flags = applicationInfo.flags //获取应用标记
//                info.isRom =
//                    flags and ApplicationInfo.FLAG_EXTERNAL_STORAGE != ApplicationInfo.FLAG_EXTERNAL_STORAGE
//                info.isUser = flags and ApplicationInfo.FLAG_SYSTEM != ApplicationInfo.FLAG_SYSTEM
//                //            Log.e(TAG, "getInstallApps: " + info.toString());
                if ((packageInfo.applicationInfo.flags and FLAG_SYSTEM) <= 0) {   //非系统App
                    // customs applications
                    list.add(info)
                }
            }
            return list
        }
```

## 网络相关

#### 是否有网

```java
//需要权限     <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
private boolean isNetworkAvailable() {
        ConnectivityManager connManager = (ConnectivityManager) getSystemService(Context.CONNECTIVITY_SERVICE); // 获取网络服务
        if (connManager == null) {
            return false;
        }
        NetworkInfo activeNetworkInfo = connManager.getActiveNetworkInfo();
        return activeNetworkInfo != null && activeNetworkInfo.isConnected();
    }
```

#### 网络类型

```java
//需要权限     <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
private String getNetworkType() {
        ConnectivityManager connManager = (ConnectivityManager) getSystemService(Context.CONNECTIVITY_SERVICE); // 获取网络服务
        if (connManager == null) {
            return "NO_NETWORK";
        }
        if (Build.VERSION.SDK_INT < 23) {   //下面的方式已经过时
            NetworkInfo networkInfo = connManager.getActiveNetworkInfo();
            if (networkInfo != null && networkInfo.isConnected()) {
                if (networkInfo.getType() == ConnectivityManager.TYPE_WIFI) {//WIFI
                } else if (networkInfo.getType() == ConnectivityManager.TYPE_MOBILE) {//移动数据
                } else if (networkInfo.getType() == ConnectivityManager.TYPE_ETHERNET) {//有线网
                }
            }
        } else {
            //高版网络状态
            Network network = connManager.getActiveNetwork();
            if (network != null) {
                NetworkCapabilities networkCapabilities = connManager.getNetworkCapabilities(network);
                if (networkCapabilities != null) {
                    if (networkCapabilities.hasTransport(NetworkCapabilities.TRANSPORT_WIFI)) {//WIFI
                    } else if (networkCapabilities.hasTransport(NetworkCapabilities.TRANSPORT_CELLULAR)) {//移动数据
                    } else if (networkCapabilities.hasTransport(NetworkCapabilities.TRANSPORT_ETHERNET)) { //有线网
                    }
                }
            }
        }
        return "NO_NETWORK";
    }
```

#### 无线网的ip

```java
//需要权限         <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
public String getWifiIp() {
        try {
            //获取wifi服务
            WifiManager wifiManager = (WifiManager) getApplicationContext().getSystemService(Context.WIFI_SERVICE);
            //判断wifi是否开启
            assert wifiManager != null;
            if (!wifiManager.isWifiEnabled()) {
                return "";
            }
            WifiInfo wifiInfo = wifiManager.getConnectionInfo();
            int ipAddress = wifiInfo.getIpAddress();
            String ip = intToIp(ipAddress);
            return ip;
        } catch (Throwable ex) {
            ex.printStackTrace();
        }
        return "";
    }

private String intToIp(int i) {
        return (i & 0xFF) + "." + ((i >> 8) & 0xFF) + "." + ((i >> 16) & 0xFF) + "." + (i >> 24 & 0xFF);
    }
```

#### 移动网和有线网的ip

```java
//需要权限          <uses-permission android:name="android.permission.INTERNET"/>
public String getCellarIp() {
        try {
            String ipv4;
            ArrayList<NetworkInterface> nilist =
                    Collections.list(NetworkInterface.getNetworkInterfaces());
            for (NetworkInterface ni : nilist) {
                ArrayList<InetAddress> ialist = Collections.list(ni.getInetAddresses());
                for (InetAddress address : ialist) {
                    if (!address.isLoopbackAddress() && !address.isLinkLocalAddress()) {
                        ipv4 = address.getHostAddress();
                        return ipv4;
                    }
                }
            }
        } catch (SocketException ex) {
            LogUtil.w("getLocalIpV4Address", ex.getMessage());
        }
        return "";
    }
```

#### 获取周边无线网信息

```java
/**
需要权限：
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE"/>
**/
public String wifiList() {
        try {
            WifiManager manager =
                    (WifiManager)getApplicationContext().getSystemService(Context.WIFI_SERVICE);
            assert manager != null;
            manager.startScan();
            StringBuffer str = new StringBuffer("");
            List<ScanResult> result = manager.getScanResults();
            if (result != null && result.size() > 0) {
                for (ScanResult scanResult : result) {
                    str.append(scanResult.SSID);
                    str.append(",");
                    str.append(scanResult.BSSID);
                    str.append(",");
                    str.append(scanResult.capabilities.replace("[", "").replace("]", ""));
                    str.append(",");
                }
                return (str.substring(0, str.length() - 1) + "]").replace("=", "").replace(
                        "&", "");
            }
        } catch (Throwable e) {
            e.printStackTrace();
        }
        return "";
    }
```

## 存储

### 存储路径

```java
public class PathUtil {

    public static String DIRECTORY_ALARMS = "Alarms";
    public static String DIRECTORY_AUDIOBOOKS = "Audiobooks";
    public static String DIRECTORY_DCIM = "DCIM";
    public static String DIRECTORY_DOCUMENTS = "Documents";
    public static String DIRECTORY_DOWNLOADS = "Download";
    public static String DIRECTORY_MOVIES = "Movies";
    public static String DIRECTORY_MUSIC = "Music";
    public static String DIRECTORY_NOTIFICATIONS = "Notifications";
    public static String DIRECTORY_PICTURES = "Pictures";
    public static String DIRECTORY_PODCASTS = "Podcasts";
    public static String DIRECTORY_RINGTONES = "Ringtones";
    public static String DIRECTORY_SCREENSHOTS = "Screenshots";

    //  /data目录
    public static String getDataDir() {
        return Environment.getDataDirectory().getAbsolutePath();
    }

    //  /system目录
    public static String getSystemDir() {
        return Environment.getRootDirectory().getAbsolutePath();
    }

    //  /cache目录
    public static String getCacheDir() {
        return Environment.getDownloadCacheDirectory().getAbsolutePath();
    }

    /**
     * @param name 都存储在SD卡公共目录下（也可以自己写自定义的文件夹名字,表示创建文件夹）
     *             DIRECTORY_DCIM  存储在/storage/emulated/0/DCIM
     *             DIRECTORY_ALARMS 存储在/storage/emulated/0/ALARMS
     * @return
     */
    public static String getPublicDir(String name) {
        //该方法9.0上已经过时,暂时还没有解决方案
        return Environment.getExternalStoragePublicDirectory(name).getAbsolutePath();
    }

    public static String getExternalStorageDir() {
        return Environment.getExternalStorageDirectory().getAbsolutePath();
    }

    public static String getExternalFilesDir(Context context) {
        return getExternalFilesDir(context, null);
    }

    /**
     * 4.4以下不存在该方法
     * 4.4位置在/storage/sdcard/Android/data/包名/files，
     * 5.0以上位置在/storage/emulated/0/Android/data/包名/files
     * 表示app外部私有目录，不需要任何权限
     *
     * @param context 上下文对象
     * @param name    为null获取上面的路径。不为null表示在该目录下创建该路径
     * @return
     */
    public static String getExternalFilesDir(Context context, String name) {
        File file = context.getExternalFilesDir(name);
        if (file != null) {
            return file.getAbsolutePath();
        }
        return null;
    }

    /**
     * 4.4以下不存在该方法
     * 4.4位置在/storage/sdcard/Android/data/包名/cache，
     * 5.0以上位置在/storage/emulated/0/Android/data/包名/cache
     * 表示app外部私有目录，不需要任何权限
     *
     * @param context 上下文对象
     * @return
     */
    public static String getExternalCacheDir(Context context) {
        File file = context.getExternalCacheDir();
        if (file != null) {
            return file.getAbsolutePath();
        }
        return null;
    }

    /**
     * 存储位置在/data/data
     *
     * @param context
     * @return
     */
    public static String getAppDir(Context context) {
        String path = "";
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.N) {
            path = context.getDataDir().getAbsolutePath();
        } else {
            path = context.getDir("name", Context.MODE_PRIVATE).getParent();
        }
        return path;
    }

    /**
     * 存储位置在/data/data/包名/files
     * 单用户模式（/data/user/0/包名/files）软链接到/data/data/包名/files
     * 多用户（第二个用户 /data/user/10/包名/files）
     *
     * @param context
     * @return
     */
    public static String getInternalFileDir(Context context) {
        return context.getFilesDir().getAbsolutePath();
    }

    /**
     * 存储位置在/data/data/包名/app_文件夹
     * 多用户同上
     *
     * @param context 上下文对象
     * @param name    文件夹名字,有一个前缀app_
     * @return
     */
    public static String getInternalDir(Context context, String name) {
        return context.getDir(name, Context.MODE_PRIVATE).getAbsolutePath();
    }

    /**
     * 存储位置在data/data/包名/cache
     * 多用户同上
     *
     * @param context
     * @return
     */
    public static String getInternalCacheDir(Context context) {
        return context.getCacheDir().getAbsolutePath();
    }

    /**
     * 存储位置在data/data/包名/databases
     * 中间的字符串不能写null和空，表示建立的文件夹）多用户同上
     *
     * @param context
     * @return
     */
    public static String getInternalDatabaseDir(Context context) {
        return context.getDatabasePath("12").getParent();
    }

    /**
     * 版本大于等于5.0
     * 存储位置在/data/data/包名/code_cache
     *
     * @param context
     * @return
     */
    @TargetApi(Build.VERSION_CODES.LOLLIPOP)
    public static String getInternalCodeCacheDir(Context context) {
        return context.getCodeCacheDir().getAbsolutePath();
    }

    public static String getInternalSharePreDir(Context context) {
        return getAppDir(context) + File.separator + "/shared_prefs";
    }
}
```

