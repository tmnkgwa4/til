# Terraform 概要

# what is terrafrom?
- インフラストラクチャ定義ツール
- 宣言的にクラウド上のリソースを定義することができるのが特徴

# 構成要素
|用語|概要|
|---|:---:|
|Configration|Terrafromコードのこと。|
|HCL|HasicorpConfigurationLanguageの略。|
|Resource|Terraformで管理する対象の基本単位|
|DataSource|Terraform管理外だが、Terraformから参照したいデータ|
|インフラ設定のコード。要するに *.tf ファイルにDSLで書くTerraformのコードのこと。
|Provider|ResourceやDataSourceなどを作成/更新/削除するプラグイン|
Provisioner|Resourceの作成/更新/削除時に実行するスクリプトなどのプラグイン|
|State|Terraformが認識しているResourceの状態。*.tfstateに保存される。|
|Backend||Stateの保存先。localやs3などが挙げられる。|
|Module|ResouceやDataSourceなどを再利用可能なようにまとめたもの。|

[Terraform職人入門: 日々の運用で学んだ知見を淡々とまとめる](https://qiita.com/minamijoyo/items/1f57c62bed781ab8f4d7)

