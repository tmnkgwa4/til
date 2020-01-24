# FlyWay って?

## OverView
- FlyWay は データベース マイグレーションツールである
  - この DB Migration とは、移行を意味するものではなく、DB 環境 (スキーマ+データ) を移行して、同一状態のDB環境を構築するもの

## 動作確認
### 必要なもの

- mysql docker-compose.yaml
```
version: '3.4'

x-template: &flyway-template
  image: boxfuse/flyway:latest
  volumes:
    - ./sql:/flyway/sql # マイグレーション用SQLファイルの格納先
    - ./conf:/flyway/conf # 設定ファイルの格納先
  depends_on:
    - db

services:
  flyway-clean:
    <<: *flyway-template
    command: clean

  flyway-migrate:
    <<: *flyway-template
    command: migrate

  flyway-info:
    <<: *flyway-template
    command: info

  db:
    image: postgres:latest
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
    ports:
      - 5432:5432
    volumes:
      - ./init:/docker-entrypoint-initdb.d # Create DataBase するinit用のSQLの格納先
    container_name: db
```

