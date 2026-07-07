  # NAT PAT #
## 簡介 ##
    NAT 一對一，PAT 多對一
### NAT(Network Address Translation，網路位址轉換) ###
    一個私有 IP 在連出外網時，必須獨佔一個公有 IP，因此公司內部有 100 台電腦想同時上網，就必須購買 100 個公有 IP。
    常用於企業內部的伺服器（如 Web Server、Mail Server）。為了讓外網的使用者能透過固定的公有 IP 存取內部伺服器，會做一對一的固定對應。
#### Static NAT ####
    #應用環境
        當內部網路有架設伺服器，就必須使用靜態 NAT。因為外網的使用者必須知道一個固定的公有 IP，才能準確連到該伺服器。
    #配置方式
        1. 建立一對一的固定對應關係
          ip nat inside source static 10.1.1.100 203.0.113.100

        2. 套用到介面上
          interface Ethernet0/1
            ip nat inside   ! 連接內部私網的介面
            exit
          interface Ethernet0/0
            ip nat outside  ! 連接外部公網的介面
            exit
