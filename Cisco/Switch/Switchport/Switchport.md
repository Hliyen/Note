# Switchport #
## Switchport Trunk ##
    讓多個不同的 VLAN 流量，共用「同一條實體線路」進行傳輸，且彼此不會搞混。
    接交換器或路由器：用 Trunk 讓所有 VLAN 的流量一併通過。
### Trunking 參數配置 ###
    allowed  白名單過濾
    native   指定 Native VLAN
    pruning  動態廣播垃圾流量過濾器
### 配置方式 ###
    int e0/1
      switchport trunk encapsulation dot1q    ## 簡寫 sw tr en dot
      switchport mode trunk                   ## 簡寫 sw mo tr
## switchport access ##
    只能通過「1 個」指定的 VLAN
    另一端接的設備 : 電腦、印表機、伺服器、IP Cam
### 配置方式 ###
    int e0/1
      switchport mode access       ## 簡寫  sw mo acc
      switchport access vlan 10    ## 簡寫  sw acc vl 10
