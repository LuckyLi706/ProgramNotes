# Mac

## 开发

## 逆向

## 软件

+ [Homebrew](https://brew.sh/)

  ```
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  可能会一直卡在这句话Downloading Command Line Tools (macOS Mojave version 10.14) for Xcode
  解决方案：https://leflacon.github.io/5f155707/
  
fatal: unable to access 'https://github.com/Homebrew/homebrew-core/': LibreSSL SSL_read - Homebrew
  解决方案：更换源地址
  rm -rf /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core;  
  git clone git://mirrors.ustc.edu.cn/homebrew-core.git/ /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core --depth=1
  cd "$(brew --repo)" 
  git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
  cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core" 
  git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
  ```
  
  