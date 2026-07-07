  # NAT PAT #
## 簡介 ##
    NAT 一對一，PAT 多對一
## NAT(Network Address Translation，網路位址轉換) ##
    一個私有 IP 在連出外網時，必須獨佔一個公有 IP，因此公司內部有 100 台電腦想同時上網，就必須購買 100 個公有 IP。
    常用於企業內部的伺服器（如 Web Server、Mail Server）。為了讓外網的使用者能透過固定的公有 IP 存取內部伺服器，會做一對一的固定對應。
### Static NAT ###
#### 應用環境 ####
    當內部網路有架設伺服器，就必須使用靜態 NAT。因為外網的使用者必須知道一個固定的公有 IP，才能準確連到該伺服器。
#### 配置方式 ####
    1. 建立一對一的固定對應關係
      ip nat inside source static [本機私有IP] [對應轉換的公有IP]
    2. 套用到介面上
      interface Ethernet0/1
        ip nat inside   ! 連接內部私網的介面
        exit
      interface Ethernet0/0
        ip nat outside  ! 連接外部公網的介面
        exit
### Dynamic NAT ###
#### 應用環境: 早期特定環境（現已不常用）####
    會向電信商（ISP）購買「一整池（Pool）」的公有 IP，當內部電腦要上網時，路由器會從池子裡隨機撈一個沒人用的公有 IP 配給它，斷線後再回收。
    如果池子裡只有 5 個公有 IP，那同時就只能有 5 台內網電腦上網，第 6 台會被擋下來。由於無法真正解決 IP 短缺問題，且成本高昂，目前在實際企業環境中已經極少單獨使用。
#### 配置方式 ####
    A：綁定在「外部介面」的 IP（最常部署於家庭或小型辦公室，如動態取得的 IP）
    
      1. 定義允許上網的內網範圍
        ip nat my_pool [POOL起始IP] [POOL結束IP] netmask [目的地遮罩]
      2. 直接轉換為外部介面 (Ethernet0/0) 的 IP，關鍵字在於最後必須加上 overload
        ip nat inside source list 1 int E0/0 overload
      3. 指定介面方向
        interface Ethernet0/1
          ip nat inside
          exit
        interface Ethernet0/0
          ip nat outside
          exit

    B：綁定在「特定的公有 IP 池」（常用於中大型企業，擁有多個固定公有 IP）
          ip nat my_pool [POOL起始IP] [POOL結束IP] natmask [目的地遮罩]
          access-list 1 permit [ACL要匹配的網路位置] [ACL專用的反向遮罩]
          ip nat inside source list 1 pool COMP_POOL overload
