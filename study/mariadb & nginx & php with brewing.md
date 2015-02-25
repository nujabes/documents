# 맥에 Mariadb & NGINX 설치하기

## 참고한 링크
[OSX Howto: Setting up a Nginx + PHP-FPM + PHP5.3 + MySQL dev machine (Page 1) / Laravel 3.x FAQ / Laravel Forums](http://forumsarchive.laravel.io/viewtopic.php?id=3216)
[Serving Apps Locally with Nginx and Pretty Domains | zaiste.net](http://zaiste.net/2013/03/serving_apps_locally_with_nginx_and_pretty_domains/)

<https://raw.githubusercontent.com/perusio/php-fpm-example-config/unix/fpm/php5-fpm.conf>

<https://gist.github.com/bobthecow/85ad6dfb594d9215b42b>

[Nginx, PHP-FPM, MySQL and phpMyAdmin on OS X](https://gist.github.com/mgmilcher/5eaed7714d031a12ed97)

## Nginx
restart

`sudo nginx -s stop && sudo nginx`

http://serverfault.com/questions/225948/how-to-restart-nginx-on-mac-os-x
sudo nginx -s reload

**Nginx 시작/정지**
nginx  
sudo nginx -s stop


서버 시작 nginx
서버 종료 nginx -s stop
서버 재시작 nginx -s reload

/usr/local/Cellar/nginx: NginX 관련 실행파일 및 로그, 도큐먼트 루트 위치
/usr/local/Cellar/nginx/1.2.7/html/: 도큐먼트 루트

/usr/local/etc/nginx: 설정파일들이 위치

/usr/local/sbin: NginX 원본 실행파일에 대한 심볼릭 링크 존재. 따라서 이 경로에 PATH지정을 해주면 NginX 를 어떤 경로에서든 실행 가능하다.

## PHP
```php
  * /usr/local/etc/php/5.5/conf.d/ext-memcache.ini was created,
    do not forget to remove it upon extension removal.
  * Validate installation via one of the following methods:
  *
  * Using PHP from a webserver:
  * - Restart your webserver.
  * - Write a PHP page that calls "phpinfo();"
  * - Load it in a browser and look for the info on the memcache module.
  * - If you see it, you have been successful!
  *
  * Using PHP from the command line:
  * - Run "php -i" (command-line "phpinfo()")
  * - Look for the info on the memcache module.
  * - If you see it, you have been successful!
```

## Wordpress
[WordPress - Nginx Community](http://wiki.nginx.org/WordPress)


## 명령어들
3 commands below turned out to be life-saver:

```
brew list nginx
brew list php54
brew list mysql
```

## Mariadb


https://mariadb.com/blog/installing-mariadb-10010-mac-os-x-homebrew
이거 보고 하면 되는데 기존에 있던 mysql데이타들이 자꾸 충돌 일으키는걸 몰랐네.
/usr/local/var/mysql에 있던 것들을 지워주니 잘 해결됬다.

```
To start mysqld at boot time you have to copy
support-files/mysql.server to the right place for your system

PLEASE REMEMBER TO SET A PASSWORD FOR THE MariaDB root USER !
To do so, start the server, then issue the following commands:

'/usr/local/Cellar/mariadb/10.0.16/bin/mysqladmin' -u root password 'new-password'
'/usr/local/Cellar/mariadb/10.0.16/bin/mysqladmin' -u root -h MBPR15.local password 'new-password'

Alternatively you can run:
'/usr/local/Cellar/mariadb/10.0.16/bin/mysql_secure_installation'

which will also give you the option of removing the test
databases and anonymous user created by default.  This is
strongly recommended for production servers.

See the MariaDB Knowledgebase at http://mariadb.com/kb or the
MySQL manual for more instructions.

You can start the MariaDB daemon with:
cd '/usr/local/Cellar/mariadb/10.0.16' ; /usr/local/Cellar/mariadb/10.0.16/bin/mysqld_safe --datadir='/usr/local/var/mysql'

You can test the MariaDB daemon with mysql-test-run.pl
cd '/usr/local/Cellar/mariadb/10.0.16/mysql-test' ; perl mysql-test-run.pl
```

```
MBPR15:~ ray$ brew install mariadb
==> Downloading https://downloads.sf.net/project/machomebrew/Bottles/mariadb-10.
Already downloaded: /Library/Caches/Homebrew/mariadb-10.0.16.yosemite.bottle.tar.gz
==> Pouring mariadb-10.0.16.yosemite.bottle.tar.gz
==> Caveats
A "/etc/my.cnf" from another install may interfere with a Homebrew-built
server starting up correctly.

To connect:
    mysql -uroot

To have launchd start mariadb at login:
    ln -sfv /usr/local/opt/mariadb/*.plist ~/Library/LaunchAgents
Then to load mariadb now:
    launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mariadb.plist
Or, if you don't want/need launchctl, you can just run:
    mysql.server start
==> Summary
🍺  /usr/local/Cellar/mariadb/10.0.16: 527 files, 131M
```


### aliases

为了后面管理方便，将命令 alias 下，vim ~/.bash_aliases

```
alias nginx.start='launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.nginx.plist'
alias nginx.stop='launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.nginx.plist'
alias nginx.restart='nginx.stop && nginx.start'
alias php-fpm.start="launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.php54.plist"
alias php-fpm.stop="launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.php54.plist"
alias php-fpm.restart='php-fpm.stop && php-fpm.start'
alias mysql.start="launchctl load -w ~/Library/LaunchAgents/homebrew.mxcl.mariadb.plist"
alias mysql.stop="launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mariadb.plist"
alias mysql.restart='mysql.stop && mysql.start'
接着编辑 ~/.bash_profile 文件，添加
```

`[[ -f ~/.bash_aliases ]] && . ~/.bash_aliases`

最后打开终端，更新下

`$ source .bash_profile`






## 명령어
파일 단어 찾는 명령어
`grep -ri "listen = " /usr/local/etc/php/5.5/``


