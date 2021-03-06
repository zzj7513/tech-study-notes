```
set version 18.4R1.8
set system login user lab uid 2000
set system login user lab class super-user
set system login user lab authentication encrypted-password "$6$taWflV9u$jcqqSgeUfs/SW8jWwHP3fN5Gg3pqjuTAfIf8BJZSmgzCKG7ggJbNqkcgCK4dsg4CaZnGPNC2yjdLHCnxDOXKQ0"
set system root-authentication encrypted-password "$6$DOl8kJ4d$nYdxu7KyEiKudTHI5PG1jtZxe.xQXAdGDWqmaiwmxlyn2fyZwpHFvqLH/DB9h75Xf/FUL2HAyi4rkJHZ0H/UT/"
set system services ftp
set system services ssh
set system host-name leaf2
set system syslog user * any emergency
set system syslog file messages any notice
set system syslog file messages authorization info
set system syslog file interactive-commands interactive-commands any
set system extensions providers juniper license-type juniper deployment-scope commercial
set system extensions providers chef license-type juniper deployment-scope commercial
set chassis aggregated-devices ethernet device-count 2
set interfaces xe-0/0/0 unit 0 family ethernet-switching vlan members v10
set interfaces xe-0/0/1 unit 0 family inet address 172.16.1.9/31
set interfaces xe-0/0/2 unit 0 family inet address 172.16.1.3/31
set interfaces em0 unit 0 family inet address 172.25.11.4/24
set interfaces em1 unit 0 family inet address 169.254.0.2/24
set interfaces lo0 unit 0 family inet address 192.168.100.12/32
set forwarding-options storm-control-profiles default all
set policy-options policy-statement Export-Directs term Loopback-Interface from protocol direct
set policy-options policy-statement Export-Directs term Loopback-Interface from interface lo0.0
set policy-options policy-statement Export-Directs term Loopback-Interface then accept
set policy-options policy-statement Export-Directs term loopback from protocol direct
set policy-options policy-statement Export-Directs term loopback from route-filter 192.168.100.0/24 orlonger
set policy-options policy-statement Export-Directs term loopback then accept
set policy-options policy-statement Load-Balance-Policy term Load-Balance then load-balance per-packet
set policy-options policy-statement Load-Balance-Policy term Load-Balance then accept
set policy-options policy-statement Load-Balance-Policy term Load-Balance-Policy then load-balance per-packet
set policy-options policy-statement Load-Balance-Policy term Load-Balance-Policy then accept
set routing-options router-id 192.168.100.12
set routing-options autonomous-system 65000
set routing-options forwarding-table export Load-Balance-Policy
set protocols bgp group overlay type internal
set protocols bgp group overlay local-address 192.168.100.12
set protocols bgp group overlay family evpn signaling
set protocols bgp group overlay local-as 65000
set protocols bgp group overlay neighbor 192.168.100.1
set protocols bgp group overlay neighbor 192.168.100.2
set protocols bgp group underlay type external
set protocols bgp group underlay export Export-Directs
set protocols bgp group underlay local-as 65202
set protocols bgp group underlay multipath multiple-as
set protocols bgp group underlay neighbor 172.16.1.2 peer-as 65101
set protocols bgp group underlay neighbor 172.16.1.8 peer-as 65102
set protocols evpn encapsulation vxlan
set protocols evpn extended-vni-list all
set switch-options vtep-source-interface lo0.0
set switch-options route-distinguisher 192.168.100.12:1
set switch-options vrf-target target:65000:1
set switch-options vrf-target auto
set vlans default vlan-id 1
set vlans v10 vlan-id 10
set vlans v10 vxlan vni 5010
```

