---
layout: post
title: "Heroku Scheduler"
date: 2012-01-11 20:24
comments: true
categories: heroku
---

## Heroku Scheduler

Heroku上で10分、1時間、1日間隔でバックグラウンドジョブを実行出来る無料アドオンです。

<!-- more -->

### 公式ドキュメント

http://devcenter.heroku.com/articles/scheduler

### 参考になるエントリー

http://blogjp.sforce.com/2011/11/heroku-schedule-dc69.html
http://sadayuki.hateblo.jp/entry/2011/12/28/194235
http://d.hatena.ne.jp/ToMmY/20111121/1321802014

***

### タスクを準備

バックグラウンドで実行するタスクを用意します。

```ruby lib/tasks/scheduler.rake
desc "This task is called by the Heroku scheduler add-on"
task :create_sample => :environment do
  puts "fakestarbaby"
end
```

### タスクの詳細設定

Heroku Schedulerアドオンを追加して、タスクを実行するように設定します。

![Heroku Scheduler](http://f.cl.ly/items/3w1z2k0o2P3M1M1T3k44/heroku_scheduler.jpg "Heroku Scheduler")

ここでは、タスクを「bundle exec rake create_sample」、間隔を10分に設定してみました。
後は、「Run」ボタンを押下すれば、バックグラウンドジョブが10分間隔で実行されるようになります。

## まとめ

同様のHerokuアドオンとして提供されているHeroku Cronは、アドオンを追加したタイミングから1日間隔でしかバックグラウンドジョブを実行出来ないが、こちらは柔軟に間隔を任意選択出来るのでとっても便利だなーと思った。