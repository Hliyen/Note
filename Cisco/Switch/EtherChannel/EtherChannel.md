# EtherChannel #
## 簡介 ##
>避免STP誤封網路線，導致4=1，明明接了4條線，使用起來和1條線沒什麼差別。
    
## 靜態(Static)/無協定 ##
>設定為靜態，這個介面就會強行被加入 port-channel [編號]。不會去管對面是如何設定，也不會發送任何確認封包。
    
### 指令 ###
    channel-group [編號] mode on
    
## LACP(Link Aggregation Control Protocol) ##
>設定為動態，會主動發送LACP的協商封包，需要對面設定active/passive。不能雙方都是passive。
    
### 指令 ###
    #主動
    channel-group [編號] mode active
    #被動
    channel-group [編號] mode passive
    
## 好處 ##
### 頻寬加倍 ###
>如果一條網路線是1Gbps，綁了4條，兩台交換機之間的總頻寬就會提升到4Gbps。不用花錢去買10G的網卡或模組，用現有的線路就能直接升級頻寬。

### 負載平衡 ###
>交換機會依據流量的來源/目的MAC或IP，將封包平均分配到這4條線上傳輸，確保每一條都有被充分利用。

### 高可用性與容錯 ###
>如果有線路斷了或port壞了，流量會瞬間自動轉移到剩下的線路上，網路完全不會中斷。
