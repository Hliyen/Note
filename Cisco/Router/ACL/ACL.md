# ACL（Access Control List，存取控制清單） #
## 應用地方 ##
    1.流量過濾
    2.配合NAT/PAT選擇上網流量
    3.配合策略路由(PBR)
    4.保護設備遠端連線(VTY安全)
## Standard ACL(標準ACL)
>檢查對象:只看來源IP地址

>缺點: 權力太粗暴。如果用標準 ACL 擋掉某個 IP，那台電腦就什麼事都不能做了。

>編號範圍:1-99 或 1300-1999
## Extended ACL (擴充ACL)
>檢查對象: 可以同時檢查 來源 IP、目的 IP、協定類型（TCP/UDP/ICMP）以及通訊埠（Port）

>優點: 控制極度精準。例如：可以做到「允許電腦 A 瀏覽網頁（Port 80/443），但禁止電腦 A 使用 FTP（Port 21）」。

>編號範圍: 100-199 或 2000-2699
## ACL 運作的黃金三大鐵律 ##
### 由上到下，依序匹配 ###
>路由器會從第一條規則開始往下看，只要一匹配成功，立刻執行（放行或丟棄），後面剩下的規則直接跳過不看。因此，最精準的規則要寫在最上面，範圍大的寫在下面。
### 末尾隱含拒絕所有（Implicit Deny All）
>每張 ACL 的最後一行，系統都自動藏了一條「拒絕所有人」的隱形規則。如果你整張 ACL 只寫了 deny 192.168.1.1，那這張 ACL 掛上去後，全公司所有人都會斷網（因為沒被你 deny 的人，最後都被隱形規則 deny 了）。所以最後通常要補上一條放行所有人的指令。
### 方向性 ###
>ACL 必須應用在路由器的接口上，且要區分 Inbound（流量流進接口） 或 Outbound（流量流出接口）。
## 範例 ##
    在 Sw101 上配置並應用一個單一的 NACL，使用以下設定：
    ● 名稱：ENT_ACL
    ● 限制僅允許 VLAN 200 上的 PC2 對 PC1 進行 ping
    ● 只允許 VLAN 200 上的 PC2 對 Sw101 進行 telnet
    ● 防止 VLAN 200 上的所有其他設備進行 telnet
    ● 允許 VLAN 200 上的所有其他網路流量
### 建立d擴充ACL ###    
    ip access-list [型態] [名稱]
    ip access-list extanded ENT_ACL
### 限制僅允許 VLAN 200 上的 PC2 對 PC1 進行 ping ###
    permit icmp host [來源] host [目的地]
    permit icmp host 192.168.200.10 host 192.168.100.10
### 只允許 VLAN 200 上的 PC2 對 Sw101 進行 telnet ###
    permit tcp host [來源] host [目的地] eq telnet
    permit tcp host 192.168.200.10 host 192.168.100.1 eq telnet
### 防止 VLAN 200 上的所有其他設備進行 telnet ###
    deny tcp [整個VLAN 200 網段] host [目的地] eq telnet
    deny tcp 192.168.200.0 0.0.0.255 host any eq telnet 
### 允許 VLAN 200 上的所有其他網路流量 ###
    permit ip any any
## 允許BOOTP和HTTPS ##
    permit udp any any eq bootps  #BOOTP 伺服器端流量：bootps (或寫 67)
    permit udp any any eq bootpc  #BOOTP 客戶端流量：bootpc (或寫 68)
    permit tcp any any eq 443  #HTTPS 門牌號：443
## 限制所有其他流量，並記錄入口介面、來源 MAC 位址、封包的來源和目的地 IP 位址以及連接埠 ##
    deny any any log-input
## 套用到Vlan 路口 ##
    int vl [自定數字]
        ip access-group [自定名稱] in
