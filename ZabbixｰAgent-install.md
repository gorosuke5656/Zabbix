[目次に戻る](./Junos-BGP-exercises.md) <br>

# Zabbix-agentのインストールと確認

##(今回実施したOS条件)<br>

仮想マシン<br>
OS：Ubuntu22<br>
Zabbix-agent Ver：Zabbix agent6.4<br>

##今回の構成
![Diagram](./images/zabbix-agent/1.jpg),br>
VirtualBOX上に構成したZabbix-agentをZabbixサーバーから監視できる状態にします<br>

## 実施要領
###【ダウンロード&展開&インストール】<br>　　
　(1) Zabbixサイトから該当のZabbixエージェントのdebファイルをダウンロード<br>
　(2) dpkgコマンドにより展開します<br>
　(3) apt installコマンドによりインストールを実施します<br>

###【設定ファイルの修正及びエージェント有効化】<br>
  (1) Zabbix-agent2のconfig(/etc/zabbix/zabbix_agent2.conf)を修正します<br>
　(2) Zabbix-agent2の再起動及び有効化を実施します<br>

###【Zabbixサーバによる設定及び確認】
　(1）WebUIにログイン後、データ収集→ホストを選択します<br>
　(2) ホストの作成を選択/設定します<br>
　(3) 作成したホストのAvailabilityが緑色になることを確認します<br>
　(4) Zabbix-agent2をインストールした端末で状態を確認します<br>


##　細部手順及び確認
###【ダウンロード&展開&インストール】<br>　　
　(1) Zabbixサイトから該当のZabbixエージェントのdebファイルをダウンロード<br>
wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb<br>

　　 ![Diagram](./images/zabbix-agent/2.jpg)<br>

　(2) dpkgコマンドにより展開します<br>

　　 ![Diagram](./images/zabbix-agent/3.jpg)<br>

　(3) apt installコマンドによりインストールを実施します<br>　
　
　　![Diagram](./images/zabbix-agent/4.jpg)<br>
　　![Diagram](./images/zabbix-agent/5.jpg)<br>
　　　
###【設定ファイルの修正及びエージェント有効化】<br>
(1) Zabbix-agent2のconfig(/etc/zabbix/zabbix_agent2.conf)を修正します<br>

　　![Diagram](./images/zabbix-agent/6.jpg)<br>
　　![Diagram](./images/zabbix-agent/7.jpg)<br>
　　　
(2) Zabbix-agent2の再起動及び有効化を実施します<br>
    #systemctl restart zabbix-agent2（再起動）<br>
    #systemctl enable zabbix-agent2 （有効化）<br>
    
    ![Diagram](./images/zabbix-agent/8.jpg)<br>
　　　
###【Zabbixサーバによる設定及び確認】
(1）WebUIにログイン後、データ収集→ホストを選択します<br>
　　![Diagram](./images/zabbix-agent/9.jpg)<br>
　　　
(2) ホストの作成を選択/設定します<br>
　　![Diagram](./images/zabbix-agent/10.jpg)<br>
　　![Diagram](./images/zabbix-agent/11.jpg)<br>
　　![Diagram](./images/zabbix-agent/12.jpg)<br>
　　![Diagram](./images/zabbix-agent/13.jpg)<br>
　　![Diagram](./images/zabbix-agent/14.jpg)<br>
　　![Diagram](./images/zabbix-agent/15.jpg)<br>
　　![Diagram](./images/zabbix-agent/16.jpg)<br>
　　
(3) 作成したホストのAvailabilityが緑色になることを確認します<br>
　　![Diagram](./images/zabbix-agent/17.jpg)<br>
　　![Diagram](./images/zabbix-agent/18.jpg)<br>
　　
(4) Zabbix-agent2をインストールした端末で状態を確認します<br>
    ![Diagram](./images/zabbix-agent/19.jpg)<br>
   
　　
　　　
　
　　　

　　　








