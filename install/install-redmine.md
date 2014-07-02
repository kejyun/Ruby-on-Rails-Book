# 安裝 Redmine

> Redmine 是一個網頁界面的專案管理與缺陷跟蹤管理系統的自由及開放原代碼的軟體工具。它整合了專案管理所需的各項功能：日曆 和 甘特圖 以協助視覺化表現專案與時間限制，事件追蹤和版本控制。此外，Redmine也可以同時處理多個項目。

> 資料來源 : [Redmine - 維基百科，自由的百科全書](http://zh.wikipedia.org/wiki/Redmine)



## 建立 Redmine 在 MySQL需要的帳號密碼

```
$ mysql -u root -p
Enter password:

mysql>CREATE DATABASE redmine CHARACTER SET utf8;
mysql>CREATE USER 'redmine'@'localhost' IDENTIFIED BY 'my_password';
mysql>GRANT ALL PRIVILEGES ON redmine.* TO 'redmine'@'localhost';
mysql>flush privileges;
mysql>exit;
```

## 下載 Redmine

*看看你們安裝的時候，到[Redmine官方網站](http://www.redmine.org/projects/redmine/wiki/Download)看可下載板本為何，在自己調整下載指令*

```shell
$ wget http://www.redmine.org/releases/redmine-2.5.1.tar.gz
$ tar -xzvf redmine-2.5.1.tar.gz
```

## 移動 Redmine 相關檔案

```shell
$ sudo mv redmine-2.5.1 /usr/share
```

## 設定 Redmine 資料夾連結

*將`/usr/share/redmine`連結到`/usr/share/redmine-2.5.1`*

```shell
$ sudo ln -s /usr/share/redmine-2.5.1 /usr/share/redmine
```

## 複製並設定 Redmine 資料庫設定檔

```
$ cp /usr/share/redmine/config/database.yml.example /usr/share/redmine/config/database.yml

$ vim /usr/share/redmine/config/database.yml
```

*將 MySQL 資料庫的帳號密碼設定到設定檔中*

```
production:
  adapter: mysql2
  database: redmine
  host: localhost
  username: redmine
  password: "my_password"
  encoding: utf8
```

## 複製並設定 Redmine 相關設定

```
$ cp /usr/share/redmine/config/configuration.yml.example /usr/share/redmine/config/configuration.yml

$ vim /usr/share/redmine/config/configuration.yml
```

*使用 Gmail SMTP 伺服器作寄送的服務*

```
production:
  email_delivery:
  delivery_method: :smtp
  smtp_settings:
    #tls: true
    enable_starttls_auto: true
    address: "smtp.gmail.com"
    port: 587
    domain: "smtp.gmail.com" # 'your.domain.com' for GoogleApps
    authentication: :plain
    user_name: "your_email@gmail.com"
    password: "your_password"
```

*記得要將`tls: true`這一行拿掉，否則會發生 SSL error。*



## 安裝及設定 Bundler


```shell
$ gem install bundler --no-rdoc --no-ri
$ sudo apt-get install libmagickwand-dev libmysql-ruby libmysqlclient-dev
$ gem install mysql2
$ cd /usr/share/redmine
$ bundle install --without development test postgresql sqlite
```

## 產生 session store secret

```shell
$ rake generate_secret_token
```

*如果發生 mysql 錯誤，需要再安裝 gem 的`mysql2`*

## 產生並建立 Redmine 資料庫

```
$ cd /usr/share/redmine
$ RAILS_ENV=production rake db:migrate
```

## 產生 Redmine 預設的組態資料

```shell
$ cd /usr/share/redmine
$ RAILS_ENV=production rake redmine:load_default_data

Select language: ar, az, bg, bs, ca, cs, da, de, el, en, en-GB, es, et, eu, fa, fi, fr, gl, he, hr, hu, id, it, ja, ko, lt, lv, mk, mn, nl, no, pl, pt, pt-BR, ro, ru, sk, sl, sq, sr, sr-YU, sv, th, tr, uk, vi, zh, zh-TW [en] zh-TW
====================================
Default configuration data loaded.
```

*命令列會提示預設語言，按ENTER使用預設的`英語`。或輸入`zh-TW`設定使用繁體中文的語言*







