---
auther: もりしー
title: "Ruby環境の作り方"
date: 2013-10-30 20:20
tags: Ruby, すごい広島
---

モリシーです。  
この開発記録は[Ruby](https://www.ruby-lang.org/ja/)製の[Middleman](http://octopress.org/)によって作成されています。  
従ってRubyが無ければ記録を残すことが出来ないので導入方法をまとめておきます。  


1.必要なパッケージをインストールする  
<code>
	$ su -
  # apt-get install build-essential bison libreadline6-dev curl git-core zlib1g-dev
  	 libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev autoconf libncurses5-dev
  # exit
</code>

2.rbenvとruby-buildをgithubからクローンする  
```
  $ cd
  $ git clone git://github.com/sstephenson/rbenv.git .rbenv
  $ git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build 
```

3.rbenvが使えるようにする  
bashの場合は`~/.bashrc`、zshの場合は`~/.zshrc`に下記の項目を追記する  
```
  export PATH="$HOME/.rbenv/bin:$PATH"
  eval "$(rbenv init -)"
``` 
追記後に`source ~/.bashrc`もしくは`source ~/.zshrc`を実行する  

4.正常にrbenvの導入が出来ていれば、下記のように表示される  
```
  $rbenv
  rbenv 0.4.0-52-g1cc7536(ここは導入したバージョンによって変わる)
	Usage: rbenv <command> [<args>]

	Some useful rbenv commands are:
	   commands    List all available rbenv commands
	   local       Set or show the local application-specific Ruby version
	   global      Set or show the global Ruby version
	   shell       Set or show the shell-specific Ruby version
	   install     Install a Ruby version using the ruby-build plugin
	   uninstall   Uninstall a specific Ruby version
	   rehash      Rehash rbenv shims (run this after installing executables)
	   version     Show the current Ruby version and its origin
	   versions    List all Ruby versions available to rbenv
	   which       Display the full path to an executable
	   whence      List all Ruby versions that contain the given executable

	See `rbenv help <command>' for information on a specific command.
	For full documentation, see: https://github.com/sstephenson/rbenv#readme
```

5.導入可能Rubyのバージョンを調べる  
```
  $ rbenv install --list
```
とすると導入可能なRubyのバージョン一覧が表示される。(大量に有るので一部省略)  
```
	Available versions:
  ~ 省略 ~
  1.9.3-p448
  1.9.3-preview1
  1.9.3-rc1
  2.0.0-p195
  2.0.0-p247
  2.0.0-preview2
  2.0.0-rc2
  2.1.0-dev
  2.1.0-preview1
  ~ 省略 ~
```

6.Rubyをインストールする
特に指定がなければ`-rc`や`-dev`、`-preview`ではない最新の安定板を入れましょう。  
```
	$ rbenv install 2.0.0-p247
```
インストールには少し時間がかかります。  
ちなみにRaspberry Piでは３時間かかります。  

7.rbenvでインストールしたRubyを読ませる。  
```
  $ rbenv rehash
  $ rbenv global 2.0.0-p247
  $ ruby --version
  ruby 2.0.0p247 (2013-06-27 revision 41674) [x86_64-darwin12.4.0]
```

これでRubyのインストール完了です。  
Rubyに興味が有るなら、こちらのコミュニティをおすすめします。  
[広島Ruby勉強会](http://hiroshimarb.github.io/)		

もしrbenvやruby-buildを更新したい場合は該当ディレクトリに移動し`git pull`して`source ~/.bashrc`もしくは`source ~/.zshrc`を実行すると更新されます。  
  
  
追伸  
記録を書くときに`bundle install`を実行しますが、実行時間を短くする小技としては  
`~/.gemrc`ファイルを作成し、`gem: --no-ri --no-rdoc`と書いておくとよいでしょう。  