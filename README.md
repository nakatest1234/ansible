Centos6
-------------------------------------------
タグ
  * check
  * useradd
  * chatwork

基本形
```
ansible-playbook -i hosts -l <host,group> site.yml
```

タグを指定
```
ansible-playbook -i hosts -l <host,group> -t useradd site.yml
```

チャットワークに通知する
```
ansible-playbook -i hosts -l <host,group> -t chatwork site.yml -k
```

チャットワークに通知する + chatworkのグループ指定
```
ansible-playbook -i hosts -l <host,group> -t chatwork site.yml -e "chatwork=hogehoge"
```
