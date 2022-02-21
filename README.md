# Nginx Practice
## 概要
Docker Composeを利用したNginxのお試し環境です。デフォルトでは複数のNginxを起動させて、サービス名でリバースプロキシするようにしています。

## テスト用のコマンド
以下のコマンドはDockerのネットワーク外からリクエストする場合のコマンドです。

```bash
# nginx-frontendにリクエストする場合
curl localhost

# nginx-backend1にリクエストする場合
curl localhost -H "Host:nginx-backend1"

# nginx-backend2にリクエストする場合
curl localhost -H "Host:nginx-backend2"
```

## Dockerのネットワーク外からサービス名で名前解決する

実行している環境の`/etc/hosts`を書き換えることで、`-H`を使用せずにサービス名で直接リクエストできるようになります。

注：`/etc/hosts`を下手に書き換えると`localhost`が使えなくなったりするので、必ずバックアップ取ってから編集しましょう。

```text:/etc/host.conf
~~~
既存の設定
~~~

127.0.0.1 nginx-backend1 nginx-backend2

```

なおDockerが自動でこの設定をしてくれるため、同じネットワークに所属していれば、設定することなくサービス名で名前解決できます。