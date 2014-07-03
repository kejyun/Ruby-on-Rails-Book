# 安裝 Passenger

## 環境

> Ubuntu : 12.04 LTS

> Ruby : 1.9.3

> Passenger : 4.0.45

*在安裝完 apache 2.2 後，不要對 apache 設定檔進行任何修改，在安裝 Passenger 實會修改 Apache 核心及設定檔，若有自己的設定檔，請自行備份，確認不要被新的設定檔覆蓋了*

## 使用 Gem 安裝 Passenger

```
$ gem install passenger
```

## 安裝 Apache Passenger 模組

```shell
$ passenger-install-apache2-module
```

*安裝過程會檢查所需要的套件，如果發生錯誤，請依照 Passenger 的指示，安裝其需要的套件*

```
Checking for required software...

 * Checking for C compiler...
      Found: yes
      Location: /usr/bin/cc
 * Checking for C++ compiler...
      Found: yes
      Location: /usr/bin/c++
 * Checking for Curl development headers with SSL support...
      Found: no
      Error: Cannot find the `curl-config` command.
 * Checking for OpenSSL development headers...
      Found: yes
      Location: true
 * Checking for Zlib development headers...
      Found: yes
      Location: true
 * Checking for Apache 2...
      Found: yes
      Location of httpd: /usr/sbin/apache2
      Apache version: 2.2.22
 * Checking for Apache 2 development headers...
      Found: no
 * Checking for Rake (associated with /usr/local/rvm/gems/ruby-1.9.3-p547/wrappers/ruby)...
      Found: yes
      Location: /usr/local/rvm/gems/ruby-1.9.3-p547/wrappers/rake
 * Checking for OpenSSL support for Ruby...
      Found: yes
 * Checking for RubyGems...
      Found: yes
 * Checking for Ruby development headers...
      Found: yes
      Location: /usr/local/rvm/rubies/ruby-1.9.3-p547/include/ruby-1.9.1/ruby.h
 * Checking for rack...
      Found: yes
 * Checking for Apache Portable Runtime (APR) development headers...
      Found: no
 * Checking for Apache Portable Runtime Utility (APU) development headers...
      Found: no

Some required software is not installed.
But don't worry, this installer will tell you how to install them.
Press Enter to continue, or Ctrl-C to abort.

--------------------------------------------

Installation instructions for required software

 * To install Curl development headers with SSL support:
   Please run apt-get install libcurl4-openssl-dev or libcurl4-gnutls-dev, whichever you prefer.

 * To install Apache 2 development headers:
   Please install it with apt-get install apache2-threaded-dev

 * To install Apache Portable Runtime (APR) development headers:
   Please install it with apt-get install libapr1-dev

 * To install Apache Portable Runtime Utility (APU) development headers:
   Please install it with apt-get install libaprutil1-dev

```

**我這邊欠缺的套件為下列套件，所以需要再重新安裝**

``` shell
$ sudo apt-get install libcurl4-openssl-dev apache2-threaded-dev libapr1-dev libaprutil1-dev
```

*重新安裝完套件後，再次執行`passenger-install-apache2-module`安裝 Apache Passenger 套件即可*

*安裝過程會需要編譯 apache 套件，所以需要一點時間*


## 確認 Passenger 需要在 Apache 設定的資料

*這𥚃要特別注意，因為passenger會一直更新版本，以下的設定`千萬不要直接拿去貼上`，否則會出現錯誤。請直接複製在apache-passenger後在螢幕上顯示的文字。*

```
LoadModule passenger_module /usr/local/rvm/gems/ruby-1.9.3-p547/gems/passenger-4.0.45/buildout/apache2/mod_passenger.so
<IfModule mod_passenger.c>
  PassengerRoot /usr/local/rvm/gems/ruby-1.9.3-p547/gems/passenger-4.0.45
  PassengerDefaultRuby /usr/local/rvm/gems/ruby-1.9.3-p547/wrappers/ruby
</IfModule>
```

## 設定 Passenger 在 Apahe 的設定檔

*建立新的設定檔`passenger.conf`*

```shell
$ sudo vim /etc/apache2/conf.d/passenger.conf
```

*貼上上面 Passenger 產生的設定檔*

```
LoadModule passenger_module /usr/local/rvm/gems/ruby-1.9.3-p547/gems/passenger-4.0.45/buildout/apache2/mod_passenger.so
<IfModule mod_passenger.c>
  PassengerRoot /usr/local/rvm/gems/ruby-1.9.3-p547/gems/passenger-4.0.45
  PassengerDefaultRuby /usr/local/rvm/gems/ruby-1.9.3-p547/wrappers/ruby
</IfModule>
```

## 設定 Ruby on Rails 檔案程式虛擬機

*接下來會安裝 Redmine 當作測試程式，所以以下以redmine做設定範例*

*建立虛擬主機設定檔`redmine`*

```shell
sudo vim /etc/apache2/sites-available/redmine
```

*虛擬主機設定*

* 名稱 : dev.redmine
* 目錄 : /usr/share/redmine/public


```
<VirtualHost *:80>
  ServerName dev.redmine
  # !!! Be sure to point DocumentRoot to 'public'!
  DocumentRoot /usr/share/redmine/public
  <Directory /usr/share/redmine/public>
     # This relaxes Apache security settings.
     AllowOverride all
     # MultiViews must be turned off.
     Options -MultiViews
     # Uncomment this if you're on Apache >= 2.4:
     #Require all granted
  </Directory>
</VirtualHost>
```

## 啟動虛擬主機設定檔

```
$ sudo a2ensite redmine
Enabling site redmine.
To activate the new configuration, you need to run:
  service apache2 reload
```

## 重新讀取 Apache 新的設定

```shell
$ sudo service apache2 reload
```
