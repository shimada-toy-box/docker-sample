# 開発環境構築手順
## 前提条件
- [Docker for Mac](https://docs.docker.com/docker-for-mac/install/) がインストールされていること
- [docker-compose](https://docs.docker.com/compose/install/) がインストールされていること

### 参考
[Docker ドキュメント日本語化プロジェクト](http://docs.docker.jp/)

## installation
以下のコマンドを実行することで環境構築と起動が行われる
```
bin/docker up
```

## ショートカットコマンド

### コマンド一覧
以下でdockerを操作するショートカットコマンドを実行でる
```
cd {project_root}
bin/docker {command}
```

| command | 内容 | 例 |
| --- | --- | --- |
| attach | 指定したコンテナの標準入力にアタッチする | bin/docker attach api |
| build | イメージを作成する | bin/docker build |
| bundle | bundle コマンドを実行する | bin/docker bundle install |
| destroy | docker環境を完全に削除 | bin/docker destroy |
| down | コンテナを削除する | bin/docker down |
| clean | コンテナとイメージを削除する | bin/docker clean |
| exec | 任意のコンテナでコマンドを実行する | bin/docker exec spring rails c |
| init | docker環境を初期化する | bin/docker init |
| rails | rails コマンドを実行する | bin/docker rails c |
| rake | rake コマンドを実行する | bin/docker rake db:schema:load |
| rubocop | rubocop コマンドを実行する | bin/docker rubocop |
| run | 任意のコンテナを立ち上げてコマンドを実行する | bin/docker run web bundle install |
| stats | コンテナのリソース監視する  | bin/docker stats |
| stop | コンテナを停止する  | bin/docker stop |
| top | コンテナ内のプロセスを表示  | bin/docker top |
| up | コンテナを立ち上げる | bin/docker up |

### TIPS

#### bin/docker up
コンテナを立ち上げるコマンド
docker環境が初期化されていない場合は初期化も行う

#### bin/docker destroy
docker環境を完全に消し去るコマンド。DBのデータなども吹き飛んでしまう。
docker環境が壊れてどうしようもないような場合に使う。

#### bin/docker init
destroyを実行した後に環境構築処理を行う
docker環境が壊れてどうしようもないような場合に使う。

#### bin/docker stop
コンテナを止める。作業を中断するときはこのコマンドを利用する。

#### bin/docker clean
コンテナとイメージを削除する。
イメージを削除することで容量に空きができるため、長期間作業を行わない場合はこのコマンドを使うことをオススメする。
このコマンドではDBのデータなどは削除されない。

### bin/docker attach api
指定したコンテナの標準入力にアタッチする
railsのbyebugを利用する際はapiコンテナにアタッチすること

#### 各アプリケーションのショートカットコマンド
`bin/docker bundle` とか `bin/docker rails` とか `bin/docker rubocop`などアプリケーションを実行するためのコマンドについては、実行に最適なコンテナで実行されるように調整されているため積極的に利用することを推奨。

## Mailhog
アプリケーションから送信したメールは全てmailhogコンテナ内に保管され、実際に外部のメールサーバーには送信しないようにしてある。

この設定により開発環境で想定外の相手に対してメールを送信するような事故を防ぐ。

### コンソール
以下のURLで受信したメールを確認することができる

[http://localhost:8025/](http://localhost:8025/)

### 転送設定
mailhogには受信したメールを再転送する仕組みがある。

転送先メーラーの設定を登録しておく場合は以下を参考に `mailhog/outgoing_smtp.json` を修正すること

**mailhog/outgoing_smtp.json のサンプル**
```
{
    "google": {
        "name": "Google",
        "host": "smtp.gmail.com",
        "port": "587",
        "username": "sample@example.com",
        "password": "your application password",
        "mechanism": "PLAIN"
    }
}
```

### 参考
[https://github.com/mailhog/MailHog](https://github.com/mailhog/MailHog)

