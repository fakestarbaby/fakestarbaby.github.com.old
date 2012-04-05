---
layout: post
title: "rails_configで環境毎に定数を管理しよう！"
date: 2012-01-12 20:42
comments: true
categories: [rails, plugins]
---

## rails_config

定数を開発環境毎にYAMLファイルで管理出来るプラグイン。

<!-- more -->

### 公式リポジトリ
[https://github.com/railsjedi/rails_config](https://github.com/railsjedi/rails_config)

### The Ruby Toolbox
[https://www.ruby-toolbox.com/projects/rails_config](https://www.ruby-toolbox.com/projects/rails_config)

***

### Railsで試してみよう！

Gemfileにrails_configを記述する。

```ruby Gemfile
gem 'rails_config'
```

コンソールでコマンドを実行すると、必要となるYAMLファイル一式が自動生成される。

```bash
$ bundle install
$ rails g rails_config:install
    create  config/initializers/rails_config.rb
    create  config/settings.yml
    create  config/settings.local.yml
    create  config/settings
    create  config/settings/development.yml
    create  config/settings/production.yml
    create  config/settings/test.yml
    append  .gitignore
```

各種ファイルの役割は以下。

* config/initializers/rails_config.rb

定義した定数にアクセスする為のクラス名称を定義する。デフォルトは「Settings」になっている。

* .gitignore

ファイル名称に「local」が含まれるYAMLファイルは、全てローカル環境専用のファイルとみなされる為、これらのファイルをバージョン管理に含めないような定義が追記される。

* config/settings.local.yml

ローカル環境専用のYAMLファイル。ローカル環境で動作させている場合は、全てのYAMLファイルに記述されている定数より優先して使用される。ローカル環境のみ、別の定数を割り当てたい時に使用する。

* config/settings.yml

全ての環境(development/test/production)のベースとして使用される。環境に左右されない定数を定義したい時に使用する。

* config/settings/development.yml

開発環境でのみ、別の定数を割り当てたい時に使用する。「config/settings.local.yml」との違いは、個々人のローカル環境毎に異なる定数なのか、開発環境毎に異なる定数なのかのみ。

* config/settings/test.yml

テスト環境でのみ、別の定数を割り当てたい時に使用する。

* config/settings/production.yml

本番環境でのみ、別の定数を割り当てたい時に使用する。

### 利用方法

利用する時は以下のような感じで。

```ruby config/settings.yml
service_name: "Service Name
service:
  tag_line: "Rails configuration plugin"
```

```bash
$ rails c

1.9.2-head :001 > Settings.service_name
  => "Service Name"
1.9.2-head :002 > Settings.service.tag_line
 => "Rails configuration plugin"
```

## どんな感じ？
同様の機能を持つsettings_logicというプラグインもあるが、こちらは各種ファイルの自動生成コマンドも用意されているし、ローカル環境専用ファイルも用意されているので非常に便利。