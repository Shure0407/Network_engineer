```bush
SW3(config-if-range)#int range f0/3-4
SW3(config-if-range)#sh

%LINK-5-CHANGED: Interface FastEthernet0/3, changed state to administratively down
%LINK-5-CHANGED: Interface FastEthernet0/4, changed state to administratively down

SW3(config-if-range)#channel-group 4 mode active
SW3(config-if-range)#
Creating a port-channel interface Port-channel 4

(config-if-range)#int po 4
SW3(config-if)#sw m tr
SW3(config-if)#sw tr allowed vlan 10,20,50,100
SW3(config-if)#sw tr native vlan 200
SW3(config-if)#exit
SW3(config)#int range f0/3-4
SW3(config-if-range)#no sh
SW3(config-if-range)#
%LINK-5-CHANGED: Interface FastEthernet0/3, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/3, changed state to up
%LINK-5-CHANGED: Interface FastEthernet0/4, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/4, changed state to up
%LINK-5-CHANGED: Interface Port-channel4, changed state to up
%LINEPROTO-5-UPDOWN: Line protocol on Interface Port-channel4, changed state to up
```

```
R3#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R3(config)#ip dhcp excluded-address 10.0.110.1 10.0.110.10
R3(config)#ip dhcp excluded-address 10.0.110.100 10.0.110.255
R3(config)#ip routing
R3(config)#ip dhcp pool Vlan110
R3(dhcp-config)#network 10.0.110.0 255.255.255.0
R3(dhcp-config)#default-router 10.0.110.243   
R3(dhcp-config)#exit
```
```bush
R2#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R2(config)#int g0/0/1
R2(config-if)#standby version 2
R2(config-if)#int g0/0/1.10
R2(config-subif)#standby 1 ip 10.0.10.242
R2(config-subif)#standby 1 priority 200
R2(config-subif)#standby 1 preempt
R2(config-subif)#
R2(config-subif)#int g0/0/1.20
R2(config-subif)#standby 2 ip 10.0.20.242
R2(config-subif)#standby 2 priority 200
R2(config-subif)#standby 2 preempt
R2(config-subif)#
R2(config-subif)#int g0/0/1.100
R2(config-subif)#standby 3 ip 10.0.100.242
R2(config-subif)#standby 3 priority 200
R2(config-subif)#standby 3 preempt
R2(config-subif)#
R2(config-subif)#int g0/0/1.80
R2(config-subif)#standby 4 ip 10.0.80.242
R2(config-subif)#standby 4 priority 200
R2(config-subif)#standby 4 preempt
R2(config-subif)#exit
R2(config)#int g0/0/1
R2(config-if)#no sh
```

```
R2(config)#int g0/0/1.100
R2(config-subif)#ip nat inside
R2(config-subif)#int g0/0/1.10
R2(config-subif)#ip nat inside
R2(config-subif)#int g0/0/1.20
R2(config-subif)#ip nat inside
R2(config-subif)#int g0/0/0
R2(config-if)#ip nat outside
R2(config-if)#ip access-list standard FOR_NAT
R2(config-std-nacl)#permit 10.0.10.0 0.0.0.255
R2(config-std-nacl)#permit 10.0.100.0 0.0.0.255
R2(config-std-nacl)#permit 10.0.20.0 0.0.0.255
R2(config-std-nacl)#exit
R2(config)#ip nat inside source list FOR_NAT interface GigabitEthernet0/0/0 overload
R2(config)#int g0/0/0
R2(config-if)#ip add 156.156.1.2 255.255.255.252
R2(config-if)#no sh
```

```
R4(config)#crypto isakmp policy 1
R4(config-isakmp)#encryption 3des
R4(config-isakmp)#hash md5
R4(config-isakmp)#authentication pre-share 
R4(config-isakmp)#group 2
R4(config-isakmp)#exit
R4(config)#crypto isakmp key cisco address 156.156.1.2
R4(config)#crypto ipsec transform-set TS esp-3des esp-md5-hmac
R4(config)#ip access-list extended FOR_VPN
R4(config-ext-nacl)#permit ip 10.0.30.0 0.0.0.255 10.0.80.0 0.0.0.254
R4(config-ext-nacl)#permit ip 10.0.40.0 0.0.0.255 10.0.80.0 0.0.0.254
R4(config-ext-nacl)#exit
R4(config)#crypto map CMAP 10 ipsec-isakmp 
% NOTE: This new crypto map will remain disabled until a peer
        and a valid access list have been configured.
R4(config-crypto-map)#set peer 156.156.1.2
R4(config-crypto-map)#set transform-set TS
R4(config-crypto-map)#match address FOR_VPN
R4(config-crypto-map)#exit
R4(config)#int g0/0/0
R4(config-if)#crypto map CMAP
*Jan  3 07:16:26.785: %CRYPTO-6-ISAKMP_ON_OFF: ISAKMP is ON




