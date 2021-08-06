# Docker コマンドチートシート

#### Docker公式リファレンス
日本語版: https://docs.docker.jp/

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

- オプション<br>
`-d` コンテナをバックグラウンドで実行する。このオプションを加えない場合、コンテナ起動時に実行されるコマンドを実行した状態になり、コマンドによってコマンドのコンソール出力が表示された状態などになる。<br>
`--name` コンテナ名を指定する。<br>
`-p` ホストとコンテナ間のポートフォワード設定する。「-p <host側のポート>:<コンテナ側のポート>」<br>

#### イメージの削除
```
docker rmi <image-name>or<image-ID>
```

#### コンテナの削除
```
docker rm <container-name>or<container-ID>
```

#### 外部イメージの取得
```
docker pull <image-name>
```

#### コピー
```
docker cp <コンテナ名>:<コンテナ内のコピー元ファイル> <ホスト側のコピー先ディレクトリ>
```

#### コンテナからDockerイメージ作成
```
docker commit <コンテナ名> <作成するDockerイメージ名>
```

#### コンテナ起動、停止
```
docker start <コンテナ名>
docker stop <コンテナ名>
```

### Dockerfile
https://knowledge.sakura.ad.jp/15253/
公開されているDockerイメージをそのまま使うのではなく、必要なパッケージやアプリ、各種設定を含んだDockerイメージを自分で作成して使用するケースが出てくる。その場合、Dockerfileを作成し、それを使用して必要なDockerイメージを作成することができます。Dockerfileには、ベースとするDockerイメージに対して実行する内容を記述する。

・流れ
Dockerfileに記述→`docker bulid`でイメージを作成する。
```
docker build -t <Dockerイメージ名> <Dockerfileが存在するディレクトリ>
```

### docker-composeとは
https://knowledge.sakura.ad.jp/16862/

Dockerイメージのビルドや各コンテナの起動・停止などをより簡単に行えるようにするツールである。
`docker-compose.yml`というファイルに設定を記述する。

#### docker-composeでのコンテナの起動
`docker-compose.yml`が置いてあるディレクトリで以下のコマンドを実行
```
docker-compose up -d
```

#### コンテナの起動状態の確認
```
docker-compose ps
```

#### docker-composeでのイメージのbuildからコンテナの起動まで
・Dockerfileにイメージの内容を記述<br>
・docker-compose.ymlに処理を記述<br>
docker-compose.ymlのあるディレクトリで
以下のコマンドを順に実行
```
# まだイメージを作ってないときはここから
docker-compose build

# イメージを既に作っている場合はここから
# コンテナの起動
docker-compose up -d

# コンテナの停止
docker-compose stop

# コンテナの削除(-fをつけることでyes/noを聞かれずに削除を実行) 
docker-compose rm

# 停止、削除、ネットワーク削除を全て実行する場合
docker-compose down

# イメージもあわせて削除する場合
docker-compose down --rmi all

```
