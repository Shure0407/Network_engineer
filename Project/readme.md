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
