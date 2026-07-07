# ACL #
## 建立群組 ##
    ip access-list [型態] [名稱]
## 限制僅允許 VLAN 200 上的 PC2 對 PC1 進行 ping
    permit icmp host [來源] host [目的地] echo
## 只允許 VLAN 200 上的 PC2 對 Sw101 進行 telnet
    permit tcp host [來源] host [目的地] eq telnet
## 防止 VLAN 200 上的所有其他設備進行 telnet
    deny tcp [整個VLAN 200 網段] host [SW IP] eq telnet
## 允許 VLAN 200 上的所有其他網路流量
    permit ip any any
## 允許BOOTP和HTTPS ##
    permit udp any any eq bootps  #BOOTP 伺服器端流量：bootps (或寫 67)
    permit udp any any eq bootpc  #BOOTP 客戶端流量：bootpc (或寫 68)
    permit tcp any any eq 443  #HTTPS 門牌號：443
## 限制所有其他流量，並記錄入口介面、來源 MAC 位址、封包的來源和目的地 IP 位址以及連接埠 ##
    deny any any log-inout
## 套用到Vlan 路口 ##
    int vl [自定數字]
        ip access-group [自定名稱] in
