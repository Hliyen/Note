# EtherChannel #
## 簡介 ##

## 靜態(Static)/無協定 ##
    設定為靜態，這個介面就會強行被加入 port-channel [編號]。他不會去管其他東西。
### 指令 ###
    channel-group [編號] mode on
## LACP(Link Aggregation Control Protocol) ##
    設定為動態，會主動發送LACP的協商封包，需要對面設定active/passive。不能雙方都是passive。
### 指令 ###
    #主動
    channel-group [編號] mode active
    #被動
    channel-group [編號] mode passive
    
