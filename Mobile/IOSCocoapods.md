# Cocoapods

## 介绍

```undefined
CocoaPods是IOS项目上负责管理依赖的工具，即对第三方库的依赖。开发iOS项目不可避免地要使用第三方开源库，CocoaPods的出现使得我们可以节省设置和更新第三方开源库的时间。
```

## 安装Ruby + CocoaPods

```shell
安装ruby（使用Homeview去）
1.brew install ruby（安装最新版的ruby）
2.ruby --version（ruby版本）
3.curl -sSL https://get.rvm.io | bash -s stable（RVM 是一个便捷的多版本 Ruby 环境的管理和切换工具.安装它，官网：https://rvm.io/）
4.rvm get stable（rvm更新）
5.rvm --version（rvm版本）
6.sudo gem update --system（gem更新）
7.gem sources --remove https://rubygems.org/（移除之前的源）
8.gem sources --add https://gems.ruby-china.com/（设置新的源）
9.gem sources -l（查看当前源）
10.gem --version（gem版本）
注意：如果你第一次安装ruby你可以忽略345的命令，还有就是遇到You can try adding it manually in `/Users/XXX/.cocoapods/repos` 这种问题直接去github下载然后放到路径下就好了，是因为文件太大网不好。

安装cocoapods
1.sudo gem install -n /usr/local/bin cocoapods（安装cocoapods）
2.pod setup（安装本地库）
3.pod repo update（更新本地库）
4.pod --version（pod版本）

卸载cocoapods
1.sudo gem uninstall -n /user/local/bin cocoapods
```

## 终端命令安装Cocoapods

```shell
安装ruby
1.ruby -v（查看当前ruby版本）
2.gem sources -l（查看当前镜像地址）
3.gem sources --remove https://rubygems.org/（移除原本镜像地址）
4.gem sources -a https://gems.ruby-china.com（替换镜像，防止被翻）
5.gem sources -l（检查替换镜像是否成功）

安装Cocoapods
1.sudo gem install cocoapods（安装cocoapods）
```

## 首次安装Cocoapods的使用

```bash
1.新建一个项目，假设项目名称为HelloWord
2.终端输入：cd HelloWord文件路径
3.创建Podfile配置文件，终端输入：vim Podfile
4.接着键盘输入i进入编辑模式，继续输入以下内容：
        platform:ios, '8.0'
        target 'HelloWord'
        pod 'Masonry', '~> 1.1.0'
5.键盘按下ESC键，然后输入“:wq”进入vim命令模式，回车
6.终端继续输入pod install，到此恭喜你，你安装好了CocoaPods，并且导入了一个第三方库Masonry，以后打开该项目只需找到HelloWord文件夹下后缀名为.xcworkspace打开即可。
```

## CocoaPods命令

```
1.pod init                       ：初始化
2.pod install                    ：安装库
3.pod update                     ：更新库
4.pod search XXX                 ：查找所需三方库
5.gem install cocoapods --pre    ：更新Cocoapods
6.pod env                        ：查看已经安装的cocoapods版本
7.pod outdated                   ：查看Podfile文件中的依赖库的最新版本
```

## 问题点（持续更新）

```jsx
1.[!] Invalid `Podfile` file: syntax error, unexpected end, expecting end-of-input
  解决方案：这是因为你Podfile文件内容输入错误，好好检查一下吧～
2.Specs satisfying the `Kingfisher (~> 5.13.3)` dependency were found, but they required a higher minimum deployment target.
  解决方案：原因是因为三方库本身支持最低版本是10.0，而我设置了8.0因此报错
3.[!] Unable to find a specification for `XXX`You have either: * out-of-date source repos which you can update with `pod repo update` or with `pod install --repo-update`.* mistyped the name or version.* not added the source repo that hosts the Podspec to your Podfile.
  解决方案：由于本地repo中没有该库或者该版本导致的，执行pod repo update即可，你会发现pod repo update真的很慢，加快速的就是更新某个库pod repo update后拼接库的路径即可XXX.podspec.json(例如：repo update ~/.cocoapods/repos//master/Specs)
```

## Cocoapods相关知识点（持续更新）

```php
1.pod install 和 pod update的区别以及使用场景
    pod install：会去检查podfile.lock是否已经包含该库，如果包含则继续判断是否指定版本，如果指定版本就去检查podfile.lock中保存的版本是否与新指定的相同，相同则跳过，不相同则更新，如果没有指定版本则不检查更新直接跳过，如果不包含该库则去下载该库并将版本保存在podfile.lock文件中。每次当pod install 命令运行，并下载安装新的pods的时候，他会在Podfile.lock中为每个pod写入它安装的版本。此文件跟踪每一个已安装的版本，并且锁定这些版本。当运行pod install 的时候它仅仅解析那些Podfile.lock中位列出的依赖关系。对于Podfile.lock中列出的pods，它仅仅会下载指明的版本，不会去检查是否有新版本可用。对于Podfile.lock中未列出的pods，他会搜索与Podfile中内容相匹配的版本 (例如 pod 'MyPod', '~>1.2')。
    pod update：这个命令会忽略Podfile.lock中的记录，直接去找符合Podfile文件中的该依赖库的约束版本（无约束的话就是最新版本）。一般在你想要更新pods到一个新的版本的时候使用。当运行pod update PODNAME时，CocoaPods将尝试查找PODNAME的更新版本，而不考虑Podfile.lock中列出的版本。 它会将pod更新为可能的最新版本（只要它与Podfile中的版本限制相匹配）。如果运行pod更新没有pod名称，CocoaPods将更新您Podfile中列出的每个pod到最新的版本。
    pod install使用场景：
          a.新创建工程，第一次引入pod库时
          b.修改了Podfile文件，添加或删除了所依赖的pod库时。
          c.团队中新人拉取工程后获取pod库时。
          d.团队中，不同开发者要同步对pod库的依赖时(有人改变了依赖关系，删除或增加pod时。还有就是有人执行了pod update,此时他的Podfile.lock文件中的跟踪版本就已经变更，此时，其他人只要pod install就能更新为和Podfile.lock文件中的版本。还有就是如果Podfile和Podfile.lock的记录相冲突，Podfile文件中指定了低于Podfile.lock中记录的版本。会以Podfile文件为准，并在获取成功后更新Podfile.lock文件。)
    pod update使用场景：一般在你想要更新pods到一个新的版本的时候使用。
2.podfile指定版本号时的逻辑运算符
    Besides no version, or a specific one, it is also possible touse logical operators:
    '> 0.1'    Any version higher than 0.1         0.1以上
    '>= 0.1'   Version 0.1 and any higher version  0.1以上，包括0.1
    '< 0.1'    Any version lower than 0.1          0.1以下
    '<= 0.1'   Version 0.1 and any lower version   0.1以下，包括0.1
    In addition to the logic operators CocoaPods has an optimisicoperator ~>:
    '~> 0.1.2' Version 0.1.2 and the versions up to 0.2, not including 0.2 and higher  0.2以下(不含0.2)，0.1.2以上（含0.1.2）
    '~> 0.1' Version 0.1 and the versions up to 1.0, not including 1.0 and higher      1.0以下(不含1.0)，0.1以上（含0.1）
    '~> 0' Version 0 and higher, this is basically the same as not having it.          0和以上，等于没有此约束
3.Podfile.lock
    a.Podfile.lock这个文件是我们新建Podfile文件后会自动生成的一个文件，里面存储了我们已经安装的依赖库的版本。
    b.当我们第一次运行Podfile时，如果对依赖库不指定版本的话，cocoapods会安装最新的版本，同时将pods的版本记录在Podfile.lock文件中。这个文件会保持对每个pod已安装版本的跟踪，并且锁定这些版本。再执行pod install的话，只会处理没有记录在Podfile.lock中的依赖库，会查找匹配Podfile中描述的版本。对于已经记录在Podfile.lock的依赖库，会下载Podfile.lock文件中记录的版本，而不会检查是否有更新。当然，如果你约束了pods的版本的话，会按照你指定的版本进行安装，同时也会更新Podfile.lock记录的信息。
    c.Podfile.lock内部
          PODS:
            - Masonry (1.1.0)
          DEPENDENCIES:
            - Masonry (~> 1.1.0)
          SPEC REPOS:
            trunk:
              - Masonry
          SPEC CHECKSUMS:
            Masonry: 678fab65091a9290e40e2832a55e7ab731aad201
          PODFILE CHECKSUM: 7a5a6c829f4d2252e3e3d116ab9757a3b270ed8a
          COCOAPODS: 1.9.3
4.Cocoapods原理
    是将所有的依赖库都放到另一个名为Pods的项目中, 然而让主项目依赖Pods项目,这样,源码管理工作任务从主项目移到了Pods项目中.
    a.Pods项目最终会编译成一个名为libPods.a的文件, 主项目只要依赖这个.a文件即可.
    b.对于资源文件, CocoaPods提供了一个名为Pods-resources.sh的bash脚步, 该脚本在每次项目, 编译的时候都会执行,将第三方库的各种资源文件复制到目标目录中.
    c.CocoaPods通过一个名为Pods.xcconfig的文件在编译设置所有的依赖和参数
5.Cocoapods下载原理
    s.source = { :git => '[git@gitlab.xxx.net](https://links.jianshu.com/go?to=mailto%3Agit%40gitlab.xxx.net):ios-thirdpartservice/xxxreact.git', :tag => '1.0.0' }
当使用Cocoapods导入私有库时，Cocoapods先是根据:git => ‘[git@gitlab.xxx.net](https://links.jianshu.com/go?to=mailto%3Agit%40gitlab.xxx.net):ios-thirdpartservice/xxxreact.git’找到对应的git仓库，然后根据:tag => ‘1.0.0’定位到对应tag的提交（如果没有注明Pod依赖库版本则定位到最后一次的提交），然后在这次提交中检索后缀为.podspec的文件（文件可以随便命名）。找到podspec文件后先要验证[s.name](https://links.jianshu.com/go?to=http%3A%2F%2Fs.name)是否与Podfile中的一致，如果不一致则install时会报错：[!]Unable to find a specification for ‘React’.验证成功后，就会根据Podspec中的s.source_files找到需要导入的代码文件，并通过其他的的数据找到对应的配置文件或资源文件等。最后，将其下载到本地项目中。如果是共有库，这些原理也相同。只是共有库要将podspec文件上传到cocoapods。在导入的时候通过名字React去cocoapods匹配对应的podspec，然后根据s.source去找到对应的仓库和对应的版本，然后会再去匹配新的podspec，后边的步骤就完全相同了。
6.Cocoapods集成原理
    当所有的依赖库都下载完后，Cocoapods会将所有的依赖库都放到另一个名为Pods的项目中，然后让主项目依赖Pods项目。这样，源码管理工作都从主目录移到了Pods项目中。Pods项目最终会编译成为一个名为libPods.a的文件，主项目只要依赖这个.a文件即可。对于资源文件，Cocoapods提供了一个名为Pods-resource.sh的bash脚本，该脚本在每次项目编译的时候都会执行，将Pods依赖库的各种资源文件复制到目标目录中。Cocoapods还通过一个名为Pods.xcconfig的文件来在编译时设置所有的依赖和参数。
7.Cocoapods版本控制原理
    当执行完pod install之后，cocoapods会生成一个podfile.lock的文件。podfile.lock文件最大的用处在于多人开发。如果你没有在podfile中指定pods版本pod ‘React’，那么默认为获取当前React依赖库的最新版本。当团队中的某个人执行完pod install命令后，生产的podfile.lock文件就记录下了当时最新pods依赖库的版本，这时团队中的其他人check下来这份包含podfile.lock文件的工程以后，再去执行pod install命令时，获取下来的pods依赖库的版本和最开始用户获取到的版本一致。如果没有podfile.lock文件，后续所有用户执行pod install命令都会获取最新版本的React,这就可能造成一个团队使用的依赖库版本不一致，这对团队协作来说绝对是个灾难。在这种情况下，如果团队想使用当前最新版本的React依赖库，有两种方案：1、更改podfile，使其指向最新版本的React依赖库 2、执行pod update命令；鉴于podfile.lock文件对团队协作如此重要，所以应该加入到版本控制里面。
8.pod 管理的第三方库有 MJExtension.Framework 和 SDWebImage.Framework, 如何在MJExtension的某个类中使用来自SDWebImage库的类
    a.在pod中 找到MJExtension, 在Build Phases 中 导入SDWebImage.Framework
    b.在pod的MJExtension.Framework 中, 找到Build Settings 配置Framework Search Paths 的 Debug 和 Release, 添加 $(inherited) 和 "$PODS_CONFIGURATION_BUILD_DIR/SDWebImage"
    c.在pod的MJExtension.xcconfig中 添加 ： FRAMEWORK_SEARCH_PATHS = $(inherited) "$PODS_CONFIGURATION_BUILD_DIR/SDWebImage"
9.指定repo镜像
    pod repo remove master   
    pod repo add master https://gitee.com/mirrors/CocoaPods-Specs   （gitee镜像）
    pod repo update 
    pod repo remove master   
    pod repo add master https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git   （清华镜像）
    pod repo update 
    source 'https://gitee.com/mirrors/CocoaPods-Specs   
.git'
    source 'https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git'
```