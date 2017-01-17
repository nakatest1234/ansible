おれおれansible
-------------------------------------------
* Centos6(x64)/amzn-linux(x64)でしか使っていません。
* 一応ベストプラクティスは目を通しています。とりあえずファイル構成だけでも。

# タグ指定で処理を選択
| タグ | 処理内容 |
| ---- | -------- |
| check | ip確認 |
| useradd | ユーザー追加。group, 秘密鍵送信, authorized_keys設定 |
| init | 初期設定。JST, logrotate(ext), yum(sysstat,wget,yum-utils) |
| chatwork | チャットワーク通知する。-e "chatwork="で設定ファイルのキー名を指定 |
| yum-repo | epel, remi, rpmforgeを追加する。enabled=0に設定 |
| php56 | php5.6 |
| php56-fpm | php-fpmインストール。socketのuser,group指定はnobodyでとりあえず入れるだけ |
| nginx | nginxを入れる。php, php-fpmも入る。 |

# コマンド
タグを指定
```
ansible-playbook -i hosts -l <host,group> -t useradd site.yml
```
*対象ホスト・グループもタグもどちらも複数指定できます*

チャットワークに通知する, chatworkのグループ指定
```
ansible-playbook -i hosts -l <host,group> -t chatwork site.yml -e "chatwork=hogehoge"
```
*リリース系プレイブックのお供に*

# インベントリファイル指定せずにホストを指定する
hostname,末尾にカンマ。連続して指定できる
```
ansible-playbook --user=ec2-user --private-key=~/ec2-user.pem -i "hostname1,hostname2," -t check site.yml
```

## 個人メモ
構文チェック
```
ansible-playbook ... --syntax-check
```

パスワード接続(-k)(sshpassインストール必須)
```
ansible-playbook ... -k
```

sudoパスワード設定(-K)
```
ansible-playbook ... -K
```

実行予定タスク一覧(--list-tasks, --list-task)
```
ansible-playbook ... --list-tasks
```

実行予定ホスト一覧(--list-hosts, --list-host)
```
ansible-playbook ... --list-hosts
```

コマンド単品
```
ansible all --user=ec2-user --private-key=~/ec-user.pem -i "host1,host2," -m shell -a "yum -y update" -s
```
