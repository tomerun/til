# bundlerを使う

## bundlerとは

プロジェクトで使用するgemの名前やバージョンを指定する仕組み。

`Gemfile` という名前のファイルにgemの名前やバージョンを書いておくと、 `bundle` コマンドを使ってインストールできる。

## 使い方

```
$ gem install bunlder   # bundlerをインストール
$ bundle init           # Gemfileのひな形を生成
Writing new Gemfile to /path/to/project/dir/Gemfile
$ cat Gemfile
# frozen_string_literal: true
source "https://rubygems.org"

# gem "rails"

## ...
## Gemfile を編集する
## ...

$ bundle install        # Gemfileに書いたgemをインストールする。
                        # 初回はGemfile.lockというファイルが生成され、実際にインストールしたバージョンが書かれる
$ bundle update         # gemのアップデート

# ...
# 自作プログラム app.rb を作成
# ...

$ bundle exec ruby app.rb  # bundlerで指定したgemを使ってapp.rbを実行
```

rubyスクリプト内では、次のようにしてrequireする
```ruby
require 'bundler/setup'   # gemのサーチパスを指定
Bundler.require           # 一括してrequire（個別にrequireしてもよい）
```

## Gemfileの記法

公式ドキュメントは次を参照
* http://bundler.io/gemfile.html
* http://bundler.io/man/gemfile.5.html

### バージョン指定

```ruby
gem "nokogiri"                           # バージョン任意
gem "RedCloth", ">= 4.1.0", "< 4.2.0"    # バージョン範囲を指定
gem 'thin', '~>1.1'                      # マイナーバージョンまでを固定（>=1.1, <1.2 と同じ意味になる）
```

### グループ指定

```ruby
gem "rspec", :group => :test             # gemごとに指定

group :test do                           # グループで指定
  gem 'faker'
  gem 'rspec'
end

group :test, :development do
  gem 'capybara'
  gem 'rspec-rails'
end
```
こうしておくと、Rubyスクリプト内で次のようにすることでrequireするライブラリを切り替えられる
```ruby
Bundler.require                  # defaults to the _default_ group
Bundler.require(:default)        # identical
Bundler.require(:default, :test) # requires the _default_ and _test_ groups
Bundler.require(:test)           # requires the _test_ group
```

特定のグループのgemを外してインストールしたい場合は次のようにする
```
$ bundle install --without test development
```


