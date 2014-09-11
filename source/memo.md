cOtopress
--------------

* [Octopress](http://octopress.org/)

* [Big Sky :: githubとjekyllとoctopressで作る簡単でモダンなブログ](
http://mattn.kaoriya.net/software/lang/ruby/20111017205717.htm)
* [Octopressのインストールから運用管理まで](https://tokkonopapa.github.io/blog/2011/12/30/octopress-on-github-and-bitbucket/)
* [GithubとOctopressでモダンな技術系ブログを作ってみる](http://blog.glidenote.com/blog/2011/11/07/install-octopress-on-github/)

##### スタートガイド
* [Octopress簡単スタートガイド](http://www.slideshare.net/yizawa/octopress)
* [OctopressでGitHub無料ブログ構築。sourceをBitbucket管理。簡単ガイド！](https://morizyun.github.io/blog/octopress-gitpage-minimum-install-guide/)


* [Markdownで書いてGitで管理するブログ「Octopress」の始め方](http://tantant.jp/blog/Octopress/installing-octopress/)

* [エンジニアのブログは Octopress が最適](http://blog.shiroyama.us/blog/2014/02/26/octopress/)


##### テーマ

* [GitHub Pages + Octopress カスタマイズ](http://qiita.com/syui/items/07365ed24eef63602233)
* [3rd Party Octopress Themes](https://github.com/imathis/octopress/wiki/3rd-Party-Octopress-Themes)

* [Octostrap](https://kaworu.github.io/octopress/)

--------------

### 参考ページ
* [GithubとOctopressでモダンな技術系ブログを作ってみる](http://blog.glidenote.com/blog/2011/11/07/install-octopress-on-github/)
* [Octopressでのプレビュー方法](https://rcmdnk.github.io/blog/2013/05/20/blog-octopress/#rake-preview)

ログ
-------
$ cd ~/mnt/doc/workspace/sites
$ git clone git://github.com/imathis/octopress.git octopress
$ cd octopress
$ cd !$

$ gem install bundler
$ bundle install

デフォルトテーマの設定
$ rake install

GitHub pageの設定
$ rake setup_github_pages
Enter the read/write url for your repository: git@github.com:openkawasaki/openkawasaki.github.io.git

$ vi Gemfile
gem 'execjs'
gem 'therubyracer'

staticサイトの生成
$ rake generate

GitHubにデプロイ(コミット)
$ rake deploy

ローカルでのpreview
$ rake preview
 or
$ rackup --port 8000
 or
$ cd public
$ python -m SimpleHTTPServer


例） http://glidenote.github.com/ 

Octopressの初期設定
[設定はConfiguring Octopress – Octopress](http://octopress.org/docs/configuring/)

url:                # For rewriting urls for RSS, etc
title:              # Used in the header and title tags
subtitle:           # A description used in the header
author:             # Your name, for RSS, Copyright, Metadata
simple_search:      # Search engine for simple site search
subscribe_rss:      # Url for your blog's feed, defauts to /atom.xml
subscribe_email:    # Url to subscribe by email (service required)
email:              # Email address for the RSS feed if you want it.

url:                # RSSに記載するためのブログURL
title:              # HTMLのヘッダとタイトルタグに使うブログのタイトル
subtitle:           # HTMLのヘッダ部分に表示するブログのサブタイトル
author:             # コピーライトやメタタグなどに使うブログの著者情報
simple_search:      # ブログ内の検索機能におけるサーチエンジン
description:        # デフォルトのメタタグ内descriptionの内容
date_format:        # 日付のフォーマット(Ruby's date strftime syntax)
subscribe_rss:      # ブログのRSSのURL(デフォルトは /atom.xml)
subscribe_email:    # e-mailを使ったブログの購読のためのURL
category_feeds:     # カテゴリ単位でのRSSを許可するか？ (デフォルトはfalse)
email:              # RSSのためのメールアドレス(必要な場合のみ)



$ echo 'openkawasaki.org' >> source/CNAME
$ echo 'openkawasaki.org' >> source/README.md

設定を修正したら
$ rake gen_deploy


新規記事の投稿
$ rake new_post["title"]

ここで指定するtitleはURLに利用されるので、日本語は利用不可のようです。（記事自体のタイトルには日本語可)

	$ rake new_post\["test post"\]
 
	$ mkdir -p source/_posts
	$ Creating new post: source/_posts/2011-11-07-test-post.markdown

	$ source/_posts/2011-11-07-test-post.markdown

	---
	layout: post
	title: "test post"
	date: 2011-11-07 15:02
	comments: true
	categories:
	---
	ここにテキストを書く  


	rake gen_deploy
	でデプロイ。

--------------


githubのmasterブランチに、手元のoctopressでgenerate したファイルがコミットされる。   
ブランチ名：master  →  static  サイト用コンテンツ   				source  →  octopress⽤の記事ソース

octopress自体もsourceブランチに登録する。
$ git add .
$ git commit -m "some message" 
$ git push origin source




• 設定は以下のファイルに記述する。 
_config.yml … Main config (Jekyll's settings) 
Rakefile … Configs for deployment 
config.rb … Compass config 
config.ru … Rack config

記事を投稿する
% rake new_post["title"] 
source/_posts/ の下に、YYYY-MM-DD-post-title.markdown とい うファイルが出来るので、これを編集する。

記事の執筆 
以下の様なYAML形式のヘッダが生成されているので、その下に文章を書いていく。
--- 
layout: post 
title: "title" 
date: 2014-04-19 0:59 +0900 
comments: true 
categories: 
--- 


code snipet 
バッククオート3つで囲うと簡単にコードを埋め込める。
``` ruby class sample 
class MyClass 
  def initializer 
  end 
end 
``` 

gistの埋め込み 
{% gist gist_id [filename] %} でgistを埋め込める。 

例：{% gist 9109720 %}
 
その他スニペットたち 
{% include_code %} 
{% codeblock %} ∼ {% endcodeblock %} 
{% video %} 
{% image %}
参照:
http://octopress.org/docs/blogging/code/
http://octopress.org/docs/blogging/plugins/

blogテーマを変更更する

octopressのテーマリポジトリ 
•  http://opthemes.com/

テーマをダウンロード 
テーマのリポジトリを、手元に clone する。
例: 「Shash」というテーマを持ってきて適用する。 
% cd octopress 
% git clone git://github.com/tommy351/Octopress-Theme-Slash.git .themes/slash 
% rake install['slash'] 
% rake generate 



----------

$ cd ~/mnt/doc/workspace/sites
$ git clone git://github.com/imathis/octopress.git homata
$ cd homata

bundleが無かったら
$ gem install bundler

$ bundle install

テーマboldandblueをインストール
$ git clone https://github.com/johnkeith/boldandblue.git .themes/boldandblue
$ rake install['boldandblue']


staticサイトの生成
$ rake generate

ローカルでのpreview
$ rake preview 


以下のエラーがでる
	Build Warning: Layout 'nil' requested in atom.xml does not exist.
	Build Warning: Layout 'nil' requested in robots.txt does not exist.

http://www.bravo-kernel.com/blog/2014/08/how-to-fix-octopress-build-warning-layout-nil-requested/
以下の2ファイルを変更
./source/atom.xml
./source/robots.txt
	layout: nil  ->  null

Octopress で GitHub Pages を置き換える
http://randd.kwappa.net/2013/04/16/521

GitHubにhomata.github.ioというリポジトリを作成する

GitHub pageの設定
$ rake setup_github_pages
Enter the read/write url for your repository: git@github.com:homata/homata.github.io

$ vi Gemfile
gem 'execjs'
gem 'therubyracer'

staticサイトの生成
$ rake generate

$ echo 'homata.com' >> source/CNAME
$ echo 'homata.com' >> source/README.md

GitHubにデプロイ(コミット)
$ rake deploy


例） http://glidenote.github.com/ 

Octopressの初期設定
[設定はConfiguring Octopress – Octopress](http://octopress.org/docs/configuring/)

url:                # For rewriting urls for RSS, etc
title:              # Used in the header and title tags
subtitle:           # A description used in the header
author:             # Your name, for RSS, Copyright, Metadata
simple_search:      # Search engine for simple site search
subscribe_rss:      # Url for your blog's feed, defauts to /atom.xml
subscribe_email:    # Url to subscribe by email (service required)
email:              # Email address for the RSS feed if you want it.

url:                # RSSに記載するためのブログURL
title:              # HTMLのヘッダとタイトルタグに使うブログのタイトル
subtitle:           # HTMLのヘッダ部分に表示するブログのサブタイトル
author:             # コピーライトやメタタグなどに使うブログの著者情報
simple_search:      # ブログ内の検索機能におけるサーチエンジン
description:        # デフォルトのメタタグ内descriptionの内容
date_format:        # 日付のフォーマット(Ruby's date strftime syntax)
subscribe_rss:      # ブログのRSSのURL(デフォルトは /atom.xml)
subscribe_email:    # e-mailを使ったブログの購読のためのURL
category_feeds:     # カテゴリ単位でのRSSを許可するか？ (デフォルトはfalse)
email:              # RSSのためのメールアドレス(必要な場合のみ)


設定を修正したら
$ rake gen_deploy

ソースもGitHubへ
setup_github_pages すると、octopress以下はsourceというブランチだけになる。


GitHubにgithubにhomata.octopressというリポジトリを作成する

あらかじめgithubにhomata.octopressというリポジトリを作っておいて…

% git remote add github git@github.com:homata/homata.octopress.git
% git push github source

記事を投稿する
$ rake new_post["namie fellow"]
$ rake gen_deploy

staticサイトの生成
$ rake generate
ローカルでのpreview
$ rake preview 

