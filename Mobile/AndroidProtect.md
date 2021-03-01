# 防

## JNI保护

### 动态实现替换函数名

```java
//重写映射的方法（返回值和入参需要和被映射的函数一样）
jstring lijie(JNIEnv *env, jobject obj) {
       //具体实现
    return env->NewStringUTF("Hello,World");
}

//原函数和被映射函数一一对应
static JNINativeMethod methods[]{
        {"stringFromJNI",
                "()Ljava/lang/String;",
                (void *) lijie
        },
        {
                //原函数名,函数的签名(入参和返回值),映射的方法名
        }};

//加载so是,最开始执行的函数,使用该函数进行动态注册以及替换函数名
JNIEXPORT jint JNICALL
JNI_OnLoad(JavaVM *vm, void *reserved) {
    JNIEnv *pEnv = NULL;
    if (vm->GetEnv((void **) &pEnv, JNI_VERSION_1_6) != JNI_OK) {
        return JNI_ERR;
    }
    //获取native函数所在的Class对象
    jclass cls = pEnv->FindClass("com/lucky/jniexercise/MainActivity");
    if (cls == NULL) {
        //__android_log_print(ANDROID_LOG_DEBUG, "__BING__", "jni_replace:FindClass Error");
        return -1;
        //进行函数注册
    } else if (pEnv->RegisterNatives(cls, methods, sizeof(methods) / sizeof(methods[0]))) {
        return JNI_ERR;
    }
    return JNI_VERSION_1_6;
}
```

## 检测TracePid

 IDA进行so动态调试是基于进程的注入技术，然后使用Linux中的ptrace机制，进行调试目标进程的附加操作。

 ptrace机制有个特点，如果一个进程被调试了，在他进程的status文件中有个TracePid会记录调试者的进程id值

```java
#include <jni.h>
#include <string>
#include <pthread.h>   //pthread_create创建线程的头文件
#include <unistd.h>    //getpid 获取进程号以及sleep 休眠的头文件
#include <stdio.h>     //fclose 关闭流头文件
#include <stdlib.h>    //exit  退出程序头文件
#include <android/log.h>

#define LOGD(...) __android_log_print(ANDROID_LOG_DEBUG, "ceshi", __VA_ARGS__)
//获取TracePid
int get_number_for_str(char *str) {
    if (str == NULL) {
        return -1;
    }
    char result[20];
    int count = 0;
    while (*str != '\0') {
        if (*str >= 48 && *str <= 57) {
            result[count] = *str;
            count++;
        }
        str++;
    }
    int val = atoi(result);
    return val;
}

//使用死循环检测TraceId
void *thread_function(void *argv) {
    int pid = getpid();
    char file_name[20] = {'\0'};
    //读取status文件
    sprintf(file_name, "/proc/%d/status", pid);
    char linestr[256];
    int i = 0, traceid;
    FILE *fp;
    while (1) {
        i = 0;
        fp = fopen(file_name, "r");
        if (fp == NULL) {
            break;
        }
        while (!feof(fp)) {
            fgets(linestr, 256, fp);
            //TraceId是在第六行
            if (i == 5) {
                traceid = get_number_for_str(linestr);
                LOGD("traceId:%d", traceid);
                if (traceid > 0) {
                    LOGD("I was be traced...trace pid:%d", traceid);
                    exit(0);
                }
                break;
            }
            i++;
        }
        fclose(fp);
        sleep(5);
    }
    return ((void *) 0);
}

void create_thread_check_traceid() {
    pthread_t t_id;
    //启动线程来进行轮番检测 &t_id线程id
    int err = pthread_create(&t_id, NULL, thread_function, NULL);
    if (err != 0) {
        LOGD("create thread fail: %s\n", strerror(err));
    }
}

JNIEXPORT  jint  JNICALL
JNI_OnLoad(JavaVM *vm, void *reserved) {
    create_thread_check_traceid();
}
```

## 多开检测

+ [检测1](https://github.com/ysrc/AntiVirtualApp)
+ [检测2](https://link.jianshu.com/?t=https://github.com/ZaratustraN/Check_VirtualAPK)
+ [检测3](https://www.zhihu.com/question/42998620)


## 混淆篇

### 代码混淆

+ [第三方库混淆](https://github.com/msdx/android-proguard-cn)
+ [变态字典混淆](https://github.com/ysrc/AndroidObfuseDictionary)
+ [基本的代码混淆](https://github.com/HurTeng/AndroidProguard)

### 资源混淆

+ [微信推出的资源混淆工具](https://github.com/shwenzhang/AndResGuard)

## 在线加固

+ [梆梆加固](https://dev.bangcle.com/)
+ [五大移动应用加固平台评测](https://zhuanlan.zhihu.com/p/21482658)