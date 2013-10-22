# リポジトリからクローンしたときに実行する
## bundle install
## sapodeveloper.middlemanにpushできるようにする
task :setup do
	sh 'bundle install'
	sh 'git remote add middleman git@github.com:sapodeveloper/sapodeveloper.middleman.git'
end

#　middlemanサーバを起動する
task :preview do
  sh 'bundle exec middleman'
end

# 作成した記事をデプロイする
## sapodeveloper.middlemanに変更点をpush
## sapodeveloper.github.ioにbuildする
task :deploy do
	sh 'git push middleman master'
	sh 'bundle exec middleman deploy'
end