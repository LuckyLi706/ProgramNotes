<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [其他工具类](#%E5%85%B6%E4%BB%96%E5%B7%A5%E5%85%B7%E7%B1%BB)
  - [App相关](#app%E7%9B%B8%E5%85%B3)
    - [安装App](#%E5%AE%89%E8%A3%85app)
    - [卸载App](#%E5%8D%B8%E8%BD%BDapp)
    - [启动App](#%E5%90%AF%E5%8A%A8app)
    - [获取App信息](#%E8%8E%B7%E5%8F%96app%E4%BF%A1%E6%81%AF)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# 其他工具类
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
