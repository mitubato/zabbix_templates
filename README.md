# ICMP_Ping_status_counts.xtemplates
監視中のicmppingの総計・OK/NGのカウントをするTemplateです。
テンプレート中でZabbixAPIにアクセスしているので下記のマクロを設定しておく必要があります。
または書き換えてください。

{$HA_IP_ADDRESS} => APIアクセス先のZabbixサーバのIP及びポート番号 ipaddress:port  
{$API_KEY} => APIのアクセスキー

licenseはMITです。
