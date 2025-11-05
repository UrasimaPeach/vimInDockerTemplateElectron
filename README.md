# vimInDockerTemplateElectron

dockerの中でvimを使う環境を構築するためのテンプレートです。
Electronアプリを作るための設定用です。

# Requirements

docker, sh

# 事前準備

## rootでないユーザーでdockerを実行するようにする。

dockerはホスト側のrootユーザー以外で使うほうが通常望ましいです。
特に理由がない場合、ホスト側のOSで下記1, 2を実行してから再起動してください。

### 1. dockerグループに自身を追加

dockerのユーザーとして自身を追加する必要があります。
下記のコマンドを使用してください。

```
sudo usermod -aG docker `whoami`;grep docker /etc/group
```

### 2. ユーザーのリマップ設定の変更

docker内での挙動をコンテナ内ではroot、コンテナ外では実行ユーザーとして扱う設定を記入します。
ホストの/etc/docker/daemon.jsonに下記の設定を追加してください。(ファイルがなければ新たなjsonとして保存してください。)

```
{
  "userns-remap": "default"
}
```

# 使用方法

vimで編集するプロジェクトを新しく始めたい場合、以下のコマンドを使います。
その後は、新しいプロジェクト内のREADME.mdを参照してください。

```
cp -r TEMPLATE_DEVELOP_DOCKER ../newPrj
cd ../newPrj
vim scripts/init.sh # ファイル先頭の変数3つを埋める
./scripts/init.sh
```

# LICENSE

MIT Lisence
