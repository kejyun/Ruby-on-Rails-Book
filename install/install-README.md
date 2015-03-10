# 安裝

**測試日期 2014-07-02**

## 環境

> Ubuntu : 12.04 LTS

> Apache 2.2

> PHP 5.3

> Ruby : 1.9.3

> Passenger : 4.0.45

# 備註

千萬不要將 Apache 升級至 2.4 版，或將 PHP 升級至5.5版，Passenger Apache外掛目前只支援 Apache 2.2版，我傻傻的升級到了2.4，一直出現衝突無法安裝正確的套件，看看之後什麼時候會支援 2.4 版的 Apache

也千萬不要將 PHP 從 5.3 升級至 5.5，他會幫你連 Apache 一起升級到 2.4 版，一升級後整個GG，為了安裝 Passenger Apache 套件卡了很久

# 參考資料

* [Using Source Package架設redmine做專案管理Step By Step with Ubuntu 13.04](http://mrtonychen.wordpress.com/2013/08/26/using-source-package-%E5%AE%89%E8%A3%9D-redmine-2-3-2-with-ubuntu-13-04/)
* [How To Install Rails, Apache, and MySQL on Ubuntu with Passenger | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-rails-apache-and-mysql-on-ubuntu-with-passenger)
* [\[備註\] 安裝 RVM and Ruby@Ubuntu 13.04 x64 | Kenmingの鮮思維](http://www.kenming.idv.tw/note_install_rvm-and-ruby_at-ubuntu-13-04-x64)

