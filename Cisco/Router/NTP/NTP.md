# NTP #
## 簡介 ##
    分為兩種模式:伺服器、客戶端
### 伺服器 ###
    為整個內部網路的「時間源頭」，所有其他設備都會向它看齊，以確保全網的日誌（Log）時間完全一致。
#### 配置方式 ####
    Router# clock set 00:00:00 1 Jan 2026  #手動調整系統時間
    Router(config)# ntp master [層級]  #層級範圍 1~15，層級越大權限越高  
### 客戶端 ###
    部署在附屬設備中，定期向 NTP 伺服器發送請求。
#### 配置方式 ####
    Router(config)# ntp server [NTP server IP]
