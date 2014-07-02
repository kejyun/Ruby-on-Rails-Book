# 安裝 RVM、Ruby 和 Rails

**測試日期 2014-07-02**

## 安裝 RVM 所需要套件

```shell
$ sudo apt-get install build-essential curl
```

## 下載並安裝 RVM

```shell
$ curl -L https://get.rvm.io | sudo bash -s stable
```

*rvm安裝後的目錄位置為`/usr/local/rvm`，之後所有的動作也會安裝在此目錄下。*

## 讓使用者可以執行 rvm 指令

```shell
sudo usermod -a -G rvm kejyun
```

*將使用者加入rvm群組，讓使用者可以執行rvm相關指令，上面的使用者`kejyun`請自行更改為自己主機的使用者帳號。*


## 讓 RVM 指令可執行

**實體主機** : 重新開機並重新登入

**虛擬主機** : 登出後重新登入

# 確認 RVM 版本

```shell
$ rvm -v
rvm 1.25.27 (stable) by Wayne E. Seguin <wayneeseguin@gmail.com>, Michal Papis <mpapis@gmail.com> [https://rvm.io/]
```

## 使用 RVM 安裝 Ruby 相關套件

```shell
$ rvm requirements
Checking requirements for ubuntu.
Installing requirements for ubuntu.
Updating systemkejyun password required for 'apt-get --quiet --yes update':
```

*不需要輸入`sudo`去執行，在安裝過程中若需要管理者密碼， rvm 則會詢問要求輸入管理者密碼*

```shell
..............
Installing required packages: gawk, libreadline6-dev, zlib1g-dev, libssl-dev, libyaml-dev, libsqlite3-dev, sqlite3, autoconf, libgdbm-dev, libncurses5-dev, automake, libtool, bison, libffi-dev...............
Requirements installation successful.
```

*安裝完成後會出現以上log，顯示安裝了哪些相依套件*

## 使用rvm安裝ruby 1.9.3

*實際安裝目錄為`/usr/loca/rvm/rubies`*

```shell
$ rvm install 1.9.3
```

## 設定預設的 ruby 版本

```shell
$ rvm use 1.9.3 --default
```

*安裝的時間會比較久，我使用虛擬主機大概安裝了7、8分鐘，若安裝失敗，有可能是伺服器過於忙碌，重新執行安裝指令`rvm use 1.9.3 --default`即可*

# 檢查 ruby 及 gem 的版本

```shell
$ ruby -v
$ ruby 1.9.3p547 (2014-05-14 revision 45962) [x86_64-linux]
$ gem -v
$ 2.2.2
```

## 更新Rubygems為搭配 Ruby 1.9.3 使用的版本

```shell
$ rvm rubygems current
$ gem -v
$ 2.2.2
```

*如果rubygems安裝發生問題，則使用以下指令更新rvm為head版本*

```shell
$ rvm get latest
```

## 安裝 Rails

*不安裝文件檔（安裝時間有點久，千萬要耐心等待）。會被安裝在`/usr/local/rvm/gems/ruby-1.9.3-p547/gems/rails-4.1.2`目錄下。相關的套件連同rails會被安裝28個。*

```shell
$ gem install rails --no-rdoc --no-ri
$ rails -v
$ Rails 4.0.0
```

*同上，Rails 的安裝時間也很久，如果安裝失敗，重新安裝一次即可*
