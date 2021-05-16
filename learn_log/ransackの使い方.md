## 内容
gem ransackを使って検索機能を実装する方法を記述

## ransackをインストールする
Gemfileにransackを記述

```
gem 'ransack'
```

ターミナルにて

```
$ bundle install
```

※サーバーを再起動する


## 検索したいcontrollerにて

```rb
def index
  @q = Question.ransack(params[:q])
  @questions = @q.result(disitinct: true)
end
```

## html.erbにて

```erb
<%= search_form_for @q do |f| %>

  <%= f.label :title_cont %>
  <%= f.search_field :title_cont %>

  <%= f.submit %>
```
今回の場合は`_cont`を使用（入力した文字を含んでいるもの）

参考
https://github.com/activerecord-hackery/ransack

[![Image from Gyazo](https://i.gyazo.com/9bd61e35f49fad1caff57575a9007a73.png)](https://gyazo.com/9bd61e35f49fad1caff57575a9007a73)

## 内容でも検索したい
以下のような投稿の時にタイトルだけでなくbodyの内容も検索に引っ掛けたい
[![Image from Gyazo](https://i.gyazo.com/5e39c6cad9a1342a11ee58d0e38c3c93.png)](https://gyazo.com/5e39c6cad9a1342a11ee58d0e38c3c93)

```erb
<%= search_form_for @q do |f| %>

  <%= f.label :title_cont %>
  <%= f.search_field :title_or_body_cont %>

  <%= f.submit %>
<% end %>
```
のように`or`を使うと

[![Image from Gyazo](https://i.gyazo.com/4ffbb47d75e47dc48789059f3c89ebdd.png)](https://gyazo.com/4ffbb47d75e47dc48789059f3c89ebdd)
検索に該当することができる