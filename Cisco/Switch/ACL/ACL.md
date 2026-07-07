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
