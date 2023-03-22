# Mac

## 开发

## 逆向

## 软件

### [Homebrew](https://brew.sh/)

#### 安装

+ 命令行安装

  ```shell
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
  ```

#### 问题

+ fatal: unable to access 'https://github.com/Homebrew/homebrew-core/': LibreSSL SSL_read - Homebrew

  ```shell
  # 解决方案：更换源地址
  rm -rf /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core;  
  git clone git://mirrors.ustc.edu.cn/homebrew-core.git/ /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core --depth=1
  cd "$(brew --repo)" 
  git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
  cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" 
  git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
  ```

+ Error:  homebrew-core is a shallow clone.homebrew-cask is a shallow clone.To `brew update`, first run:...

  ```shell
  # 解决时本来很简单，只需按上述提示执行相应命令即可：但是但是默认关联 git 仓库是国外的，速度慢，还经常被墙，导致 early EOF 之类的错误：
  git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core fetch --unshallow
  git -C /usr/local/Homebrew/Library/Taps/homebrew/homebrew-cask fetch --unshallow
  
  # 更换源（国外常用仓库慢的经典解决办法，自然是临时将该仓库临时源设置为国内的镜像。一般使用中科大的）
  ## 更新 homebrew-cask
  cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
  # 更换源
  git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
  # 更新，由于已经 cd 到相应文件夹了，因此不需要通过 -C 指定路径了
  git fetch --unshallow 
  ## 更新 homebrew-core
  cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-core
  # 更换源
  git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
  # 更新
  git fetch --unshallow
  
  # 更新brew
  brew update
  ```

### [Cocoapods](IOSCocoapods.md)

