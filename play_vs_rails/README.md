# PlayとRails、どうして差がついたのか

subtitle
:   2016/5/13 オプト社内勉強会

allotted-time
:   15m

# 自己紹介
渋谷　充宏 @m4buya

* サーバーサイドプログラマ
* Ruby / Scala
* https://github.com/mshibuya
* RailsAdmin committer


# 本日のテーマ
オプト開発２部のプロダクトで多く使われているPlay Frameworkと
自分が慣れ親しんだRailsを独断と偏見(と些少な知識)をもって比較することで、
得手不得手など見えてきたらいいな…という感じです



# Play Framework

![](https://www.playframework.com/assets/images/logos/play_full_color.svg){:relative_height='100'}


# Play Framework

https://www.playframework.com/documentation/ja/2.3.x/Home

    Play は、現代の web アプリケーション開発に
    必要なコンポーネント及び API を統合した生産性の高い
    Java と Scala の web アプリケーションフレームワークです。
    
    Play の特徴は、ライトウェイト、ステートレス、webフレンドリーな
    アーキテクチャであること、機能予測のしやすさです。また、
    Iteratee IO をベースにしたリアクティブモデルのおかげで、
    スケーラブルなアプリケーションでも
    CPU、メモリ、スレッドなどのリソース消費が最小限になっています。



# Ruby on Rails

![](https://www.endpoint.com/images/logos/rails.png){:relative_height='70'}

# Ruby on Rails

https://ja.wikipedia.org/wiki/Ruby_on_Rails

    Railsの基本理念は
    「同じことを繰り返さない」（DRY:Don't Repeat Yourself）と
    「設定より規約」（CoC:Convention over Configuration）である。




# ORM

![](http://www.agile-code.com/blog/wp-content/uploads/2013/03/ORMMapping.png){:relative_height='100'}

# Play

* 標準ではEBean
  * 知らない。。
* Slick
* Skinny
* ScalikeJDBC
	* ORMなの?

# Rails

* ActiveRecord
* Mongoid(MongoDB)
* DataMapper(開発止まってる)
* Sequel


# Scaffold

![](http://previews.123rf.com/images/stokkete/stokkete1211/stokkete121100170/16230601-Silhouette-of-construction-workers-on-scaffold-working-under-a-blue-sky-Stock-Photo.jpg){:relative_height='100'}


# Play

* Scalaだとなさそう？
* Javaならある
  * https://github.com/lmcalpin/Play--Scaffold


# Rails

強力

    create  app/controllers/welcome_controller.rb
     route  get 'welcome/index'
    invoke  erb
    create    app/views/welcome
    create    app/views/welcome/index.html.erb
    invoke  test_unit
    create    test/controllers/welcome_controller_test.rb
    invoke  helper
    create    app/helpers/welcome_helper.rb
    invoke  assets
    invoke    coffee
    create      app/assets/javascripts/welcome.js.coffee
    invoke    scss
    create      app/assets/stylesheets/welcome.css.scss


# Routing

![](https://upload.wikimedia.org/wikipedia/en/thumb/0/06/Georouting_face_routing.svg/336px-Georouting_face_routing.svg.png){:relative_height='100'}

# Play

    GET   /clients/:id          controllers.Clients.show(id: Long)
    GET   /clients/all          controllers.Clients.list()
    POST  /clients              controllers.Clients.create()
    PUT   /clients/:id          controllers.Clients.update(id: Long)

- 外部DSL
- マッピングのみ

# Rails

    resources :clients
    namespace :admin do
      resources :users
    end


- 内部DSL
- 高機能

# View

![](http://img11.deviantart.net/1047/i/2012/082/b/e/view_from_gubalowka_by_cyberkiller1-d4toa0j.jpg){:relative_height='100'}

# Play

引数に型がある！

    @(customer: Customer, orders: List[Order])
    
    <h1>Welcome @customer.name!</h1>
    
    <ul>
    @for(order <- orders) {
      <li>@order.title</li>
    }
    </ul>


# Rails

    <h1>Names of all the people</h1>
    <% @people.each do |person| %>
      Name: <%= person.name %><br>
    <% end %>


# Form

![](https://pixabay.com/static/uploads/photo/2012/04/25/00/23/checklist-41335_960_720.png){:relative_height='100'}

# Play

case classを作っておき、マッピング

    case class User(name: String, age: Long)
    
    val userForm = Form(
      mapping(
        "name" -> text,
        "age" -> number
      )(UserData.apply)(UserData.unapply)
    )

# Rails

マッピングとかない。ARオブジェクトにつっこんで終わり

    Person.create(params[:person])

# 並行処理
![](https://upload.wikimedia.org/wikipedia/commons/e/e9/Greensboro_road_signs.jpg){:relative_height='100'}


# Play
- 非同期・イベントドリブン
- スレッドプールは低め
	- ブロッキングなIOをたくさんするとパフォーマンスに影響がでる

# Rails
* マルチプロセス or マルチスレッド
* たくさん並べればなんとかなる
  * メモリとかたくさん食いがち

# まとめ
* Play
  * Scalaいい
    * 型
* Rails
  * Ruby素敵

# ご静聴ありがとうございました
![](https://raw.github.com/rabbit-shocker/rabbit/master/sample/lavie.png){:relative_height='80'}


