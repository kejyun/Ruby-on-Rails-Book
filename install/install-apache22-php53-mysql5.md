# 安裝 Apache、PHP 及 MySQL

**測試日期 2014-07-02**

## 環境

> Ubuntu : 12.04 LTS

> Apache 2.2

> PHP 5.3

*千萬不要執行 apt 套件更新的動作`sudo apt-get update`，否則 Apache 可能會被安裝為目前最新的 2.4版*

## 安裝 Apache、PHP 及 MySQL

```shell
$ sudo apt-get install apache2 php5 mysql-server
```

## 輸入 MySQL 管理者密碼


## 確認 Apache 版本

```shell
$ apache2 -v
Server version: Apache/2.2.22 (Ubuntu)
Server built:   Apr 17 2014 21:49:25
```

## 確認 PHP 版本

```
$ php -v
PHP 5.3.10-1ubuntu3.12 with Suhosin-Patch (cli) (built: Jun 20 2014 00:38:55)
Copyright (c) 1997-2012 The PHP Group
Zend Engine v2.3.0, Copyright (c) 1998-2012 Zend Technologies
```


## 設定 MySQL 資料庫編碼

*建立新的設定檔`characterset.cnf`*

```shell
$ sudo vim /etc/mysql/conf.d/characterset.cnf
```

**加入編碼設定**

```
[client]
default-character-set=utf8
[mysqld]
character-set-server=utf8
```

## 重新啟動 MySQL

```shell
$ sudo service mysql restart
```

## 檢查 MySQL 連線編碼

```
$ mysql -u root -p
Enter password:

mysql>show variables like 'character_set%';
+--------------------------+----------------------------+
| Variable_name            | Value                      |
+--------------------------+----------------------------+
| character_set_client     | utf8                       |
| character_set_connection | utf8                       |
| character_set_database   | utf8                       |
| character_set_filesystem | binary                     |
| character_set_results    | utf8                       |
| character_set_server     | utf8                       |
| character_set_system     | utf8                       |
| character_sets_dir       | /usr/share/mysql/charsets/ |
+--------------------------+----------------------------+
mysql>exit;
```
