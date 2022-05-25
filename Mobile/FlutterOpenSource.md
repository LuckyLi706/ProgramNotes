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

  