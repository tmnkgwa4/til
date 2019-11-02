# Terraform 概要

## what is terrafrom?
1. インフラストラクチャ定義ツール
1. 宣言的にクラウド上のリソースを定義することができるのが特徴

## 構成要素
1. HCL
  1. *H*ashicorp *C*onfiguration *L*anguageの略
  1. 設定言語のこと
1. Resource
  1. リソースは重要な構成要素
  1. このブロックでAWS、GCPなどのクラウドリソースを定義する
  1. なので、クラウドリソース = Resourceと読み替えても良いかも
1. Datasource
  1. ReadonlyなResourceのこと
  1. ROなためTerraform管理外だが、Terraformから参照したいデータのことを指す
1. Provider
  1. Resourceの作成更新削除に実行するプラグイン
1. State
  1. Terraformが認識するResouce状態
  1. `*.tfstate`ファイルに保存される

## 主なコマンド
1. terraform init
  1. Terraformを初期化する上でまず最初に実行するコマンド
  1. 作業領域の初期化
  1. これを実行すると`*.tf`ファイルで定義しているプラグインのダウンロード処理が始まる
  1. ダウンロードファイルは`.terraform`フォルダに保存される
1. terraform plan
  1. apply時にどのようなリソースが作成/更新/削除されるかをdry-runするコマンド
1. terraform apply
  1. `*.tf`ファイルを基に、リソースの生成を行うコマンド
  1. リソースが生成されると、`terraform.state`というファイルにリソースに関連する情報が保存される
  1. 1世代前のものがバックアップされ、`terraform.state.backup`に保存される
1. terraform show
  1. ステータス確認コマンド
  1. 実際には`terraform.state`ファイルの状態をステータスを表示する
1. terraform fmt
  1. formatを自動で修正してくれるコマンド
1. terraform destroy
  1. Terraformプロジェクトを削除するコマンド

## reference
[Terraform職人入門: 日々の運用で学んだ知見を淡々とまとめる](https://qiita.com/minamijoyo/items/1f57c62bed781ab8f4d7)
