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
	sh 'bundle exec middleman build'
	sh 'bundle exec middleman deploy'
end

# ブログ記事のベースを作る
task :new_post, :title do |t, args|
	# ファイル名が無ければ終了
	if args.title
    title = args.title
  else
    puts "rake aborted! please input title"
    exit
  end
 
  # ファイルを生成するパスを指定する。
  path = "source/blog/"
  path += Time.now.strftime('%Y/%m')
  # ファイル作成年月のフォルダが無ければフォルダを作成する。
  FileUtils.mkdir_p(path) unless FileTest.exist?(path)
 
  #ファイルを作成する
  year = Time.now.strftime('%Y')
  month = Time.now.strftime('%m')
  created_at = Time.now.strftime('%Y-%m-%d')
  filename = "source/blog/#{year}/#{month}/#{created_at}-#{title}.html.markdown"
  if File.exist?(filename)
    puts "rake aborted! 既にファイルが存在しています。"
    exit
  end
  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""
    post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M')}"
    post.puts "tags: "
    post.puts "---"
  end
end