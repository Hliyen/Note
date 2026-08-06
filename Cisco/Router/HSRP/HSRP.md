# HSRP 熱備援冗餘協定 #
## 功能 ##
### 閘道高可用性（High Availability, HA） ###
    提供第一跳路由器備援（FHRP）。底下電腦的 Gateway 填寫 HSRP 的「虛擬 IP（Virtual IP）」，當主要路由器（Active）斷線時，備用路由器（Standby）會在數秒內接管該虛擬 IP 與 MAC 位址。
### 終端設備「無感切換」 ###
    電腦、伺服器或印表機不需要安裝任何軟體，也不需要修改 IP / Gateway 設定，甚至下載到一半的封包也不會連線中斷。
### 主動搶佔（Preempt）與狀態回歸 ###
    主要路由器修復重啟後，可以設定自動「搶回」Active 身份，讓網路流量回到原本的最佳路徑。
### 介面追蹤與主動降級（Interface Tracking） ###
    不僅能監控路由器本體是否死機，還能監控「對外 WAN 口」是否斷線。如果連外線路斷了，HSRP 會自動降低優先度（Priority），主動將 Gateway 角色讓給另一台 WAN 口正常的路由器。
### 搭配多 VLAN 實現簡易負載平衡（Load Sharing） ###
    讓 Router A 擔任 VLAN 10 的 Active、VLAN 20 的 Standby；Router B 則相反。這樣兩台設備平時能各自分擔流量，壞掉時又能互相備援。
## 配置方式 ##
### R1 ###
    R1(config)# interface Vlan11
    R1(config-if)# ip address 10.1.11.2 255.255.255.0
    R1(config-if)# standby 11 ip 10.1.11.1           !<-- 1. 指定 HSRP 群組號碼(11)與虛擬 IP
    R1(config-if)# standby 11 priority 110          !<-- 2. 提高優先度，爭取成為 Active (預設 100)
    R1(config-if)# standby 11 preempt               !<-- 3. 開啟搶佔，修好開機後自動拿回權力
    R1(config-if)# standby 11 track Ethernet0/0 20  !<-- 4. (選配) 追蹤 WAN 口，若 e0/0 斷線優先度減 20
    R1(config-if)# no shutdown
### R2 ###
    R2(config)# interface Vlan11
    R2(config-if)# ip address 10.1.11.3 255.255.255.0
    R2(config-if)# standby 11 ip 10.1.11.1           !<-- 群組號碼與虛擬 IP 必須與 R1 一致
    R2(config-if)# standby 11 preempt
    R2(config-if)# no shutdown
### show ###
    show standby brief
    
