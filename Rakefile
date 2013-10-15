# coding: utf-8
require 'bundler/setup'
require 'thread'
require 'launchy'
require 'date'

task :preview do
  sh 'bundle exec jekyll serve --watch'
end

task :new_post, :title do |t, args|
	# ファイル名が無ければ終了
	if args.title
    title = args.title
  else
    puts "rake aborted! please input title"
    exit
  end

  # ファイルを生成するパスを指定する。
  path = "_posts/"
  path += Time.now.strftime('%Y/%m')
  # ファイル作成年月のフォルダが無ければフォルダを作成する。
  FileUtils.mkdir_p(path) unless FileTest.exist?(path)

  #ファイルを作成する
  year = Time.now.strftime('%Y')
  month = Time.now.strftime('%m')
  created_at = Time.now.strftime('%Y-%m-%d')
  filename = "_posts/#{year}/#{month}/#{created_at}-#{title}.markdown"
  if File.exist?(filename)
    puts "rake aborted! 既にファイルが存在しています。"
    exit
  end
  puts "Creating new post: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: post"
    post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""
    post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M')}"
    post.puts "comments: true"
    post.puts "categories: "
    post.puts "---"
  end
end

task :new_page, :create_page do |t, args|
	# ファイル名が無ければ終了
	if args.create_page
    create_page = args.create_page
  else
    puts "rake aborted! please input create page name"
    exit
  end

  # ファイルを生成するパスを指定する。
  path = "pages/#{create_page}"
  # ファイル作成年月のフォルダが無ければフォルダを作成する。
  FileUtils.mkdir_p(path) unless FileTest.exist?(path)

  #ファイルを作成する
  filename = "pages/#{create_page}/index.md"
  if File.exist?(filename)
    puts "rake aborted! 既にファイルが存在しています。"
    exit
  end
  puts "Creating new page: #{filename}"
  open(filename, 'w') do |post|
    post.puts "---"
    post.puts "layout: page"
    post.puts "title: \"#{create_page.gsub(/&/,'&amp;')}\""
    post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M')}"
    post.puts "---"
  end
end
