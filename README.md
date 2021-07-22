Ruby on Rails を使った実践的な開発方法を学びます
Devise を使った認証機能の開発を行います
画像アップロード機能の開発を行います
seed を使った初期データの投入方法を学びます
Hammer.js を使ってスワイプ機能の開発を行います
中間テーブルを利用したデータベース設計方法を学びます
Action Cable を使ってリアルタイムでメッセージを送る機能の開発を行います

settings.jsonファイルに以下のコードをコピーします（内容を理解する必要はありません）。

json
{
    // 差分を横に並べて表示せずに、行内に表示する
    "diffEditor.renderSideBySide": false,
    // ファイル保存時に自動フォーマットする
    "editor.formatOnSave": true,
    // 現在の行を強調表示する
    "editor.renderLineHighlight": "all",
    // 空白文字を表示する
    "editor.renderWhitespace": "all",
    // スペース2個分のインデント
    "editor.tabSize": 2,
    // ウィンドウ幅右端で折り返す
    "editor.wordWrap": "on",
    // ファイル保存時に新しい行を末尾に挿入する
    "files.insertFinalNewline": true,
    // アイコンテーマの指定
    "workbench.iconTheme": "vscode-icons"
}
このコードをコピー＆ペーストしたら、settings.jsonファイルを上書きして保存します。
（command + Sキーを押して上書き保存ができます）

● Ruby
  → VSCodeに対するRuby言語とデバッグサポートを提供する。

● Japanese Language Pack for Visual Studio Code
  → 日本語対応のVSCodeのUIを提供する。

● vscode-icons
  → ファイルやフォルダにアイコンを追加する。
それでは拡張機能を追加します。

●Homebrewをインストール
ソフトウェアの導入を簡単にするため、macOS用のパッケージ管理システムであるHomebrewをインストールします。
brew -v

Homebrew 2.5.8
Homebrew/homebrew-core (git revision 8ef7f; last commit 2020-11-05)
Homebrew/homebrew-cask (git revision 0e83ed; last commit 2020-11-05)
「Homebrew 2.5.8」とバージョンが表示され、Homebrewがインストールされたことが確認できました。

●rbenvをインストール
次に、Rubyのバージョンを簡単に切り替えられるrbenvをインストールします。

brew install rbenv
コマンドを実行後に、実際にrbenvがインストールされているかを確認します。

rbenv --version
コマンドを実行すると、次のようにバージョン情報が表示されます。

rbenv --version
rbenv 1.1.2
この表示では「rbenv 1.1.2」とバージョン情報が表示されています。

rbenvがインストールされたことを確認できました。

●rbenvにPATHを通す
rbenvコマンドを利用するために、rbenvにPATHを通します。

「PATHを通す」とは、コマンドの実行ファイルの場所を確認するために指定することです。

参考：PATHを通すとは？（Mac OS X）

rbenvコマンドのPATHを通すために、次の3つのコマンドを用意しました。

console
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
source ~/.bash_profile
これらのコマンドを１行ずつ入力して、実行します。

まずは最初のコマンドです。

スクリプトを.bash_profileに追加します。

console
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile
>> ~/.bash_profileでスクリプトを.bash_profileに追加しました。

次に、２番めのコマンドを入力して実行します。

console
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
このコマンドを追加することで、ターミナル起動時にrbenvを自動的に起動させます。

最後に、sourceというコマンドを使って追加した内容を反映します。

console
source ~/.bash_profile
.bash_profileに追加した内容を反映できました。

これでrbenvコマンドを利用するのに必要なPATHが通りました。

●Rubyをインストール
次にRubyをインストールします。

Rubyをインストールする前に、インストールできるRubyのバージョンを確認します。

rbenv install -l
コマンドを実行すると、最新の安定版のバージョンが一覧で表示されます。

もし最新バージョンが表示されない場合は、rbenvとruby​​-buildを最新版にする必要があります。

参考：rbenv Upgrading with Homebrew

それでは、次のコマンドを入力してRuby 2.7.2をインストールします。

console
rbenv install 2.7.2
コマンドを実行するとインストールを開始します。インストール完了まで数分間かかることがあります。

これでRubyがインストールされました。

ローカルで使うRubyのバージョンを指定
さらにローカルで使うRubyのバージョンを指定するために、以下のコマンドを実行します。

console
rbenv local 2.7.2
これでローカルでRubyの2.7.1のバージョンが使用されます。

このようにlocalを使うと、プロジェクトごとにRubyのバージョンを指定できます。

PC（サーバー）内で同じバージョンを共通して使う場合は、localではなくglobalを使います。

次に、Rubyのバージョン情報を確認します。次のコマンドを入力します。

console
ruby -v
コマンドを実行すると、次のようにバージョンが表示されます。

●Bundlerをインストール
Rubyをインストールしたら、次にBundlerをインストールします。

RubyではGemというライブラリを使いパッケージを管理しています。

Gemコマンドで簡単にインストールやアンインストールができますが、複数のGemを使うとGem同士で依存関係が生まれ、バージョン違いによる不具合が出てきます。

そこで、BundlerでGemのそれぞれのバージョンを正確に追跡し管理して、Rubyプロジェクトに一貫した環境を提供します。

console
bundler -v
コマンドの実行後、次のように表示されます。

console
bundler -v
Bundler version 2.1.4
「version 2.1.4」とバージョン情報が表示されました。

これでBlundlerがインストール済みであることを確認できました。

●yarnをインストール
次にyarnをインストールします。

yarnはJavaScriptのライブラリの利用に必要なパッケージマネージャです。

yarnと互換性のあるnpmというパッケージマネージャもあります。しかし、Rails6ではWebpackerが標準になったことにより、yarnが必要です。

それでは、yarnのインストールを行いましょう。

次のコマンドを入力します。

console
brew install yarn
Homebrewのコマンドを実行すると、yarnがインストールされます。

yarnが実際にインストールされたかを確認するために、次のコマンドを入力します。

yarn -v
1.16.0
ここでは「1.16.0」と表示されました。バージョン情報が表示されていれば、yarnがインストールされたことが確認できます。

●Railsをインストール
いよいよ、Railsをインストールします。

Railsのインストール時に「-v バージョン番号」とバージョンを指定してインストールできます。

今回はバージョン「6.0.3.4」をインストールします。

参考：railsの全バージョン履歴

次のコマンドを入力します。

console
gem install rails -v 6.0.3.4
コマンドを実行すると、インストールを開始します。インストールの完了までに数分かかることがあります。

Railsのバージョンを確認
Railsをインストールしたら、Railsのバージョンを確認するために次のコマンドを入力します。

console
rails -v
コマンドを実行すると、次の画面が表示されます。

console
rails -v
Rails 6.0.3.4
「Rails 6.0.3.4」と表示されました。

これで無事にRuby on Railsのインストールが完了しました。

●PostgreSQLをインストールする
本教材で使用するデータベースはPostgreSQLです。

※ SQLite3でも学習を進められます

PostgreSQLは無償で利用できるリレーショナルデータベースです。Homebrewを使って簡単にインストールができます。

インストールするには次のコマンドを入力します。

console
brew install postgresql
コマンドを実行すると、インストールされます。

実際にPostgreSQLがインストールされているかを確認するために、次のコマンドを入力します。

console
psql --version
コマンドを実行すると、次のように表示されます。

console
psql --version
psql (PostgreSQL) 11.2
「psql (PostgreSQL) 11.2」とバージョン情報が表示されたので、PostgreSQLのインストールが完了しました。

インストールが完了したら、PostgreSQLを起動します。以下のコマンドを実行してください。

console
brew services start postgresql
PostgreSQLを起動させる理由としては、Railsでローカルサーバーを立ち上げた際にPostgreSQLが起動していなかったらエラーが出るためです。

今回の目標は「ローカルサーバーを立ち上げて、Railsのデフォルトページを表示する」ことです。

ローカルにインストールされたRailsのバージョンを確認
新規Railsアプリケーションを作成
作成したディレクトリに移動
データベースを作成
ローカルサーバーを起動
Railsのデフォルトページを表示
それでは、実際にWebアプリケーションの作成を行いましょう。

1. ローカルにインストールされているRailsのバージョンの確認
新規Railsアプリケーションを作成する前に、ローカルにインストールされたRailsのバージョンを確認します。

ターミナル上で、次のコマンドを入力してください。

console
gem search ^rails$ -l
コマンドを実行すると、次のような結果が表示されます。

console
gem search ^rails$ -l

*** LOCAL GEMS ***

rails (6.0.3.4)
「Rails6.0.3.4」がインストールされていることがわかります。

表示されたバージョンを使って、Railsアプリケーションを作成します。

2. 新規Railsアプリケーションの作成
RailsでWebアプリケーションを新規作成します。

Webアプリケーションの新規作成では、rails newコマンドを入力します。

rails newコマンドでは命令文の最後に作成するアプリケーション名を指定します。

【例】

console
rails new 作成するアプリケーション名
今回はRails6.0.3.4を使って「techpit-match」という名前のアプリケーションを作成します。

次のコマンドを入力します。

console
rails _6.0.3.4_ new techpit-match --database=postgresql
命令文のrailsとnewの間にRailsのバージョンを入力すると、Railsのバージョンを指定できます（ここではローカルにある6.0.3.4を指定）。

また--database=で利用するデータベースを指定できます（ここではpostgresqlを指定）。

rails newコマンドで「techpit-match」というディレクトリ（フォルダ）が作成されました。

3. 作成したディレクトリに移動
cdコマンドを使って、新たに作成した「techpit-match」ディレクトリに移動します。

ちなみに「cd」は、change directory（ディレクトリを移動する）の略です。

ディレクトリ移動を行う命令文は、次の表現になります。

【例】

console
cd 移動したいディレクトリ名
今回は「techpit-match」ディレクトリに移動するため、次のコマンドを入力します。

console
cd techpit-match
コマンドを実行すると、「techpit-match」ディレクトリに移動します。

4. データベースを作成
「techpit-match」ディレクトリ内にローカルサーバーを立ち上げるために、データベースを作成します。

データベースを作成するには、次のコマンドを入力します。

console
rails db:create
コマンドを実行すると、次の実行結果が表示されます。

console
rails db:create
Created database 'techpit_match_development'
Created database 'techpit_match_test'
rails db:create コマンドを実行すると、config/database.ymlファイルを元にデータベースを作成します。

config/database.ymlファイルには、データベースに関する設定が記述されているファイルです。実際にファイルの中身を見てみましょう。

config/database.yml
# 中略
# Configure Using Gemfile
# gem 'pg'
#
default: &default
  adapter: postgresql
  encoding: unicode
  # For details on connection pooling, see Rails configuration guide
  # https://guides.rubyonrails.org/configuring.html#database-pooling
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

development:
  <<: *default
  database: techpit_match_development

  # 中略

# Warning: The database defined as "test" will be erased and
# re-generated from your development database when you run "rake".
# Do not set this db to the same as development or production.
test:
  <<: *default
  database: techpit_match_test

# As with config/credentials.yml, you never want to store sensitive information,
# like your database password, in your source code. If your source code is
# ever seen by anyone, they now have access to your database.
# 中略
以下のコードを見てください。

config/database.yml
development:
  <<: *default
  database: techpit_match_development

  # 中略

test:
  <<: *default
  database: techpit_match_test
developmentは開発用という意味で、testはテスト用という意味になります。

databaseはデータベース名を指定しています。今回でいうと開発用はtechpit_match_development、テスト用はtechpit_match_testという名前でデータベースを作成しています。

5. ローカルサーバーを起動
ローカルサーバーを立ち上げるには、次のコマンドを入力します。

console
rails server
コマンドを実行するとサーバーが起動します（rails sと省略することも可能）。

うまくサーバーが起動すると、ターミナルで次のように表示されます。

console
rails server
=> Booting Puma
=> Rails 6.0.3.2 application starting in development 
=> Run `rails server --help` for more startup options
Puma starting in single mode...
* Version 4.3.5 (ruby 2.7.1-p83), codename: Mysterious Traveller
* Min threads: 5, max threads: 5
* Environment: development
* Listening on tcp://127.0.0.1:3000
* Listening on tcp://[::1]:3000
Use Ctrl-C to stop
6. Railsのデフォルトページを表示
ローカルサーバーを起動したら、ブラウザで「http://localhost:3000/ 」にアクセスします。

次の画像のようにRailsのデフォルトページが表示されていれば、うまく動作しています。

image

以上で今回のパートは終了です。

お疲れさまでした。

本教材で使う画像をダウンロードします。以下のリンクから3つの画像をダウンロードしてください。

https://drive.google.com/drive/folders/1-FomnekKzTbaxCjGdYA6qtOR0vZZk2qg?usp=sharing

ダウンロード後、app/javascript/imagesディレクトリ内に画像を移動させてください。画像はドラッグ＆ドロップで移動できます。

※ app/javascriptディレクトリ内に imagesディレクトリはないため以下のコマンドを実行してから画像を移動してください

console
mkdir app/javascript/images
javascript/images/ディレクトリが以下のような構成になればOKです。

image

最後に、app/javascript/imagesディレクトリ内の画像を使用できるように設定します。

●config/webpacker.yml を次のように編集してください。

config/webpacker.yml
# 中略

  webpack_compile_output: true

  # Additional paths webpack should lookup modules
  # ['app/assets', 'engine/foo/app/assets']
  resolved_paths: []
  resolved_paths: ['app/javascript/images', 'app/assets/images']

  # Reload manifest.json on all requests so we reload latest compiled packs
  cache_manifest: false

  # Extract and emit a css file
  extract_css: false

# 中略

●今回のパートではBootstrapを導入していきます。
Bootstrapは有名なWebフレームワークで、CSSを細かく指定せずにサイトをある程度形にできます。レスポンシブにも対応してくれる便利なツールです。Bootstrapを導入するとWebアプリケーションを効率よく開発できます。

ゴールまでの流れ
Webpackerとは
BootstrapをWebpackerで導入
Bootstrapが導入されたか確認
それでは、Bootstrapの導入をおこないましょう。

1. Webpackerとは
今回Bootstrapを導入するにあたって、Webpackerを使って導入していきます。

Webpackerとは、複数のJavaScriptファイルなどを1つにまとめて出力するツールであるwebpackを簡単にRailsアプリケーションに統合できるgemです。

Rails5.1から標準でサポートされるようになりました。

webpackとはモジュールバンドラツールのことで、昨今のモダンなJavaScript開発で必須となりつつある仕組みです。

以下の画像はwebpackの公式サイトのイメージ図になります。

2. BootstrapをWebpackerで導入
Webpackerをインストールするには、まずGemfileに以下のコードを追加します。ただ先ほど説明した通り、Rails5.1以降標準でサポートされているため、デフォルトでGemが追加されています。

一応Gemfileを確認してみましょう。

techpit-match
└── Gemfile
gem 'webpacker', '~> 4.0'
なのでgemは追加する必要はありません。

Gemfileにwebpackerというgemがあることを確認できたらBootstrapを導入します。

yarn を使っている場合、パッケージをインストールするには、yarn addというコマンドを実行します。

【例】

console
yarn add project-name
参考：yarn add

それでは、以下のコマンドを実行してください。

console
yarn add jquery bootstrap popper.js
Bootstrapでは、いくつかのコンポーネントで jQuery, Popper.js といった JavaScript のプラグインが必要なため一緒にインストールします。

コマンドを実行すると、次のような結果が表示されます。
うまくいっていたら、package.json というファイルに以下のようなコードが追加されます。追加されたコードには導入したパッケージとそのパッケージのバージョンが記載されています。

次に導入したパッケージの設定のコードを追加します。config/webpack/environment.jsに以下のコードを追加してください。

config/webpack/environment.js
const { environment } = require('@rails/webpacker')

module.exports = environment

# ==========ここから追加する==========
const webpack = require('webpack')
environment.plugins.append(
  'Provide',
  new webpack.ProvidePlugin({
    $: 'jquery/src/jquery',
    jQuery: 'jquery/src/jquery',
    Popper: ['popper.js', 'default']
  })
)
# ==========ここまで追加する==========
上記のコードでimportやrequireなしで$やBootstrapのJavaScriptが使えるようになります。

Bootstrapのstyleをimport
次に、app/javascript/stylesheets/application.scssにBootstrapのstyleをimportする記述を追記します。

このapp/javascript/stylesheetsディレクトリ及び、app/javascript/stylesheets/application.scssファイルは存在しないので以下のコマンドで作成します。

console
mkdir app/javascript/stylesheets
touch app/javascript/stylesheets/application.scss
作成したら、application.scssファイルに以下のコードを追加してください。

app/javascript/stylesheets/application.scss
@import '~bootstrap/scss/bootstrap';
application.jsにコードを追加
yarnでインストールしたBootstrapのパッケージを利用できるようにimportします。

app/javascript/packs/application.js に以下のコードを追加してください。

app/javascript/packs/application.js
# ==========ここから追加する==========
import 'bootstrap';
import '../stylesheets/application';
# ==========ここまで追加する==========

// This file is automatically compiled by Webpack, along with any other files
// present in this directory. You're encouraged to place your actual application logic in
// a relevant structure within app/javascript and only use these pack files to reference
// that code so it'll be compiled.

require("@rails/ujs").start()
require("turbolinks").start()
require("@rails/activestorage").start()
require("channels")


// Uncomment to copy all static images under ../images to the output folder and reference
// them with the image_pack_tag helper in views (e.g <%= image_pack_tag 'rails.png' %>)
// or the `imagePath` JavaScript helper below.
//
// const images = require.context('../images', true)
// const imagePath = (name) => images(name, true)
レイアウトに stylesheet_pack_tag を追加
最後にレイアウトにstylesheet_pack_tagを追加します。stylesheet_pack_tagを使うことでWebpackで.cssや.scssファイルのスタイルシートにも対応します。

app/views/layouts/application.html.erbに以下のコードを追加してください。

app/views/layouts/application.html.erb
<!DOCTYPE html>
<html>
  <head>
    <title>TechpitMatch</title>
    <%= csrf_meta_tags %>
    <%= csp_meta_tag %>

    <%= stylesheet_link_tag 'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_pack_tag 'application', 'data-turbolinks-track': 'reload' %>

    <%# ここに追加 %>
    <%= stylesheet_pack_tag 'application', 'data-turbolinks-track': 'reload' %>

  </head>

  <body>
    <%= yield %>
  </body>
</html>
以上でBootstrapの導入は終了です。

3. Bootstrapが導入されたか確認
実際にBootstrapが機能するか確認します。

仮のボタンにBootstrapのクラスを当てます。

app/views/top/index.html.erbを以下のコードを追加してください。

app/views/top/index.html.erb
<p>このページはトップページです。</p>

<%# ここに追加 %>
<%= link_to "仮のボタンです", "#", class: "btn btn-primary" %>
コードを追加したら、http://localhost:3000 にアクセスしてください。青色のボタンが表示されていればうまく動作しています。

image

以上で今回のパートは終了です。

お疲れ様でした。
  
4-2
Deviseの導入
4章では、ユーザーの認証機能を実装していきます。ユーザーの認証機能を簡単に実装するために、Deviseというgemを導入します。

Deviseは、ユーザーのアカウント作成やログイン機能などの認証に必要な機能を簡単に実装できるRails用のgemです。

Deviseの公式ドキュメントはこちらです。

参考: Devise

本パートのゴール
本パートでは、下記の画像のようにデザインは何もない状態のアカウント作成・ログインページを表示するところまで実装します。

アカウント作成ページ

ログインページ

ゴールまでの流れ
Deviseのgemをインストール
Deviseのビューファイルをインストール
Userモデルを作成
Usersテーブルを作成
Deviseの導入の確認
Devise の導入は、基本的に公式ドキュメントに沿って実装していくので、導入方法を覚える必要はないです。

では、実際に進めていきましょう。

1. Deviseのgemをインストール
まず今回導入するDeviseの公式ドキュメントにアクセスしてください。

公式ドキュメント）Devise

アクセスしたら「Getting started」の箇所を見ましょう。

image

「Add the following line to your Gemfile」とあるので、まずGemfileに以下のコードを追加します。

techpit-match
└── Gemfile
gem 'devise'
Gemfileにデフォルトであったコメントアウトは不要なので削除して大丈夫です。

上記のgemを追加するとGemfileは以下のようになります。

source 'https://rubygems.org'
git_source(:github) { |repo| "https://github.com/#{repo}.git" }

ruby '2.7.2'

gem 'rails', '~> 6.0.3', '>= 6.0.3.4'
gem 'pg', '>= 0.18', '< 2.0'
gem 'puma', '~> 4.1'
gem 'sass-rails', '>= 6'
gem 'webpacker', '~> 4.0'
gem 'turbolinks', '~> 5'
gem 'jbuilder', '~> 2.7'
gem 'bootsnap', '>= 1.4.2', require: false

# ここに追加
gem 'devise'

group :development, :test do
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
end

group :development do
  gem 'web-console', '>= 3.3.0'
  gem 'listen', '~> 3.2'
  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'
end

group :test do
  gem 'capybara', '>= 2.15'
  gem 'selenium-webdriver'
  gem 'webdrivers'
end

gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
追加したgemを反映させるためにbundle installを実行します。

console
bundle install
次に「Next, you need to run the generator」と公式ドキュメントにあるように以下のコマンドを実行してください。

console
rails generate devise:install
上記コマンドを実行すると以下のファイルが作成されます。

create  config/initializers/devise.rb
create  config/locales/devise.en.yml
またファイルを作成すると、ターミナルに以下のようなメッセージが表示されます。

こちらはDeviseを使う上での初期設定になるので、1から順に見て行きましょう。

console
rails generate devise:install
Running via Spring preloader in process 16776
      create  config/initializers/devise.rb
      create  config/locales/devise.en.yml
===============================================================================

Depending on your application's configuration some manual setup may be required:

  1. Ensure you have defined default url options in your environments files. Here
     is an example of default_url_options appropriate for a development environment
     in config/environments/development.rb:

       config.action_mailer.default_url_options = { host: 'localhost', port: 3000 }

     In production, :host should be set to the actual host of your application.

     * Required for all applications. *

  2. Ensure you have defined root_url to *something* in your config/routes.rb.
     For example:

       root to: "home#index"
     
     * Not required for API-only Applications *

  3. Ensure you have flash messages in app/views/layouts/application.html.erb.
     For example:

       <p class="notice"><%= notice %></p>
       <p class="alert"><%= alert %></p>

     * Not required for API-only Applications *

  4. You can copy Devise views (for customization) to your app by running:

       rails g devise:views
       
     * Not required *

===============================================================================
1はメール送信の設定で本教材ではメール送信の実装は行わないので、1は飛ばします。

2も既にrootルーティングを3章で実装しているので、2も飛ばして大丈夫です。

3はフラッシュメッセージに関してですが、本教材ではフラッシュメッセージは実装しないので、3も飛ばします。

本教材では、4を進めていきます。

2. Deviseのビューファイルをインストール
先ほどの4のメッセージには、以下のように書かれていました。

4. You can copy Devise views (for customization) to your app by running:

       rails g devise:views
直訳すると、「次のコマンドを実行すると、Deviseのビューをアプリケーションにコピーできます」という意味になります。なのでコマンドを実行して、Deviseのビューファイルを作成しましょう。

rails g devise:views
実行すると以下のような結果が表示されます。

rails g devise:views
Running via Spring preloader in process 17438
      invoke  Devise::Generators::SharedViewsGenerator
      create    app/views/devise/shared
      create    app/views/devise/shared/_error_messages.html.erb
      create    app/views/devise/shared/_links.html.erb
      invoke  form_for
      create    app/views/devise/confirmations
      create    app/views/devise/confirmations/new.html.erb
      create    app/views/devise/passwords
      create    app/views/devise/passwords/edit.html.erb
      create    app/views/devise/passwords/new.html.erb
      create    app/views/devise/registrations
      create    app/views/devise/registrations/edit.html.erb
      create    app/views/devise/registrations/new.html.erb
      create    app/views/devise/sessions
      create    app/views/devise/sessions/new.html.erb
      create    app/views/devise/unlocks
      create    app/views/devise/unlocks/new.html.erb
      invoke  erb
      create    app/views/devise/mailer
      create    app/views/devise/mailer/confirmation_instructions.html.erb
      create    app/views/devise/mailer/email_changed.html.erb
      create    app/views/devise/mailer/password_change.html.erb
      create    app/views/devise/mailer/reset_password_instructions.html.erb
      create    app/views/devise/mailer/unlock_instructions.html.erb
実行結果から、様々なhtml.erbファイルが作成されていることがわかります。

3. Userモデルを作成
モデルとはMVCで言うところのMにあたり、データベースへのアクセスをはじめ、情報のやり取りを行うシステムの階層です。

以下のコマンドでDevise用のUserモデルを作成します。モデル名の値は任意です。作成したいモデル名で作成できます。今回はUserというモデル名で作成します。

console
rails g devise User
上記のコマンドを実行すると以下のような結果が表示されます。

console
rails g devise User
Running via Spring preloader in process 18101
      invoke  active_record
      create    db/migrate/20201117072443_devise_create_users.rb
      create    app/models/user.rb
      invoke    test_unit
      create      test/models/user_test.rb
      create      test/fixtures/users.yml
      insert    app/models/user.rb
       route  devise_for :users
最後の行にroute devise_for :usersという記載があります。これはconfig/routes.rbにDeviseのルーティングを追加しています。

実際にconfig/routes.rbを確認してみましょう。

config/routes.rb
Rails.application.routes.draw do
  devise_for :users
  root 'top#index'
end
devise_for :usersという記述がDeviseのルーティングになります。この1行のコードがサインアップやサインインなどのルーティングを設定しています。

4. Usersテーブルを作成
先ほどUserモデルを作成した際に、db/migrate/ディレクトリの中にマイグレーションファイルが作成されました。

image

マイグレーションファイルとは、テーブルの設計図です。設計図のままだと特に何かを作成することはないので、設計図をもとにテーブルを作成する必要があります。

Railsだとマイグレーションファイルを実行することで、設計図を元にテーブルを作成したり、カラムを追加したりできます。

マイグレーションファイルを実行するには以下のコマンドで実行できます。

console
rails db:migrate
上記のコマンドを実行すると以下のような結果が表示されます。

console
rails db:migrate
== 20201117072443 DeviseCreateUsers: migrating ================================
-- create_table(:users)
   -> 0.0159s
-- add_index(:users, :email, {:unique=>true})
   -> 0.0107s
-- add_index(:users, :reset_password_token, {:unique=>true})
   -> 0.0031s
== 20201117072443 DeviseCreateUsers: migrated (0.0299s) =======================
5. Deviseの導入の確認
gemを新しく追加しているので、サーバーを再起動させます。まず以前立ち上げていたサーバーを終了させます。終了させるにはcontrol + Cを同時に押せば大丈夫です。

その後「rails s」コマンドでローカルサーバーを立ち上げます。

そして、http://localhost:3000/users/sign_up を開くと以下の画面のようにアカウント作成ページが表示されていれば問題ありません。


また http://localhost:3000/users/sign_in にアクセスすると以下のようなページが表示されます。


以上で本パートは終了です。

お疲れさまでした。
         
5-5
Font Awesome の導入
今回のパートではFont Awesomeを導入していきます。

Font Awesomeを導入することで、Web上でよく利用されるアイコンをアイコンフォントという文字として使えます。

本パートのゴール
本パートでは、プロフィールページにアイコンを表示させます。

image

ゴールまでの流れ
Font Awesome の導入
Font Awesome が導入されたか確認
では、実際に進めてみましょう。

1. Font Awesome の導入
それでは、Font Awesome を導入していきます。Bootstrapと同様yarnを使って導入します。以下のコマンドを実行してください。

console
yarn add @fortawesome/fontawesome-free
コマンドを実行すると、次のような結果が表示されます。

console
yarn add @fortawesome/fontawesome-free
yarn add v1.22.10
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning " > webpack-dev-server@3.11.0" has unmet peer dependency "webpack@^4.0.0 || ^5.0.0".
warning "webpack-dev-server > webpack-dev-middleware@3.7.2" has unmet peer dependency "webpack@^4.0.0".
[4/4] 🔨  Building fresh packages...
success Saved lockfile.
success Saved 1 new dependency.
info Direct dependencies
└─ @fortawesome/fontawesome-free@5.15.1
info All dependencies
└─ @fortawesome/fontawesome-free@5.15.1
✨  Done in 4.33s.
package.jsonファイルには以下のコードが追加されます。

package.json
{
  "name": "techpit_match",
  "private": true,
  "dependencies": {
    "@fortawesome/fontawesome-free": "^5.15.1",
    "@rails/actioncable": "^6.0.0",
    "@rails/activestorage": "^6.0.0",
    "@rails/ujs": "^6.0.0",
次に、app/javascript/stylesheets/application.scssにFont Awesome のCSSを読み込みます。

app/javascript/stylesheets/application.scss
@import '~bootstrap/scss/bootstrap';

/* ここに追加 */
@import '~@fortawesome/fontawesome-free/scss/fontawesome';

@import "top";

@import "users/sign_up";
@import "users/sign_in";
次にyarnでインストールした Font Awesome のパッケージを利用できるようにimportします。

app/javascript/packs/application.jsに以下のコードを追加してください。

app/javascript/packs/application.js
import 'bootstrap';
import '../stylesheets/application';
// ここに追加
import '@fortawesome/fontawesome-free/js/all';

// 中略
以上でFont Awesomeの導入は終了です。

2. Font Awesome が導入されたか確認
Font Awesomeが機能するか確認します。

以下のリンクにアクセスしてください。

Font Awesome - fire

すると下記の画像のような画面が表示されます。

image

次に上記の画像の矢印で示しているコードをコピペします。

<i class="fas fa-fire"></i>
このコードがfireというアイコンを表すコードになります。users/show.html.erbに追加してみましょう。

app/views/users/show.html.erb
<p>このページはプロフィールページです。</p>

<%# ここに追加 %>
<i class="fas fa-fire"></i>
上記のコードを追加したら、http://localhost:3000/users/id にアクセスしてください。

id は users テーブルに登録されているidにしてください

image

上記の画像のように黒い小さい炎が表示されていればうまく動作しています。

以上で今回のパートは終了です。

お疲れさまでした。

6-4
プロフィール情報を編集できるようにする
「4-6 追加したカラムを保存できるようにする」で説明した通り、Deviseでは、デフォルトでメールアドレスとパスワードはパラメータを受け取るようにストロングパラメータが設定されています。

つまり、デフォルトではメールアドレスとパスワードしか編集することはできません。

なので、4-6 で実装したようにconfigure_permitted_parametersメソッド内で編集できるカラムを指定します。

それでは、コードを追加していきましょう。app/controllers/application_controller.rb に以下のコードを追加してください。

app/controllers/application_controller.rb
class ApplicationController < ActionController::Base
  before_action :configure_permitted_parameters, if: :devise_controller?

  protected

  def configure_permitted_parameters
    devise_parameter_sanitizer.permit(:sign_up, keys: [:name, :gender])

    # この行を追加
    devise_parameter_sanitizer.permit(:account_update, keys: [:name, :self_introduction])

  end
end
アカウント作成時と違う箇所は、キーがaccount_updateになっているところです。このキーに関しては、Deviseの公式ドキュメントに記載されています。

参考）Devise - Strong Parameters

追加したコードで、nameカラムとself_introductionカラムを編集できるようにしています。

以上で本パートは終了です。

お疲れさまでした。
                                                    
7-4
CarrierWave と MiniMagick の導入
このパートでは画像アップロードをするために、CarrierWave と MiniMagick の導入をおこないます。

本パートのゴール
本パートでは、CarrierWave と MiniMagick の導入をおこないます。

ゴールまでの流れ
CarrierWave の導入
MiniMagick の導入
アップローダーファイルの修正
では、進めていきましょう。

1. CarrierWave の導入
CarrierWave は、Ruby on Rails のWebアプリケーションで簡単にファイルアップロードするための機能を提供してくれるライブラリです。

参考）CarrierWave

CarrierWave の Gem をインストール
それでは、CarrierWave をインストールします。以下のコードをGemfile に追加してください。

# 中略

gem 'jbuilder', '~> 2.7'
gem 'bootsnap', '>= 1.4.2', require: false

gem 'devise'

# ここに追加
gem 'carrierwave', '~> 2.0'

group :development, :test do
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
end

# 中略
コードを追加したらgemを反映させるためにbundle installを実行します。

console
bundle install
アップローダーを生成
次に、アップローダーを生成します。

以下のコマンドを実行してください。

console
rails g uploader ProfileImage
上記のコマンドを実行すると、以下のファイルが作成されます。

app/uploaders/profile_image_uploader.rb
次にモデルファイル(Userモデル)にアップローダーをマウントします。app/models/user.rbに以下のコードを追加してください。

app/models/user.rb
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable
  
  validates :name, presence: true
  validates :self_introduction, length: { maximum: 500 }

  enum gender: { 男性: 0, 女性: 1 }

  # ここに追加
  mount_uploader :profile_image, ProfileImageUploader

  def update_without_current_password(params, *options)

    if params[:password].blank? && params[:password_confirmation].blank?
      params.delete(:password)
      params.delete(:password_confirmation)
    end

    result = update_attributes(params, *options)
    clean_up_passwords
    result
  end
end
ProfileImageUploaderは先ほど生成したprofile_image_uploader.rbファイルにあるクラス名になります。

2. MiniMagick の導入
MiniMagick は画像加工をしてくれるgemです。MiniMagick を使用するためにはImageMagickという画像処理ライブラリを導入する必要があります。

参考）MiniMagick

なので、まずお使いのPCにImageMagickがインストールされているか確認します。以下のコマンドを実行してください。

console
convert -version
以下のようにVersion: ImagiMagick ~と表示されていれば、お使いのPCにはImageMagickは入っているので、そのまま MiniMagick のインストールに進んでください。

console
convert -version
Version: ImageMagick 7.0.10-35 Q16 x86_64 2020-11-01 https://imagemagick.org
Copyright: © 1999-2020 ImageMagick Studio LLC
License: https://imagemagick.org/script/license.php
Features: Cipher DPC HDRI Modules OpenMP(4.5) 
Delegates (built-in): bzlib freetype gslib heic jng jp2 jpeg lcms lqr ltdl lzma openexr png ps tiff webp xml zlib
上記のように Version が表示されなければ、ImageMagick をインストールしていきます。

以下のコマンドを実行してください。

console
brew install imagemagick
MiniMagick のGemをインストール
次にMiniMagick をインストールします。以下のコードをGemfileに追加してください。

# 中略

gem 'bootsnap', '>= 1.4.2', require: false

gem 'devise'
gem 'carrierwave', '~> 2.0'

# ここに追加
gem "mini_magick"

group :development, :test do
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
end

# 中略
コードを追加したらgemを反映させるためにbundle installを実行します。

console
bundle install
3. アップローダーファイルの修正
次にapp/uploaders/profile_image_uploader.rbを修正します。

修正するのは、以下の2点です。

4行目のコメントアウトを外す
extension_whitelist メソッドのコメントアウトを外す
app/uploaders/profile_image_uploader.rb
class ProfileImageUploader < CarrierWave::Uploader::Base
  # Include RMagick or MiniMagick support:
  # include CarrierWave::RMagick
  include CarrierWave::MiniMagick # コメントアウトを外す

  # Choose what kind of storage to use for this uploader:
  storage :file
  # storage :fog

  # Override the directory where uploaded files will be stored.
  # This is a sensible default for uploaders that are meant to be mounted:
  def store_dir
    "uploads/#{model.class.to_s.underscore}/#{mounted_as}/#{model.id}"
  end

  # Provide a default URL as a default if there hasn't been a file uploaded:
  # def default_url(*args)
  #   # For Rails 3.1+ asset pipeline compatibility:
  #   # ActionController::Base.helpers.asset_path("fallback/" + [version_name, "default.png"].compact.join('_'))
  #
  #   "/images/fallback/" + [version_name, "default.png"].compact.join('_')
  # end

  # Process files as they are uploaded:
  # process scale: [200, 300]
  #
  # def scale(width, height)
  #   # do something
  # end

  # Create different versions of your uploaded files:
  # version :thumb do
  #   process resize_to_fit: [50, 50]
  # end

  # Add a white list of extensions which are allowed to be uploaded.
  # For images you might use something like this:

  # コメントアウトを外す
  def extension_whitelist
    %w(jpg jpeg gif png)
  end

  # Override the filename of the uploaded files:
  # Avoid using model.id or version_name here, see uploader/store.rb for details.
  # def filename
  #   "something.jpg" if original_filename
  # end
end
rb
include CarrierWave::MiniMagick
上記のコードで、MiniMagickを使えるようにしています。

rb
def extension_whitelist
  %w(jpg jpeg gif png)
end
このコードでアップロードできる拡張子を制限しています。

以上で、本パートは終了です。

お疲れさまでした。
  
8-8
Hammer.js の導入
今回のパートではHammer.jsを導入していきます。

Hammer.js はJavaScriptのライブラリで、タッチジェスチャーを実装したいときに利用したいときに使用します。

参考: Hummer.js

本教材では、Hammer.jsを使ってスワイプ機能を実装します。

本パートのゴール
本パートでは、Hammer.jsを導入します。

ゴールまでの流れ
Hammer.js の導入
application.js にコードを追加
それでは、Hammer.jsの導入をおこないましょう。

1. Hammer.js の導入
Bootstrap や Font Awesome と同様yarnを使って導入します。以下のコマンドを実行してください。

console
yarn add hammerjs
コマンドを実行すると、次のような結果が表示されます。

console
yarn add v1.22.10
[1/4] 🔍  Resolving packages...
[2/4] 🚚  Fetching packages...
[3/4] 🔗  Linking dependencies...
warning " > webpack-dev-server@3.11.0" has unmet peer dependency "webpack@^4.0.0 || ^5.0.0".
warning "webpack-dev-server > webpack-dev-middleware@3.7.2" has unmet peer dependency "webpack@^4.0.0".
[4/4] 🔨  Building fresh packages...
success Saved lockfile.
success Saved 1 new dependency.
info Direct dependencies
└─ hammerjs@2.0.8
info All dependencies
└─ hammerjs@2.0.8
✨  Done in 2.72s.
package.jsonファイルには以下のコードが追加されます。

package.json
    "@rails/ujs": "^6.0.0",
    "@rails/webpacker": "4.3.0",
    "bootstrap": "^4.5.3",
+   "hammerjs": "^2.0.8",
    "jquery": "^3.5.1",
    "popper.js": "^1.16.1",
    "turbolinks": "^5.2.0"
2. application.js にコードを追加
yarnでインストールしたHammer.jsのパッケージを利用できるようにimportします。

app/javascript/packs/application.js に以下のコードを追加してください。

app/javascript/packs/application.js
import 'bootstrap';

// ここに追加
import 'hammerjs';

import '../stylesheets/application';
import '@fortawesome/fontawesome-free/js/all';

// 中略
以上で今回のパートは終了です。

お疲れさまでした。
  
12-6
Action Cable を使ったチャット機能の実装
本パートでは、リアルタイムでメッセージを送るために Action Cable を使った実装をおこないます。

本パートのゴール
本パートでは、チャットルームページのフォーム内でテキストを入力しEnterを押すと、入力した内容をアラートで表示するところまで実装します。

image

ゴールまでの流れ
Action Cable とは
ChatRoomチャネルの作成
chat_room_channel.rb の実装
chat_room_channel.js の実装
では進めていきましょう。

1. Action Cable とは
Action Cable とは、WebSocketとRailsのその他の部分をシームレスに統合するためのものです。Action Cable が Rails5 から導入されたことで、Rails アプリケーションの効率の良さとスケーラビリティを損なわずに、通常の Rails アプリケーションと同じスタイル・方法でリアルタイム機能をRubyで記述できます。

参考: Action Cable の概要

WebSocket とは、ユーザーのブラウザとサーバー間を常時接続状態にして双方向通信ができる技術です。

参考: WebSocket

2. ChatRoomチャネルの作成
それでは、Action Cableの設定をおこなっていきます。

Action Cable では、チャネル(Channel) というものを作成します。チャネルには論理的な処理を記載します。MVCのコントローラーが果たす役割と似ています。

それでは、以下のコマンドを実行して、ChatRoomチャネルを作成しましょう。

console
rails g channel chat_room speak
実行結果は以下になります。

console
rails g channel chat_room speak
Running via Spring preloader in process 28144
      invoke  test_unit
      create    test/channels/chat_room_channel_test.rb
      create  app/channels/chat_room_channel.rb
   identical  app/javascript/channels/index.js
   identical  app/javascript/channels/consumer.js
      create  app/javascript/channels/chat_room_channel.js
作成された、chat_room_channel.rbとchat_room_channel.jsの中身は以下のようになっています。

app/channels/chat_room_channel.rb
class ChatRoomChannel < ApplicationCable::Channel
  def subscribed
    # stream_from "some_channel"
  end

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end

  def speak
  end
end
app/javascript/channels/chat_room_channel.js
import consumer from "./consumer"

consumer.subscriptions.create("ChatRoomChannel", {
  connected() {
    // Called when the subscription is ready for use on the server
  },

  disconnected() {
    // Called when the subscription has been terminated by the server
  },

  received(data) {
    // Called when there's incoming data on the websocket for this channel
  },

  speak: function() {
    return this.perform('speak');
  }
});
3. chat_room_channel.rb の実装
次に、サーバーサイドの処理をするapp/channels/chat_room_channel.rbの実装をします。

app/channels/chat_room_channel.rb を以下のように編集してください。

app/channels/chat_room_channel.rb
class ChatRoomChannel < ApplicationCable::Channel
  def subscribed
    # この行を編集する
    stream_from "chat_room_channel"
  end

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end

  # ==========ここから編集する==========
  def speak(data)
    ActionCable.server.broadcast 'chat_room_channel', chat_message: data['chat_message']
  end
  # ==========ここまで編集する==========
end
rb
def subscribed
  stream_from "chat_room_channel"
end
subscribedでどのchannel(今回はchat_room_channel)を購読するか指定します。このコードで、chat_room_channel.rbとchat_room_channel.jsでデータ送受信できます。

rb
def speak(data)
  ActionCable.server.broadcast 'chat_room_channel', chat_message: data['chat_message']
end
上記のコードで、chat_room_channel.jsで実行されたspeakアクションのchat_messageを受け取り、chat_room_channel.jsのreceivedメソッドにdataを送信します。

4. chat_room_channel.js の実装
次に、クライアントサイドの処理をするapp/javascripts/channels/room_channel.jsを実装します。

最初は、フォームに文字を入力してエンターを押したら、アラートを表示するところまで実装します。

app/javascripts/channels/room_channel.js
import consumer from "./consumer"

// この行を編集する
const appChatRoom = consumer.subscriptions.create("ChatRoomChannel", {
  connected() {
    // Called when the subscription is ready for use on the server
  },

  disconnected() {
    // Called when the subscription has been terminated by the server
  },

  received(data) {
    // この行を編集する
    return alert(data['chat_message']);
  },

  // ==========ここから編集する==========
  speak: function(chat_message) {
    return this.perform('speak', { chat_message: chat_message });
  }
  // ==========ここまで編集する==========
});

// ==========ここから追加する==========
if(/chat_rooms/.test(location.pathname)) {
  $(document).on("keydown", ".chat-room__message-form_textarea", function(e) {
    if (e.key === "Enter") {
      appChatRoom.speak(e.target.value);
      e.target.value = '';
      e.preventDefault();
    }
  })
}
// ==========ここまで追加する==========
js
if(/chat_rooms/.test(location.pathname)) {
上記のコードでチャットルームページかどうかを確かめています。チャットルームページだけで上記の処理をしたいためです。

location.pathname で現在のページURLのパスを参照します。http://localhost:3000/chat_rooms/1 にアクセスしたら、/chat_rooms/1を取得します。

.test()メソッドは、正規表現で指定された文字列の一致を調べるための検索を実行します。正であればtrueを返します。

参考: MDN web docs - RegExp.prototype.test()

js
$(document).on("keydown", ".chat-room__message-form_textarea", function(e) {
  if (e.key === "Enter") {
上記のコードで、フォーム内でEnterキーを押したときに処理を実行します。

js
appChatRoom.speak(e.target.value);
上記のコードで、speakアクションを発火させています。

js
speak: function(chat_message) {
  return this.perform('speak', { chat_message: chat_message });
}
上記のコードで、chat_room_channel.rbのspeakアクションにchat_messageを送っています。

js
received(data) {
  return alert(data['chat_message']);
},
上記のコードで、chat_room_channel.rbから送られてきたdataを受け取り、アラートを表示します。

それでは、動作確認をしてみましょう。

チャットルームページにアクセスして、フォームにテキストを入力し、Enterキーを押してください。

image

上記の動画のように入力したテキストがアラートに表示されればうまく動作しています。

アラート表示までの流れ
ここまでのアラート表示までの流れは以下になります。

チャットルームページのフォーム内でEnterキーを押す
chat_room_channel.js の appChatRoom の speak アクションが発火
入力したテキスト(chat_message)を chat_room_channel.rb の speak アクションに送る
chat_room_channel.rb の speak アクションでは、送られたchat_messageを受け取り、chat_room_channel.js の received に data を送る
データを受け取ったreceivedでは、受け取ったデータをアラートで表示
以上で本パートは終了です。

次のパートでも引き続き Action Cable の実装を進めていきます。

お疲れさまでした。
  
12-7
Action Cable を使ったチャット機能の実装 2
本パートでは、引き続き Action Cable を使ったチャット機能の実装を進めていきます。

本パートのゴール
本パートでは、入力したテキストをchat_messagesテーブルに保存し、チャットルームページに表示するところまで実装します。


ゴールまでの流れ
chat_room_id を chat_room_channel.rb の speak アクションに送る
送られてきたチャットメッセージの情報を保存する
保存後の処理を追加
ブロードキャストの処理の追加
ブラウザ内の表示を書き換える
では進めていきましょう。

1. chat_room_id を chat_room_channel.rb の speak アクションに送る
チャットルームページで入力したテキストをデータベースに保存するには、どのチャットルームページで行なわれたテキストなのかchat_room_idが必要です。

なので、chat_room_idをchat_room_channel.rb の speak アクションに送るようにします。

app/javascripts/channels/chat_room_channel.js を以下のように編集してください。

app/javascripts/channels/chat_room_channel.js
  // 中略

  // ==========ここから編集==========
  speak: function(chat_message, chat_room_id) {
    return this.perform('speak', { chat_message: chat_message, chat_room_id: chat_room_id });
  }
  // ==========ここまで編集==========
});

if(/chat_rooms/.test(location.pathname)) {
  $(document).on("keydown", ".chat-room__message-form_textarea", function(e) {
    if (e.key === "Enter") {
      // この行を追加
      const chat_room_id = $('textarea').data('chat_room_id')
      // この行を編集
      appChatRoom.speak(e.target.value, chat_room_id);
      e.target.value = '';
      e.preventDefault();
    }
  })
}
js
const chat_room_id = $('textarea').data('chat_room_id')
appChatRoom.speak(e.target.value, chat_room_id);
上記のコードでchat_room_idを取得し、appChatRoomのspeakアクションにchat_room_idを引数として渡しています。

js
speak: function(chat_message, chat_room_id) {
    return this.perform('speak', { chat_message: chat_message, chat_room_id: chat_room_id });
  }
上記のコードで、chat_room_idをchat_room_channel.rb の speak アクションに送っています。

2. 送られてきたチャットメッセージの情報を保存する
次に、chat_room_channel.rb の speak アクションで送られてきたチャットメッセージの情報をchat_messagesテーブルに保存します。

app/channels/chat_room_channel.rb を以下のように編集してください。

app/channels/chat_room_channel.rb
  # 省略

  def unsubscribed
    # Any cleanup needed when channel is unsubscribed
  end

  def speak(data)
    # ==========ここから編集する==========
    ChatMessage.create!(
      content: data['chat_message'],
      user_id: current_user.id,
      chat_room_id: data['chat_room_id']
    )
    # ==========ここまで編集する==========
  end
end
content及びchat_room_idは、chat_room_channel.jsのspeakアクションから送られてきたデータを保存します。

また誰がチャットメッセージを送信したかのuser_idが必要なためログインしているユーザー(current_user)のidを保存します。

chat_room_channel.rb で current_user を取得
先ほど、current_userを使いましたが、chat_room_channel.rb ではcurrent_userを使うことはできません。そのため、app/channels/application_cable/connection.rbでcurrent_userを使うためのコードを書く必要があります。

app/channels/application_cable/connection.rbを以下のように編集してください。

app/channels/application_cable/connection.rb
module ApplicationCable
  class Connection < ActionCable::Connection::Base
    identified_by :current_user

    def connect
      reject_unauthorized_connection unless find_verified_user
    end

    private

      def find_verified_user
        self.current_user = env['warden'].user
      end
  end
end
identified_byはコネクション(クライアントとサーバー間の関係を成立させる基礎)を識別するキーです。

rb
env['warden'].user
上記のコードで、ログインしているユーザーの情報を取得できます。

rb
reject_unauthorized_connection
上記のコードは、WebSocket接続が開いている場合は閉じ、404を返します。

参考: ActionCable :: Connection :: Authorization

3. 保存後の処理を追加
次にchat_messagesテーブルにデータを保存した後の処理を書きます。

データを保存した後に処理を書きたい場合、モデルにafter_create_commit等を使います。

参考: Active Record コールバック - 10 トランザクションコールバック

それでは、app/models/chat_message.rbに以下のコードを追加してください。

app/models/chat_message.rb
class ChatMessage < ApplicationRecord
  belongs_to :user
  belongs_to :chat_room

  # この行を追加
  after_create_commit { ChatMessageBroadcastJob.perform_later self }
end
rb
after_create_commit { ChatMessageBroadcastJob.perform_later self }
上記のコードで、データを保存後にChatMeesageBroadcastJobを実行するようにしています。

4. ブロードキャストの処理の追加
先ほど、speakメソッドのブロードキャストの処理を削除したため、ブロードキャストの処理を追加します。

先ほど削除したコードはこちらです。

app/channels/chat_room_channel.rb
ActionCable.server.broadcast 'chat_room_channel', chat_message: data['chat_message']
ブロードキャストをすることで、他のクライアントからデータを見ることができます。

それでは、以下のコマンドでChatMessageBroadcastJobを作成します。

console
rails g job ChatMessageBroadcastJob
実行結果は以下になります。

console
rails g job ChatMessageBroadcastJob
Running via Spring preloader in process 38489
      invoke  test_unit
      create    test/jobs/chat_message_broadcast_job_test.rb
      create  app/jobs/chat_message_broadcast_job.rb
作成した、app/jobs/chat_message_broadcast_job.rb を以下のように編集してください。

app/jobs/chat_message_broadcast_job.rb
class ChatMessageBroadcastJob < ApplicationJob
  queue_as :default

  def perform(chat_message)
    ActionCable.server.broadcast 'chat_room_channel', chat_message: render_chat_message(chat_message)
  end

  private

    def render_chat_message(chat_message)
      ApplicationController.renderer.render(partial: 'chat_messages/chat_message', locals: { chat_message: chat_message, current_user: chat_message.user })
    end
end
rb
def perform(chat_message)
  ActionCable.server.broadcast 'chat_room_channel', chat_message: render_chat_message(chat_message)
end
上記のコードでブロードキャストの処理をしています。また、render_chat_message(chat_message)でrender_chat_messageメソッドを呼び出しています。

rb
def render_chat_message(chat_message)
  ApplicationController.renderer.render(partial: 'chat_messages/chat_message', locals: { chat_message: chat_message, current_user: chat_message.user })
end
ApplicationController.rendererでコントローラーの制約を受けずに、任意のビューテンプレートをレンダリングします。今回は、chat_messages/_chat_message.html.erbを呼び出しています。

localsオプションで、部分テンプレートで使える変数を定義しています。

5. ブラウザ内の表示を書き換える
最後に、chat_room_channel.jsのreceivedを書き換えて、アラートではなくブラウザ内の表示を書き換えます。

chat_room_channel.jsを以下のように編集してください。

app/javascripts/channels/room_channel.js
  // 中略

  disconnected() {
    // Called when the subscription has been terminated by the server
  },

  received(data) {
    // =========ここから編集==========
    const chatMessages = document.getElementById('chat-messages');
    chatMessages.insertAdjacentHTML('beforeend', data['chat_message']);
    // =========ここまで編集==========
  },

  speak: function(chat_message, chat_room_id) {
    return this.perform('speak', { chat_message: chat_message, chat_room_id: chat_room_id });
  }
});

// 中略
document.getElementById('chat-messages');でid="chat-messages"の要素のオブジェクトを返します。

参考: MDN web docs - Document.getElementById()

id="chat-messages"の要素は、app/views/chat_rooms/show.html.erbにあります。

app/views/chat_rooms/show.html.erb
<div id='chat-messages'>
  <%= render @chat_messages %>
</div>
js
chatMessages.insertAdjacentHTML('beforeend', data['chat_message']);
insertAdjacentHTML で第2引数のdata['chat_message']を挿入します。挿入位置は、'beforeend'なので、element 内部の、最後の子要素の後に挿入します。

参考: MDN web docs - element.insertAdjacentHTML

以上でチャット機能の実装は完了です。チャットルームページで動作確認をしましょう。


上記のように入力したテキストがチャットルームページに表示されればうまく動作しています。

チャットメッセージが表示するまでの流れ
ここまでのチャットメッセージを表示するまでの流れは以下になります。

チャットルームページのフォーム内でEnterを押す
chat_room_channel.js の appChatRoom の speak アクションが発火
入力したテキスト(chat_message)を chat_room_channel.rb の speak アクションに送る
chat_room_channel.rb の speak アクションでは、送られたchat_messageを受け取り、chat_messages テーブルに保存。ChatMeesageBroadcastJobを呼ぶ。
chat_message_broadcast_job.rb で部分テンプレートchat_messages/_chat_message.html.erbを呼び出す。
chat_room_channel.jsのreceivedを呼び出し、ブラウザ内にテキストを表示
以上で本パートは終了です。

お疲れさまでした。
         
