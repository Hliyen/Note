# SSH #
## 介紹 ##
>配置 SSH是為了解決傳統 Telnet 協定的缺陷——明文傳輸。使用 Telnet 遠端登入路由器時，密碼和輸入的指令在網路上都是完全透明的，極易被竊聽；而 SSH 會將所有的連線流量進行高強度加密，確保遠端管理的安全。
### 配置方式 ###
    ip domain-name [自定網域名城] #設定網域名稱
    username [使用者名稱] password [密碼]  #設定使用者名稱及密碼
    crypto key generate rsa #產生RSA加密金鑰
    line vty 0 4  #進入虛擬終端線路（VTY），指引連線的通行規則
      transport input ssh  #限制去向：只允許 SSH
      login local  #限制身分：強制使用上面建立的本機帳密
