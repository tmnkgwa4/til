# Terraform 概要

## what is terrafrom?
- インフラストラクチャ定義ツール
- 宣言的にクラウド上のリソースを定義することができるのが特徴

## 構成要素
1. Configration
  - 
1. HCL
  - *H*ashicorp *C*onfiguration *L*anguageの略
  - 設定言語のこと
1. Resource
  - リソースは重要な構成要素
  - このブロックでAWS、GCPなどのクラウドリソースを定義する
  - なので、クラウドリソース = Resourceと読み替えても良いかも
1. Datasource
  - ReadonlyなResourceのこと
  - ROなためTerraform管理外だが、Terraformから参照したいデータのことを指す
1. Provider
  - Resourceの作成更新削除に実行するプラグイン
1. State
  - Terraformが認識するResouce状態
  - `*.tfstate`ファイルに保存される

## 主なコマンド
1. terraform init
  - Terraformを初期化する上でまず最初に実行するコマンド
  - 作業領域の初期化
  - これを実行すると`*.tf`ファイルで定義しているプラグインのダウンロード処理が始まる
1. terraform plan
  - 
1. terraform apply
  - 
1. terraform show
  - 
1. terraform fmt
  - 
1. terraform destroy
  - 

## reference
[Terraform職人入門: 日々の運用で学んだ知見を淡々とまとめる](https://qiita.com/minamijoyo/items/1f57c62bed781ab8f4d7)
