# Docker コマンドチートシート

#### ローカル環境のDockerイメージの取得
```
docker images
```

#### ローカル環境のDockerコンテナの一覧を取得
```
docker ps -a
```

- CONTAINER ID
コンテナのID
- IMAGE
使用したDockerイメージ
- COMMAND
コンテナ起動時にコンテナ内で実行するコマンド
- CREATED
コンテナを実行したタイミング
- STATUS
コンテナの状態
- PORTS
ポートフォワード設定
- NAMES
コンテナの名前

#### コンテナの起動
イメージを使用して、コンテナを起動する。
```
docker run <image-name>
```

#### イメージの削除
```
docker rmi <image-name>or<image-ID>
```

#### コンテナの削除
```
docker rm <container-name>or<container-ID>
```
