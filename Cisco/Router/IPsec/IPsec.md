# IPsec #
## 配置方式 ##
### RA ###
    crypto isakmp policy 10
    encryption aes
    hash sha256
    authentication pre-share
    group 14
    crypto isakmp key vpnuser address 10.0.0.2
    crypto ipsec transform-set myset esp-aes esp-sha256-hmac
    access-list 100 permit ip 10.1.1.0 0.0.0.255 172.16.2.0 0.0.0.255
    crypto map mymap 10 ipsec-isakmp
      set peer 10.0.0.2
      set transform-set myset
      match address 100
    interface GigabitEthernet0/1
      ip address 10.1.1.2 255.255.255.0
    interface GigabitEthernet0/0
      ip address 172.16.1.1 255.255.255.0
      crypto map mymap
      ip route 0.0.0.0 0.0.0.0 172.16.1.2
    end
    sh cry ip sa
    sh cry map
    sh cry ses re det
### RB ###
    crypto isakmp policy 10
    encryption aes
    hash sha256
    authentication pre-share
    group 14
    crypto isakmp key vpnuser address 172.16.1.1
    access-list 100 permit ip 172.16.2.0 0.0.0.255 10.1.1.0 0.0.0.255
    crypto map mymap 10 ipsec-isakmp
      set peer 172.16.1.1
      set transform-set myset
      match address 100
    interface Gt0/1
      ip address 172.16.2.1 255.255.255.0
    interface GigabitEthernet0/0
      ip address 10.0.0.2 255.255.255.0
      crypto map mymap
    ip route 0.0.0.0 0.0.0.0 10.0.01
    end
    sh cry ip sa
    sh cry map
    sh cry ses re det
