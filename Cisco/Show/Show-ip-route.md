# Show-ip-route #
## directly connected ##
    10.10.10.0/30 is directly connected, F0/1
    代表 10.10.10.0/30 這個網段在 F0/1 介面上。
## 左側 C O B ##
    路由來源代碼
    C (Connected)： 直連網段
    O (OSPF) : 這條路由是透過 OSPF 動態路由協定 從別台路由器自動學習過來的
    B (BGP) : 這條路由是透過 BGP（Border Gateway Protocol，邊界閘道協定） 學習過來的
## [110/2576] ##
    [110/2576]
    [管理距離(AD)/成本度量值(Metric)]
    AD : 
      用來評估「這個路由來源可不可信」（數字越小越可信）。
      110：代表這條路由來自 OSPF（Cisco 預設 OSPF 的 AD 為 110）。
      20：代表這條路由來自 eBGP（External BGP 預設的 AD 為 20）。
    Metric :
      用來評估「走這條路要付出多少代價/有多遠」（數字越小越近、速度越快）。
      6576 或 110：代表 OSPF 計算出來的路徑 Cost 值（通常由頻寬大小計算而得）。
      0：BGP 的 Metric (MED) 值。
  ## O  10.10.13.144/28 [110/110] via 10.10.10.1 ##
     [O]  [10.10.13.144/28] [110/110] [via 10.10.10.1]
     [透過 OSPF學到的] [目的地網段] [AD/Metric] [next hop(下一跳)]
      
