# DHCP #
## 簡介 ##
    每台設備都需要一個IP才可與其他設備進行通訊，若是一間教室有30台電腦，要手動配置30個IP太過於麻煩，所以通常會於網路設備上配置DHCP，讓設備自動配發IP，降低管理難度
### 配置方式 ###
    ip dhcp excluded-address [排除的起始IP] [排除的結束IP]  #排除保留區
    ip dhcp pool [自訂名稱]  #建立dhcp pool
    network [配置的IP] [配置的子網路遮罩]   #配置網段
    default-router [預設閘道IP]   #配置預設閘道
    dns-server 8.8.8.8  #DNS
    domain-name Cisco.com #域名，可寫可不寫
    lease 0 8 #租約時間，天，小時，預設為1天
