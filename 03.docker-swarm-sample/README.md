# 何を実現しているか？

## Serviceの使い方の実践

ホストに次の４つのコンテナを作成し、あるイメージをDocker Swarmを使ってWorkerに配置するための環境を構築している。


|No|Container Name| Description |
|:---:|:---| :--- |
|1| Repository | Dockerイメージを格納しておりポート5000でホストおよび他のコンテナーから見えるようにしている。 |
|2| Manager(dind) | serviceの管理者としてDockerイメージを各Workerコンテナにデプロイするためのコンテナ。 |
|3| Worker01(dind) | mangerのserviceに所属させるコンテナ |
|4| Worker02(dind) | mangerのserviceに所属させるコンテナ |
|5| Worker03(dind) | mangerのserviceに所属させるコンテナ |

ここでは、`$ docker-compose up -d`の後に手動でService関係の設定を全て実施している。

### 利用するイメージ
02.docker-example-echoで作成した`example/echo:latest`イメージ