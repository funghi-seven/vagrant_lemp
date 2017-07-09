vagrant_lemp
====

サクッと開発環境を作るためのVagrantfileとansible Playbook

## Description

以下の構成で作ります

* CentOS6 (latest)
* php 7.1
* nginx (latest)
* mysql 5.6

### CentOSにインストールするリポジトリ

  * webtatic
    * gitの最新版を入れるため
  * IUS
    * php 7.1関係を入れるため
  * epel
    * 依存
  * nginx
  * mysql

### インストール後の設定

まだ書いてない

## Requirement

* VirtualBox
* Vagrant

## Usage

```vagrant up```

## Licence

[MIT](https://github.com/tcnksm/tool/blob/master/LICENCE)

