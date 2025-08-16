[目次に戻る](./README.md) <br>

# ネットワーク機器監視設定と確認

##(今回監視する機器)<br>

NEC IX2025<br>
監視方式　　　：SNMPVer2<br>
監視IPアドレス：192.168.10.254<br>

##今回の構成
![Diagram](./images/Network-monitoring/1.jpg)<br>
NEC IX2025をSNMPVer2を使用してZabbixで監視できるようにします！<br>



## 実施要領

### １ NEC Univerge IXのテンプレートをZabbixにインポートする<br>
 Zabbixには標準でIXのテンプレートはインストールされていないのでインポートを実施<br>
 以下からZabbixのIX用テンプレートをダウンロードできます！<br>
 https://www.zabbix.com/integrations/nec<br>

![Diagram](./images/Network-monitoring/2.jpg)<br>

リンクをクリックするとZabbixさんのGithubにいくことができます！<br>
 https://github.com/zabbix/community-templates/tree/main/Network_Devices/template_nec_univerge_ix<br>

![Diagram](./images/Network-monitoring/3.jpg)<br>
![Diagram](./images/Network-monitoring/4.jpg)<br>
![Diagram](./images/Network-monitoring/5.jpg)<br>

上記のようにyamlファイルが該当のテンプレートなのでダウンロードします<br>

次にZabbixサーバーにログインして<br>

　ZabbixのWeb画面 → データ収集　→　テンプレート　→　インポートを選択<br>
![Diagram](./images/Network-monitoring/6.jpg)<br>
![Diagram](./images/Network-monitoring/7.jpg)<br>
![Diagram](./images/Network-monitoring/8.jpg)<br>

これでテンプレートがインポートできました！<br>

　テンプレート名はちなみに　”UNIVERSE　IX”　になります！<br>


### ２ NEC IX2025の設定<br>
 IXがSNMPに応答するようにエージェントの設定と、障害発生時にトラップを発生させるように設定<br>
![Diagram](./images/Network-monitoring/9.jpg)<br>

### ３ ZabbixにIX2215を登録します<br>
　(1) ホストグループの作成<br>
　　ネットワークデバイスのホストグループがなかったため、新規作成<br>
![Diagram](./images/Network-monitoring/10.jpg)<br>
![Diagram](./images/Network-monitoring/11.jpg)<br>
![Diagram](./images/Network-monitoring/12.jpg)<br>
　　
　(2) ホストの設定<br>
　　SNMPエージェントとしてNEC IX2025を登録<br>
　　(今回の条件）<BR>
　　名前<BR>
　　：　NEC-IX2215-1（任意の名前）<BR>
    テンプレート<BR>
　　：UNIVERSE IX<BR>
    ホストグループ
　　：NETWORK　DEVICE(先ほど作成したもの）<BR>
　　インタフェース<BR>
　　：SNMP　 192.168.10.254（NEC　IX2215のIPアドレス）<BR>
　　　　　　：SNMP Ver SNMPVer2<BR>
　　　　　　：SNMPコミュニティ gorosuke<BR>
　　　　　　
![Diagram](./images/Network-monitoring/13.jpg)<br>
![Diagram](./images/Network-monitoring/14.jpg)<br>
![Diagram](./images/Network-monitoring/15.jpg)<br>
![Diagram](./images/Network-monitoring/16.jpg)<br>
![Diagram](./images/Network-monitoring/17.jpg)<br>


### ４ NEC IX2215の監視確認<br>
　　NEC IX2215がSNMPで監視できているかを確認<br>
![Diagram](./images/Network-monitoring/18.jpg)<br>
![Diagram](./images/Network-monitoring/19.jpg)<br>
　　
　　
　　
### ５　グラフの作成及び確認<br>
   今回はGe0.0及びGe1.0のインタフェースの送受信ビット数のグラブを作成<br>
![Diagram](./images/Network-monitoring/20.jpg)<br>
![Diagram](./images/Network-monitoring/21.jpg)<br>
![Diagram](./images/Network-monitoring/22.jpg)<br>
![Diagram](./images/Network-monitoring/23.jpg)<br>
![Diagram](./images/Network-monitoring/24.jpg)<br>

正しくグラフが表示されるかを確認します<br>

NEC IX2025の対向に設置されているJuniper SRX100からIX2025のインタフェースに対してPINGを送信します！<br>

![Diagram](./images/Network-monitoring/25.jpg)<br>
![Diagram](./images/Network-monitoring/26.jpg)<br>
   
   
 
