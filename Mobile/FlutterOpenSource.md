## 弹窗类

### file_picker 

文件或者文件夹选择弹窗（支持全平台）

+ [地址](https://pub.dev/packages/file_picker)

+ 使用

  ```dart
  //弹窗选择单个文件
  FilePickerResult? result = await FilePicker.platform.pickFiles();
  if (result != null) {
    final fileBytes = result.files.first.bytes;  //获取文件字节流
    final fileName = result.files.first.name;   //获取文件名
    if (kIsWeb) {    //web端获取不到文件路径
       print(fileName);
       return;
    }
    PlatformFile file = result.files.first;
    //获取文件信息
    print(file.name);
    print(file.bytes);
    print(file.size);
    print(file.extension);
    print(file.path);
    print(result.files.single.path);  // 获取文件路径
  } else {
    // User canceled the picker
  }
  
  //弹窗可以选择多个文件
  FilePickerResult? result = await FilePicker.platform.pickFiles(allowMultiple: true);
  if (result != null) {
    List<File> files = result.paths.map((path) => File(path)).toList();
  } else {
    // User canceled the picker
  }
  
  //弹窗可以选择多个文件（定义文件类型）
  FilePickerResult? result = await FilePicker.platform.pickFiles(
    type: FileType.custom,
    allowedExtensions: ['jpg', 'pdf', 'doc'],
  );
  
  //弹窗选择文件夹
  String? selectedDirectory = await FilePicker.platform.getDirectoryPath();
  if (selectedDirectory == null) {
    // User canceled the picker
  }
  
  //弹窗保存文件
  String? outputFile = await FilePicker.platform.saveFile(
    dialogTitle: 'Please select an output file:',
    fileName: 'output-file.pdf',
  );
  if (outputFile == null) {
    // User canceled the picker
  }
  
  
  ```


## 存储类

### shared_preferences

如果要存储一些简单的数据，使用shared_preferences插件会比较简单（支持全平台）

+ [地址](https://pub.dev/packages/shared_preferences)

+ 使用

  ```dart
  /**
  各平台存储位置
  Android	   SharedPreferences
  iOS	      NSUserDefaults
  Linux	In the XDG_DATA_HOME directory
  macOS	NSUserDefaults
  Web	LocalStorage
  Windows	In the roaming AppData directory
  **/
  
  //1.写数据
  // Obtain shared preferences.
  final prefs = await SharedPreferences.getInstance();
  // Save an integer value to 'counter' key.
  await prefs.setInt('counter', 10);
  // Save an boolean value to 'repeat' key.
  await prefs.setBool('repeat', true);
  // Save an double value to 'decimal' key.
  await prefs.setDouble('decimal', 1.5);
  // Save an String value to 'action' key.
  await prefs.setString('action', 'Start');
  // Save an list of strings to 'items' key.
  await prefs.setStringList('items', <String>['Earth', 'Moon', 'Sun']);
  
  //2.读数据
  // Try reading data from the 'counter' key. If it doesn't exist, returns null.
  final int? counter = prefs.getInt('counter');
  // Try reading data from the 'repeat' key. If it doesn't exist, returns null.
  final bool? repeat = prefs.getBool('repeat');
  // Try reading data from the 'decimal' key. If it doesn't exist, returns null.
  final double? decimal = prefs.getDouble('decimal');
  // Try reading data from the 'action' key. If it doesn't exist, returns null.
  final String? action = prefs.getString('action');
  // Try reading data from the 'items' key. If it doesn't exist, returns null.
  final List<String>? items = prefs.getStringList('items');
  
  //3.删数据
  // Remove data for the 'counter' key.
  final success = await prefs.remove('counter');
  ```

## 网络相关

### dio

一个强大的Dart Http请求库，支持Restful API、FormData、拦截器、请求取消、Cookie管理、文件上传/下载、超时等

+ [地址](https://pub.dev/packages/dio)

+ 使用

  ```dart
  //实例化
  import 'package:dio/dio.dart';
  Dio dio =  Dio();
  
  //通过dio发起请求
  
  //发起GET请求
  Response response;
  response=await dio.get("/test?id=12&name=wendu")
  print(response.data.toString());
  //对于GET请求我们可以将query参数通过对象来传递，上面的代码等同于：
  response=await dio.get("/test",queryParameters:{"id":12,"name":"wendu"})
  print(response);
  
  //发起一个POST请求
  response=await dio.post("/test",data:{"id":12,"name":"wendu"})
  
  //发起多个并发请求
  response= await Future.wait([dio.post("/info"),dio.get("/token")]);
  
  //下载文件
  response=await dio.download("https://www.google.com/",_savePath);
  
  //发送 FormData,如果发送的数据是FormData，则dio会将请求header的contentType设为“multipart/form-data”
  FormData formData = FormData.from({
     "name": "wendux",
     "age": 25,
  });
  response = await dio.post("/info", data: formData)
      
  //通过FormData上传多个文件:
  FormData formData = FormData.from({
     "name": "wendux",
     "age": 25,
     "file1": UploadFileInfo(File("./upload.txt"), "upload1.txt"),
     "file2": UploadFileInfo(File("./upload.txt"), "upload2.txt"),
       // 支持文件数组上传
     "files": [
        UploadFileInfo(File("./example/upload.txt"), "upload.txt"),
        UploadFileInfo(File("./example/upload.txt"), "upload.txt")
      ]
  });
  response = await dio.post("/info", data: formData)
      
  //值得一提的是，dio内部仍然使用HttpClient发起的请求，所以代理、请求认证、证书校验等和HttpClient是相同的，我们可以在onHttpClientCreate回调中设置，例如:
  (dio.httpClientAdapter as DefaultHttpClientAdapter).onHttpClientCreate = (client) {
      //设置代理 
      client.findProxy = (uri) {
        return "PROXY 192.168.1.2:8888";
      };
      //校验证书
      httpClient.badCertificateCallback=(X509Certificate cert, String host, int port){
        if(cert.pem==PEM){
        return true; //证书一致，则允许发送数据
       }
       return false;
      };   
    };
  ```

  

