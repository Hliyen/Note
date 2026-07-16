# Port Security #
## 功能 ##
>1.限制 MAC 位址的最大數量（Limit MAC Count）：

    可以規定「這個網路孔同時只能允許 1 個（或 3 個） MAC 位址通過」。
>2.鎖定特定 MAC 位址（MAC Binding）：

    可以手動指定，或自動指定 MAC（Sticky MAC）。只有這張網卡能用這個孔上網。
>3.違規懲罰機制（Violation Actions）：

    當非授權的設備插進來，或者來源 MAC 超過設定數量時，交換器可以執行三種不同程度的懲罰：
    ● Shutdown（預設、最常用）：直接把這個網路孔關閉斷電，必須由網管人員手動下指令才能重新啟用。
    ● Restrict（限制）：不關閉網路孔，只把非法的封包丟棄，並狂發報警訊息（Syslog/SNMP Trap）給網管人員，且違規計數器會一直累加。
    ● Protect（保護）：最溫和。直接丟棄非法封包，但「不關孔、不報警」，默默做事。

## 配置 ##
    int e0/0  #進入要套用的介面
    sw mo acc  #只能套用在 access 或 trunk
    sw port-sec #啟動 Port Security
    sw port-sec maximum 1  #限制最大允許的 MAC 數量為 1
    sw port-sec mac-address sticky  #讓交換器動態學習第一個 MAC 並寫入運行設定
    sw port-sec violation shutdown  #設定違反規則時的懲罰方式為 Shutdown
    
