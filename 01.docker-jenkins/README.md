# 何を実現しているか？

## ブラウザでアクセス可能なJenkinsサーバーの作成
```& docker-compose up -d```を実行するとJenkinsサーバーを動作させているコンテナーが立ち上がる。
```http://localhost:8080```にブラウザでアクセスするとJenkinsを確認できる。

## データをjenkins_homeフォルダーで永続化

ホストの```./jenkins_home```とmasterの```/var/jenkins_home```をマウントしているため、コンテナを削除して再作成しても前回と同じ状態を復元できる。

## SSHキーを設定してJenkinsからNodeの設定をすればMaster/Slaveとして利用できる
JenkinsのMasterコンテナ(jenkins_container_master)だけでなく、Slave(slave01)も動作しているので設定をすればSlaveを活用できるようになっている。なお、sshキーは一度Jenkinsを起動させた後、```$ docker container exec -it jenkins_container_master ssh-keygen -t rsa -C ""```を実行(Fileは```/var/jenkins_home/.ssh/id_rsa```。パスワードはEmpty。)してssh keyを作成して、```docker-compose.yml```のJENKINS_SLAVE_SSH_PUBKEYを作成した公開鍵で置き換える。