---
auther: もりしー
title: "Ruby環境の作り方"
date: 2013-10-30 20:20
tags: Ruby, すごい広島
---

もりしーです。  
この開発記録は[Ruby](https://www.ruby-lang.org/ja/)製の[Middleman](http://middlemanapp.com/)によって作成されています。  
従ってRubyが無ければ記録を残すことが出来ないので導入方法をまとめておきます。  


1.必要なパッケージをインストールする  
<code>
	$ su - <br>
  # apt-get install build-essential bison libreadline6-dev<br>
  		curl git-core zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev<br>
  		sqlite3 libxml2-dev libxslt1-dev autoconf libncurses5-dev<br>
  # exit
</code>

2.rbenvとruby-buildをgithubからクローンする  
<code>
  $ cd<br>
  $ git clone git://github.com/sstephenson/rbenv.git .rbenv<br>
  $ git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build <br>
</code>

3.rbenvが使えるようにする  
bashの場合は`~/.bashrc`、zshの場合は`~/.zshrc`に下記の項目を追記する  
<code>
  export PATH="$HOME/.rbenv/bin:$PATH"<br>
  eval "$(rbenv init -)"
</code>
追記後に`source ~/.bashrc`もしくは`source ~/.zshrc`を実行する  

4.正常にrbenvの導入が出来ていれば、下記のように表示される  
<code>
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
</code>

5.導入可能Rubyのバージョンを調べる  
<code>
  $ rbenv install --list
</code>
とすると導入可能なRubyのバージョン一覧が表示される。(大量に有るので一部省略)  
<code>
	Available versions:<br>
  ~ 省略 ~<br>
  1.9.3-p448<br>
  1.9.3-preview1<br>
  1.9.3-rc1<br>
  2.0.0-p195<br>
  2.0.0-p247<br>
  2.0.0-preview2<br>
  2.0.0-rc2<br>
  2.1.0-dev<br>
  2.1.0-preview1<br>
  ~ 省略 ~<br>
</code>

6.Rubyをインストールする
特に指定がなければ`-rc`や`-dev`、`-preview`ではない最新の安定板を入れましょう。  
<code>
	$ rbenv install 2.0.0-p247
</code>
インストールには少し時間がかかります。  
ちなみにRaspberry Piでは３時間かかります。  

7.rbenvでインストールしたRubyを読ませる。  
<code>
  $ rbenv rehash<br>
  $ rbenv global 2.0.0-p247<br>
  $ ruby --version<br>
  ruby 2.0.0p247 (2013-06-27 revision 41674) [x86_64-darwin12.4.0]<br>
</code>

これでRubyのインストール完了です。  
Rubyに興味が有るなら、こちらのコミュニティをおすすめします。  
[広島Ruby勉強会](http://hiroshimarb.github.io/)		

もしrbenvやruby-buildを更新したい場合は該当ディレクトリに移動し`git pull`して`source ~/.bashrc`もしくは`source ~/.zshrc`を実行すると更新されます。  
  
  
追伸  
記録を書くときに`bundle install`を実行しますが、実行時間を短くする小技としては  
`~/.gemrc`ファイルを作成し、`gem: --no-ri --no-rdoc`と書いておくとよいでしょう。  