## Router config


**Core Router**
hostname CORE-ROUTER
ipv6 unicast-routing

interface g0/0
 ipv6 address 2026:BB23:22CD:10::1/64
 ipv6 ospf 1 area 0
 no shutdown

interface g0/1
 ipv6 address 2026:BB23:22CD:30::1/64
 ipv6 ospf 1 area 0
 no shutdown


**Access Control(Security)**
ipv6 access-list NO_WEB_TO_INTERNET
 permit icmp any any
 deny tcp any any eq www
 deny tcp any any eq 443
 permit ipv6 any any


**Internal Router**
hostname INTERNAL-ROUTER
ipv6 unicast-routing

interface g0/0
 ipv6 address 2026:BB23:22CD:60::2/64
 ipv6 ospf 1 area 0
 no shutdown


**ISP Router**
hostname ISP-ROUTER
ipv6 unicast-routing

interface g0/0
 ipv6 address 2026:BB23:22CD:90::1/64
 no shutdown


**Core Router Configuration Command**
Router> enable
Router# configure terminal
Router(config)# hostname CORE-ROUTER
CORE-ROUTER(config)# ipv6 unicast-routing
CORE-ROUTER(config)# interface gigabitEthernet0/0
CORE-ROUTER(config-if)# no shutdown
CORE-ROUTER(config-if)# ipv6 address 2026:BB23:22CD:10::1/64
CORE-ROUTER(config-if)# ipv6 ospf 1 area 0
CORE-ROUTER(config-if)# exit
CORE-ROUTER(config)# interface gigabitEthernet0/1
CORE-ROUTER(config-if)# no shutdown
CORE-ROUTER(config-if)# ipv6 address 2026:BB23:22CD:30::1/64
CORE-ROUTER(config-if)# ipv6 ospf 1 area 0
CORE-ROUTER(config-if)# exit
CORE-ROUTER(config)# interface gigabitEthernet0/2
CORE-ROUTER(config-if)# no shutdown
CORE-ROUTER(config-if)# ipv6 address 2026:BB23:22CD:60::1/64
CORE-ROUTER(config-if)# ipv6 ospf 1 area 0
CORE-ROUTER(config-if)# exit
CORE-ROUTER(config)# interface serial0/1/1
CORE-ROUTER(config-if)# no shutdown
CORE-ROUTER(config-if)# clock rate 64000
CORE-ROUTER(config-if)# ipv6 address 2026:BB23:22CD:100::1/64
CORE-ROUTER(config-if)# ipv6 ospf 1 area 0
CORE-ROUTER(config-if)# exit
CORE-ROUTER(config)# ipv6 router ospf 1
CORE-ROUTER(config-rtr)# router-id 1.1.1.1
CORE-ROUTER(config-rtr)# exit
CORE-ROUTER(config)# end
CORE-ROUTER# write


**ACCESS CONTROL**
CORE-ROUTER#configure terminal
Enter configuration commands, one per line. End with CNTL/Z.
CORE-ROUTER(config)#ipv6 access-list No_WEB_TO_INTERNET
CORE-ROUTER(config-ipv6-acl)#permit icmp any any
CORE-ROUTER(config-ipv6-acl)#deny tcp any any eq www
CORE-ROUTER(config-ipv6-acl)#deny tcp any any eq www
CORE-ROUTER(config-ipv6-acl)#deny tcp any any eq 443
CORE-ROUTER(config-ipv6-acl)#permit ipv6 any any
CORE-ROUTER(config-ipv6-acl)#exit
CORE-ROUTER(config)#interface serial 0/1/1
CORE-ROUTER(config-if)#ipv6 traffic-filter NO_WEB_TO_INTERNET out
CORE-ROUTER(config-if)#exit
CORE-ROUTER(config)#interface serial 0/1/0
CORE-ROUTER(config-if)#ipv6 traffic-filter NO_WEB_TO_INTERNET out
CORE-ROUTER(config-if)#exit
CORE-ROUTER(config)#end
CORE-ROUTER#
%SYS-5-CONFIG_I: Configured from console by console
CORE-ROUTER#write memory
Building configuration...
[OK]
CORE-ROUTER#


**Internal Router Configuration Command**
Router> enable
Router# configure terminal
Router(config)# hostname Internal-Router
Internal-Router(config)# ipv6 unicast-routing
Internal-Router(config)# interface serial0/1/0
Internal-Router(config-if)# no shutdown
Internal-Router(config-if)# ipv6 address 2026:BB23:22CD:100::2/64
Internal-Router(config-if)# ipv6 ospf 1 area 0
Internal-Router(config-if)# exit
Internal-Router(config)# interface gigabitEthernet0/0
Internal-Router(config-if)# no shutdown
Internal-Router(config-if)# ipv6 address 2026:BB23:22CD:60::2/64
Internal-Router(config-if)# ipv6 ospf 1 area 0
Internal-Router(config-if)# exit
Internal-Router(config)# interface gigabitEthernet0/1
Internal-Router(config-if)# no shutdown
Internal-Router(config-if)# ipv6 address 2026:BB23:22CD:200::1/64
Internal-Router(config-if)# ipv6 ospf 1 area 0
Internal-Router(config-if)# exit
Internal-Router(config)# interface gigabitEthernet0/2
Internal-Router(config-if)# no shutdown
Internal-Router(config-if)# ipv6 address 2026:BB23:22CD:210::1/64
Internal-Router(config-if)# ipv6 ospf 1 area 0
Internal-Router(config-if)# exit
Internal-Router(config)# ipv6 router ospf 1
Internal-Router(config-rtr)# router-id 2.2.2.2
Internal-Router(config-rtr)# exit
Internal-Router(config)# end
Internal-Router# write


**ISP Router Configuration Command**
Router> enable
Router# configure terminal
Router(config)# hostname ISP-Router
ISP-Router(config)# ipv6 unicast-routing
ISP-Router(config)# interface serial0/1/0
ISP-Router(config-if)# no shutdown
ISP-Router(config-if)# ipv6 address 2026:BB23:22CD:80::1/64
ISP-Router(config-if)# exit
ISP-Router(config)# interface gigabitEthernet0/0
ISP-Router(config-if)# no shutdown
ISP-Router(config-if)# ipv6 address 2026:BB23:22CD:90::1/64
ISP-Router(config-if)# exit
ISP-Router(config)# end
ISP-Router# write

















