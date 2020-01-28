# [WIP] RDS replica lag とは？

## Overview
- Network に関わっていた時間が長かったため、LAG = **L**ink **AG**gregation しか浮かんでこなくて恥を書いたため調査
  - Time Lag のことだ!

### そもそも replica とは？
- データの複製のこと
  - Master DB
    - データを変更
    - 変更内容を Slave に転送
    - Master は 複数の Slave を持つことができる
  - Slave DB ( Read Replica )
    - Master DB での変更内容を受け取ることができる
    - Read Replica では、デフォルトで ReadOnly
      - 設定で Write も可能

## どんなときに嬉しいの？
  - DB へのアクセス頻度が高く、DBサーバのリソースが逼迫している場合、スケールアップ（サーバのスペックを上げる）ことが多い。
  - しかし、スケールアップが困難である場合は読み込みを分散してシステム全体のパフォーマンス向上を図る
    - 一般的には Write のほうが Read よりも少ない
    - Write は ACID の観点から、水平分散が難しい
      - 原子性 Atomicity
        - トランザクションに含まれるタスクがすべて実行されるか、あるいは全く実行されないことを保証する性質
        - 例: 1万円の送金
          - 口座Aの残高から1万円を引く
          - 口座Bの残高に1万円を加える
          - 上記2操作はすべて行われるか、全く行われないことを指す。
          - 預金に矛盾が生じちゃうから。
      - 一貫性 Consistency
        - 整合性とも言われる
        - トランザクション開始と終了時に予め与えられた整合性を満たすこと
        - 例: 1万円の送金
          - 口座Aの残高から1万円を引く
          - 口座Bの残高に1万円を加える
          - このなかで、口座Aの残高を瞬間的にマイナスにするような処理はできない
            - 極端にいうと、残高を一旦引き出して、送金分を差し引いて処理を加えて、残りを残高に入れ直すような処理はできない。
      - 独立性 Isolation
        - トランザクション中に行われる操作の過程が他の操作から隠蔽されること
      - 永続性 Duration
        - トランザクション操作の完了通知をユーザが受けた時点で、その操作は永続的になる

## 実装
- Master DB の ReadOnly のレプリカ を作成する
- App からデータを読み込む際、リードレプリカをアクセス先に設定する
- 複数のリードレプリカを利用することは可能だが、app側で振り分けすることで更に負荷分散が見込める
- DB からの読み込み負荷が高い場合、負荷を分散できる
- DB 解析用途などでマスターに負荷をかけずに処理したいときにも有効
- Read Replica はマスターに昇格することも可能

## 注意点
- Read Replica は冗長目的ではない。ちゃんと冗長したい場合は、Master - Slave のレプリケーションを検討してね
- 一般的にレプリケーションは非同期である
  - Master と Read Replica の間には若干の LAG があることを理解する
    - これが Replica LAGのこと
    - LAG が大きいと、Master のデータが反映されるのに時間が伴うため
  - RDS は自動バックアップを無効にすると、そのRDSからRead Replica を作成することができない

## Reference
- [CDP](http://aws.clouddesignpattern.org/index.php/CDP:Read_Replicaパターン)
