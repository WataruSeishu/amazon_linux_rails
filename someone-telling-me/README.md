# README

# VagrantインストールからRuby、Railsのインストールまで   

## 動作環境構築について【Vagrant】

## 最新のAmazonLinuxのboxを持ってくる（Virtualbox Only）

```
vagrant init mvbcoding/awslinux
vagrant up --provider virtualbox
```

## Amazon Linuxへパッケージインストール

* Amazon LinuxのEC2インスタンスが作成されたら、ec2-userでログインする。
* gitインストール。

```
$ sudo su -
# yum -y install git
```

## Rubyインストールに必要なパッケージインストール。

```
# yum -y install gcc-c++ glibc-headers openssl-devel readline libyaml-devel readline-devel zlib zlib-devel libffi-devel libxml2 libxslt libxml2-devel libxslt-devel sqlite-devel
```

> ※libffi-develをインストールしないで、後述の「rbenv install -v X.X.X」を実行すると「./libffi-3.2.1/.libs/libffi.a: could not read symbols: Bad value」というエラーが表示されます。なので「libffi-devel」パッケージ(C/C++言語の関数を動的に呼ぶためのライブラリ)もインストールするようにしています。

## Rbenvインストール

```
# git clone https://github.com/sstephenson/rbenv.git /usr/local/rbenv
# cp -p /etc/profile /etc/profile.ORG
# diff /etc/profile /etc/profile.ORG
#

# echo 'export RBENV_ROOT="/usr/local/rbenv"'' >> /etc/profile
# echo 'export PATH="${RBENV_ROOT}/bin:${PATH}"' >> /etc/profile
# echo 'eval "$(rbenv init -)"' >> /etc/profile

# source /etc/profile
```

##ruby-buildインストール

```
# git clone https://github.com/sstephenson/ruby-build.git /usr/local/rbenv/plugins/ruby-build
# sh /usr/local/rbenv/plugins/ruby-buildu/install.sh
```

## RBENV_ROOT環境変数の有効化やrbenv init実行

```
# su - root

# env | grep RBENV
RBENV_ROOT=/usr/local/rbenv
RBENV_SHELL=bash
#
```

## インストールしたrbenvバージョン確認

```
# rbenv --version
rbenv 0.4.0-146-g7ad01b2
#
```

## Ruby インストール

```
# pwd
/root
# rbenv install -l
　 (中略)
  2.1.5
  2.2.0-dev
  2.2.0-preview1
  2.2.0-preview2
  2.2.0-rc1
  2.2.0
  2.2.1　→　このバージョンをインストールします。
  2.3.0-dev
  jruby-1.5.6
 　(中略)

# rbenv install -v X.X.X(ここの数字は適宜指定)
# rbenv rehash
# rbenv global X.X.X(指定したバージョンを再度指定)
 ```


## Railsインストール

```
# pwd
/root
# gem update --system
# gem install nokogiri -- --use-system-libraries
# gem install --no-ri --no-rdoc rails
# gem install bundler
# rbenv rehash
```


## インストールしたRailsのバージョンとgem確認

```
# rails -v
Rails X.X.X
#
# gem list

*** LOCAL GEMS ***

actionmailer (4.2.1)
actionpack (4.2.1)
(中略)
#
```

Rails環境構築完了

# DB周辺
## MariaDB

※rootユーザーのまま行う

```
vi /etc/yum.repos.d/MariaDB.repo

# MariaDB 10.1 CentOS repository list - created 2016-03-13 07:22 UTC
# http://mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.1/centos6-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
```

```
# yum install -y MariaDB-server MariaDB-client
# /etc/init.d/mysql start
初期設定
# mysql_secure_installation
# chkconfig mysql on
```

# nginx周辺

※rootユーザーのまま行う

## インストール

```
# rpm -ivh http://nginx.org/packages/centos/6/noarch/RPMS/nginx-release-centos-6-0.el6.ngx.noarch.rpm
# yum install nginx
# which nginx
/usr/sbin/nginx
```

## 起動

```
# service nginx start
# chkconfig nginx on
```
