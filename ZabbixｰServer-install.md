[目次に戻る](./README.md) <br>

# Zabbixサーバーのインストールと確認

## (今回実施したOS条件)<br>
### 仮想化環境：VirtualBOX
    仮想マシン　OS：Ubuntu22　　メモリー：4096Ｍ　CPU：２　　　gorosuke/root123
　  Webサーバ(Apache）
　　PHP：Ver8.1及びPHP-fpm
　　DBサーバ：MariaDB
　　Zabbixバージョン:Zabbix Ver7
　　
## 今回の構成
![Diagram](./images/Zabbix install/1.jpg)<br>
VirtualBOX上に構成したUbuntuにZabbixサーバーをインストールします！<br>


## 実施手順
　　
(1)　Ubuntuをアップデートします。
(2)　Apache2をインストール&設定します。
(3)　MariaDBのインストール&設定します。
(4)　PHPとPHP-fpmのインストール&設定します。
(5)　Zabbixのインストールします。
(6)　ZabbixのWebインタフェースにアクセスし、設定します。
(7)　ZabbixのWebインタフェースにアクセスし、ログインします。
(8)　Zabbixのステータスを確認します。

参考サイト
Ubuntu22.04にZabbix7を構築
https://falconblog.org/zabbix-construct-v1/


## 事前準備
　Ubuntuのキーボード配列を英語キーボード→日本語キーボードに変更しておきます
　![Diagram](./images/Zabbix install/2.jpg)<br>

## 実施手順
　(1)　Ubuntuをアップデートします。<br>
　![Diagram](./images/Zabbix install/3.jpg)<br>
　 インターネットに接続した状態で以下のコマンドを実行します!<br>
　 　#apt updateコマンド,#apt autoremoveを実行します！<br>
　 ![Diagram](./images/Zabbix install/3.jpg)<br>
　 ![Diagram](./images/Zabbix install/4.jpg)<br>
　 
　 (2)　Apache2をインストール&設定します。<br>
　  インターネットに接続した状態で以下のコマンドを実行します!<br>
　  #apt install apache2
　  ![Diagram](./images/Zabbix install/4.jpg)<br>
　  インストール後、起動確認でUbuntuのマシンからブラウザでApache2の起動確認を実施します
　  　http://localhost
　  ![Diagram](./images/Zabbix install/5.jpg)<br>
　  
　  (3)　MariaDBのインストール&設定します。
　   ①　インストール<br>
　   #apt install mariadb-serverを実行します!<br>
　  ![Diagram](./images/Zabbix install/6.jpg)<br>
　  
　   ②　設定ファイルの確認<br>
　   #nano /etc/mysql/mariadb.conf.d/50-server.conf<br>
　   ![Diagram](./images/Zabbix install/7.jpg)<br>
　   
　   図のように90行目:(Character-set-server)は デフォルトの文字コードを確認する<br>
     # 絵文字等 4バイト文字を扱うにはutf8mb4にしておく<br>
     
     ③　MariaDBを再起動後、インストール作業を実施<br>
     # mysql_secure_installation<br>
     ![Diagram](./images/Zabbix install/7.jpg)<br>
     
     ④　PHPとPHP-fpmのインストール&設定します。<br>
     ア　PHP及びPHP-fpmのインストール<br>
      #apt install php8.1 php8.1-mbstring php-pear<br>
     ![Diagram](./images/Zabbix install/8.jpg)<br>
     
     イ　インストール完了後、PHPのバージョン情報を確認します<br>
     #php -v<br>
     ![Diagram](./images/Zabbix install/10.jpg)<br>
     
     ウ　インストール後、PHPの設定情報をブラウザで確認できるようにします。<br>
     ![Diagram](./images/Zabbix install/11.jpg)<br>
     ![Diagram](./images/Zabbix install/11.jpg)<br>
     (参考）PHPの設定情報をコマンドでも確認が可能です！<br>
     
     エ　PHP-fpmをインストールします。<br>
     
     関連してApacheの連携モジュールもインストールします<br>
     #a2emod proxy_fcgi setenvif<br>
     #a2emod php8.1-fpm<br>
     
     設定後、再度、PHPの設定情報をブラウザで確認できるようにします。<br>
     
     (4)  
     
     (5)　Zabbixのインストール<br>
       Wgetコマンドを使用してZabbixをダウンロードします<br>
     　　![Diagram](./images/Zabbix install/15.jpg)<br>
     　dpkgコマンドによるZabbixの展開<br>
     　　![Diagram](./images/Zabbix install/16.jpg)<br>
     　Zabbixで使用する関連ファイルをダウンロード<br>
     　　![Diagram](./images/Zabbix install/17.jpg)<br>
     　DB（MariaDB）にログイン及び設定<br>
     　　![Diagram](./images/Zabbix install/18.jpg)<br>
     　Zabbixの初期データベース構築<br>
     　（Zabbix が動作するのに必要なテーブルや初期データが作成される）<br>
     　　![Diagram](./images/Zabbix install/19.jpg)<br>
     　DB（MariaDB）にログイン及び設定変更<br>
     　　![Diagram](./images/Zabbix install/20.jpg)<br>
     　Zabbix側のDB接続設定を実施<br>
     　　![Diagram](./images/Zabbix install/21.jpg)<br>
     　　![Diagram](./images/Zabbix install/22.jpg)<br>
     　　![Diagram](./images/Zabbix install/23.jpg)<br>
     　Zabbixサーバの再起動及び有効化<br>
     　　![Diagram](./images/Zabbix install/24.jpg)<br>
     　Zabbixエージェントの設定変更及びエージェント再起動<br>
     　　![Diagram](./images/Zabbix install/25.jpg)<br>
     　PHP8.1のFPM関連ファイルの設定<br>
     　　![Diagram](./images/Zabbix install/25.jpg)<br>
     　　ZabbixのWebインタフェースにアクセスし、確認します<br>
     　　![Diagram](./images/Zabbix install/25.jpg)<br>
     　　データベースの接続設定を実施します<br>
     　　![Diagram](./images/Zabbix install/26.jpg)<br>
     　　サーバ名、タイムゾーン等を設定します。

