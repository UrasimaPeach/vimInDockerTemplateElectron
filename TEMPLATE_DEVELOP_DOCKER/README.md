# 開発環境テンプレート

概要

# 使用方法


# 以下技術者(開発者)向け

## Requirements

docker, sh

## 開発環境

このプロダクトではdockerを使って開発と動作確認が行われます。
リポジトリのルートディレクトリは開発環境内でマウントしているので、root権限で実行すれば通常通りソースコードの編集などの作業が可能です。
devContainer等使うほうが行儀がいいと思いますが、管理人はVSCodeよりもvimを使いたいので開発環境内コマンドでvimを使って開発を進めています。
VSCodeを使いたい人はRemote Desktopなどを使うと良いでしょう。(その場合は追加のymlファイルなどPRくださればレビューします。)

## 実行方法

1. 「コマンド」の「コンテナのビルド」
2. 「コマンド」の「コンテナの実行」
3. 「コマンド」の「コンテナへのアクセス」

(「コマンド」の「コンテナのビルド」は初回だけでOKです。)

## コマンド

### コンテナのビルド

以下のコマンドでコンテナを立ち上げることでユーザー用の実行環境が出来上がります。

```
docker compoose build --build-arg UID=`id -u` --build-arg GID=`id -g` --build-arg USERNAME=`whoami`
```

### コンテナの実行

以下のコマンドで開発環境兼実行環境をデーモンとして実行します。

```
docker compose up -d
```

### コンテナへのアクセス

以下のコマンドで開発環境のDockerにアクセスする。

```
./scripts/ad.sh
```

最初にコンテナにアクセスした時、コンテナ内でvimの設定ファイルの初期化を行う。
また、npmの設定もコピーする。

```
./scripts/init_in_container.sh
PROJECT_NAME=hoge # 任意のプロジェクト名を指定する
mkdir ${PROJECT_NAME}
cp package.json.example ${PROJECT_NAME}/package.json 
cp forge.config.js.example ${PROJECT_NAME}/forge.config.js
cp main.js.example ${PROJECT_NAME}/main.js
cp index.html.example ${PROJECT_NAME}/index.html
cd ${PROJECT_NAME}
npm install
```

### コンテナの終了

以下のコマンドで開発環境兼実行環境のデーモンを落とします。

```
docker-compose down
```

### 開発環境内コマンド

#### 開発環境内でvimを使う。

```
vim src/example.tsx
```

#### 依存ライブラリのライセンスを出力する

```
cd ${PROJECT_NAME}
npm install -g yarn # 基本的にnpmを使う想定のコンテナだが、ライセンスを出力するために一時的にyarnをコンテナにインストール
yarn licenses generate-disclaimer > public/THIRD_PARTY_LICENSES.txt
```

#### Electron製のアプリの動作確認

なお動作確認のコンテナ内にはフォントがないので、日本語を含むデータを確認したい場合はビルドを行って別の環境で確認してください。

コンテナ内
```
npm run start
```

コンテナ外でxwindow systemあるいはwaylandへのアクセスをローカルホストのみ許可する必要がある場合、下記のコマンドを使用してください。

```
xhost +local:
```

確認の後、閉じるコマンドは下記のとおりです。

```
xhost -
```

#### Electron製アプリをmakeして実行ファイルを出力する

```
npm run make
```

#### Electron製アプリをpackageして配布形式にする

```
npm run package
```

# LISCENCE

MIT License

# Author

FIRST_AUTHOR_NAME
