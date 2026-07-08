# DHCP Snooping(DHCP 監聽) #
>如果有多個DHCP同時發放IP，導致機器無法順利拿到真正的IP，DHCP Snooping 的出現，就是為了在交換器（Switch）上築起一道防火牆，防止拿到錯誤的IP
## 配置方式 ##
    ip dhcp snooping  #啟用 DHCP Snooping
    ip dhcp snooping vlan 10  #指定要在哪些 VLAN 啟用這項安全機制
    int e0/0
      ip dncp snooping trust  #配置為可信賴介面
    int ra e0/2-5
      ip dhcp snooping limit rate 15  #配置不可信賴介面(限制速率，防止惡意癱瘓)
## 重要觀念 ##
>沒有在 e0/2-5 輸入任何不信任的指令，因為輸入了「ip dhcp snooping 」和「ip dhcp snooping vlan 10」，交換器就會極端地把所有接口預設轉為 Untrusted。所以我們只需要特地去把 e0/0 撈出來宣告 trust 即可
