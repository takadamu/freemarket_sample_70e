# 概要
テックキャンプの最終課題にて作成したフリーマーケットのアプリケーションです  
自身で実装した箇所、および開発を通じて得られた経験について紹介します<br>

## 接続先情報
[フリマ](http://18.180.41.211/)  
ID/Pass  
ID: admin  
Pass: 2222  

### テスト用アカウント等<br>
- 購入者用  
  - メールアドレス: test1@gmail.com  
  - パスワード: 1234567  
- 購入用カード情報  
  - 番号：4242424242424242  
  - 期限：12/20  
  - セキュリティコード：123  
- 出品者用  
  - メールアドレス名: test2@gmail.com  
  - パスワード: 1234567  

# DB設計
## usersテーブル
|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false|
|encrypted_password|string|null: false| -->
### Association
- belongs_to_active_hash :birth_year
- belongs_to_active_hash :birth_month
- belongs_to_active_hash :birth_day
- belongs_to_active_hash :prefecture
- devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable
- has_many :items
- has_many :comments
- has_many :favorites
- has_one  :profile
- has_one  :user_address
- has_many :cards

## profilesテーブル
|Column|Type|Options|
|------|----|-------|
|family_name|string|null: false|
|first_name|string|null: false|
|family_name_kana|string|null: false|
|first_name_kana|string|null: false|
|birth_year|integer|null: false|
|birth_month|integer|null: false|
|birth_day|integer|null: false|
|introduction|text||
|image|string||
|phone_number|string||
|user_id|string|null: false, foreign_key: true| -->
### Association
- belongs_to :user

## user_addressesテーブル
|Column|Type|Options|
|------|----|-------|
|post_code|string|null: false|
|prefecture_code|string|null: false|
|city|string|null: false|
|house_number|string||
|building_name|string||
|user_id|string|null: false, foreign_key: true| -->
### Association
- belongs_to :user

## categories_table
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
### Association
- has_many :items
- has_ancestry

## brands_table
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
### Association
- has_many :items

## items_table
|Column|Type|Options|
|------|----|-------|
|name|string||
|buyer_id|references|foreign_key: true|
|size|string||
|item_condition|string||
|postage_payer|string||
|postage_type|string||
|prefecture_code|string||
|estimated_shipping_date|string||
|item_description|text||
|trading_status|string||
|price|integer||
|category_id|references|foreign_key: true|
|brand_id|references|foreign_key: true|
|user_id|string|foreign_key: true|
### Association
- belongs_to_active_hash :prefecture
- belongs_to_active_hash :item_size
- belongs_to_active_hash :condition
- belongs_to_active_hash :postage_pay
- belongs_to_active_hash :shipping_date
- belongs_to_active_hash :postage_ty
- has_many :item_images, dependent: :destroy
- has_many :comments, dependent: :destroy
- has_many :favorites
- belongs_to :user
- belongs_to :brand, optional: true
- belongs_to :category, optional: true

## comments_table
|Column|Type|Options|
|------|----|-------|
|user_id|references|foreign_key: true|
|item_id|references|foreign_key: true|
|message|text|null: false|
### Association
- belongs_to :user
- belongs_to :item

## cards table
|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false|
|customer_id|string|null: false|
|card_id|string|null: false|
### Association
- belongs_to :user

## item_imagesテーブル
|Column|Type|Options|
|------|----|-------|
|src|string||
|item_id|references|null: false, foreign_key: true|
### Association
- belongs_to :item

# 開発環境
Ruby/Ruby on Rails/MySQL/Github/AWS/Visual Studio Code  
開発期間と平均作業時間  
開発期間：約3週間  
1日あたりの平均作業時間：約11時間  

# 開発体制
人数：5人  
アジャイル型開発（スクラム）  
Trelloによるタスク管理  

# 動作確認方法
Chromeの最新版を利用してアクセスしてください。  
ただしデプロイ等で接続できないタイミングもございます。その際は少し時間をおいてから接続ください。  
接続先およびログイン情報については、上記の通りです。  
同時に複数の方がログインしている場合に、ログインできない可能性がございます。  
テストアカウントでログイン→トップページからログインしたユーザーの名前を選択→ユーザーマイページに遷移→サイドバーよりクレジットカード情報選択→登録・閲覧・削除
確認後、ログアウト処理をお願いします。  

# 開発担当箇所
- DB設計
[![Image from Gyazo](https://i.gyazo.com/341704edaf3d596477c2a221fb023fc0.png)](https://gyazo.com/341704edaf3d596477c2a221fb023fc0)

- ルーティングの設定(バックエンド)
- デプロイ
- ユーザーマイページ（バックエンド）
- ユーザーマイページ（フロントエンド）<br>
http://18.180.41.211/users/11にアクセスするとご覧いただけます。
[![Image from Gyazo](https://i.gyazo.com/8dc247884314bdb9b77027251711fb95.jpg)](https://gyazo.com/8dc247884314bdb9b77027251711fb95)

- クレジットカード登録（フロントエンド）  
test1アカウント（出品者用アカウント）ログイン後  
http://18.180.41.211/cards/newでご覧いただけますます。
[![Image from Gyazo](https://i.gyazo.com/9f97c5d0d8d5743b1d71edab09f81136.png)](https://gyazo.com/9f97c5d0d8d5743b1d71edab09f81136)

- クレジットカード削除（フロントエンド）  
test2アカウント（購入者用アカウント）ログイン後、  
http://18.180.41.211/cards/showでご覧いただけます。
[![Image from Gyazo](https://i.gyazo.com/763d7607de02863c4dc97ee02c685f2e.png)](https://gyazo.com/763d7607de02863c4dc97ee02c685f2e)

- クレジットカード登録（バックエンド）  
payjpに反映
- 商品購入機能（バックエンド）  
payjpに反映

- 商品購入機能（フロントエンド）

# 各担当箇所の詳細
- DB設計
  - 概要
    - 必要なテーブル、カラムの選定
    - アソシエーションの決定
  - 担当内容
    - ER図の作成
    - 各テーブルの作成
    - 各モデルの作成<br><br>
- トップページ（ログイン・未ログイン状態時の切り替え）
  - 概要
    - ログイン時と未ログイン時で表示の切り替えをする
    - ヘッダーとフッターの部分テンプレート化
  - 担当内容（バックエンド）
    - ログイン時はユーザーの名前とログアウトの表示
    - 未ログイン時はログインと新規登録の表示
  - 担当内容（フロントエンド）
    - 別ページでも使用できるよう、ヘッダーとフッターの部分テンプレート化をし、必要なページに適用・反映<br><br>
- 新規登録・ログインページ
  - 概要
    - ヘッダー・フッダー
  - 担当内容（フロントエンド）
    - ヘッダーフッターの部分テンプレート化
    - 必要ページへの適用・反映<br><br>
- ユーザーマイページ
  - 概要
    - カレントユーザー名の表示
    - マイページからログアウトができる
    - クレジットカードの登録・削除
  - 担当内容（バックエンド）
    - ログインしたユーザーの名前がプロフィールに表示される
    - クレジットカードへのアクセスキーを保存するモデル、コントローラ、ルーティングの作成
    - payjpを導入し、カード登録時にpayjp側へカード情報と顧客情報を新規作成
    - 登録した情報にアクセスする為のキーをDBへ保存する機能の実装
    - DBのキーを利用してpayjpのクレジットカード情報を取得し、自分のカード情報(下4桁,期限など)を表示する機能の実装
    - クレジット情報から削除を押すと、カード情報が削除され、再度登録できるようになる
  - 担当内容（フロントエンド）
    - haml,scssを使用しマークアップ作業
    - 「>」表示などはfont-awesomeを使用で統一
    - サイドバーにいつでも項目を追加削除できるよう、高さなどを調整
    - サイドバーの部分テンプレート化<br><br>
- 商品購入機能
  - 概要
    - クレジットカード決済後、payjpのコンソールに反映させる
  - 担当内容（バックエンド）
    - クレジットカードへのアクセスキーを保存するコントローラ内のメソッドを作成
    - 決済が完了すると注文情報、売上情報のレコードを作成する処理の実装
  - 担当内容（フロントエンド）
    - 購入完了ページのマークアップ<br><br>
- デプロイ
  - 概要
    - AWSの取得とEC2インスタンスの生成
    - Basic認証
    - S3の導入
    - Capistranoを利用した自動デプロイ
    - credentialsファイルによるキーの管理
    - DBをAWS用で作成しMySQLに反映
  - 担当内容
    - 既存のEC2インスタンスの解放と新規インスタンスの生成
    - 本番環境でのみBasic認証がされるように条件分岐を記述
    - S3にてバケットを作成し、投稿された画像がバケットに入ってくるように設定
    - Capistranoを利用した自動デプロイ化をし、本番環境で反映されないもののエラーの原因を探して解決する
    - credentialsファイルを作成し、AWSのキーを暗号化
    - ローカル環境と本番環境のDBを両方MySQLで管理

# 開発を通じて得られた知見
## 工夫した点
### ①チームとして工夫を行った点
最初にいくつかチームの約束事を設定し、コミニュケーションをしっかり取ることで、メンバーの状況や進捗をみんなが把握できるよう徹底しました。それにより、進捗の遅れを事前に防ぎ、計画通りに作業を進める事ができました。  
また、分からなすぎて途方に暮れてしまうことがないように、各々の技術レベルを考慮し実装するページを割り振ったことで、マークアップとサーバーサイドをどちらも経験できるような心の余裕も作ることができたと思います。

### ②個人として工夫を行った点
デプロイやpayjpなど、みんなが避けてしまいがちな部分を積極的に実装するよう心がけました。また、各々が実装しているページのヘッダーやフッターをこちらで早めに部分テンプレート化させ、ビューをある程度調整させたことで、ページ遷移の流れなど全体のイメージが掴みやすくなり、スムーズに開発ができたと思います。

# 苦労した点
### ①スクラムマスターとして
チーム開発初期、メンバーの「やめたい」「帰りたい」「もうむり」と飛び交うネガティブな言葉に戸惑いを感じ、スクラムマスターとしてチームの士気を下げないよう「自分だけは絶対にポジティブな発言しかしない」と決めて開発をしました。  
しかし、諸連絡への返事がない、土日に何をしているか分からない状態が続き、どんなに士気を下げないように自分だけが努力をしても、それはチーム開発とは言えないことに気付き、一人で抱えずメンバーにシェアすることにしました。  
チームの約束事を決め、コミュニケーションをしっかり取るよう意識したところ、一人ひとりの主体性が上がり、メンバーから「今一番楽しい！」とポジティブな言葉も聞けるようになりました。  
チーム開発において、指針を示すリーダーのような存在は必要だけれど、開発に関わる一人ひとりの意識が一致することが、開発を円滑にする一番の近道だと感じました。  
今後企業に入り開発を進める時、コミュニケーションを取ることを怠らないようにし、自ら進んで発信していこうと思います。

### ②デプロイ
アプリが完成していない初期段階で自動デプロイをするのが初めてだったため、見たことのないエラーを何度も経験しました。  
デプロイ自体に問題がなくても、マージしたファイルの記述に問題があったりなど、エラーの原因を探し出すためには順序があることや、色々なログの見方を学びました。何度も経験で、エラーへの抵抗がなくなり、冷静に対処することができるようになりました。

### ③自分以外の人が書いたコードの読み解き修正
自分以外のメンバーが担当した箇所でエラーが起きた際、担当者が技術的に不安があるとのことでエラー解決を引き受けました。  
人が書いたコードを読み解き修正する作業は初めてだったため、読み解く作業に苦労しました。  
どの記述は必要なのか解読し、足りていないものは何なのか自分なりに考えて実装したところ、エラーは解決し反映させることができました。  
人のコードを読める技術と、人が読んでもわかるコードを書く記述の大切さを実感することができたので、今後の開発では「読みやすいコードを書く」ことにも重点を置いていこうと思います。

### ③GitHub
作業当初に全ブランチでコンフリクトが起き、解決策が分からず苦労しました。  
開発を進めていく中で、コンフリクトが起こる箇所があらかじめわかるようになり、メンバーには事前に「どのブランチでどのようなコンフリクトが起こる可能性があるか」「起こったときの対処法」を伝えることで、混乱なくスムーズに開発を進めることができるようになりました。  
コンフリクトは必ず起きるものだとは思いますが「いかにコンフリクトを少なくするか」「回避するか」という視点で、一歩先のことを考えながら開発を進めていく技術を身に付けていきたいです。  
<br>
<br>
以上
