# ICMP_Ping_status_counts.xtemplates
監視中のicmppingの総計・OK/NGのカウントをするTemplateです。
テンプレート中でZabbixAPIにアクセスしているので下記のマクロを設定しておく必要があります。
または書き換えてください。

{$HA_IP_ADDRESS} => APIアクセス先のZabbixサーバのIP及びポート番号 ipaddress:port  
{$API_KEY} => APIのアクセスキー

licenseはMITです。

## このテンプレートを必要としている人が試すであろうコード
計算item  
```
count(last_foreach(/*/icmpping,0,"eq"))
count(last_foreach(/*/icmpping?[value="0"]))
```  
　→集計関数のcount、last_foreachにはlastvalueと比較する機能はありません(Zabbix6.4)  
   
Zabbix API
```json
{
  "jsonrpc": "2.0",
  "method": "item.get",
  "params": {
    "output": ["lastvalue"],
    "monitored": true,
    "countOutput": true,
    "search": {
      "name": "ICMP ping",
      "key_": "icmpping"
    },
    "filter": {
       "lastvalue":["eq","0"]
    }
  },
  "auth": "{{auth_key}}",
  "id": 1
}
```
　→ filterにはlastvalueと比較する機能はありません(Zabbix6.4)
