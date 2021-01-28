```markdown
set version 18.4R1.8
set system login user lab uid 2000
set system login user lab class super-user
set system login user lab authentication encrypted-password "$6$p1EvX0QF$/pcFXCImB/Rli3M1EJOrwQXQU1135kwDRvHDr7NmBUjaTsTRQroIuqIH/rsFUe1/9KXGH11yBP.J3nIf6lzNp1"
set system root-authentication encrypted-password "$6$NA38MaaO$.dfkxopTvjvGumOcpgVnbBHzJuWR61iVLI3Zg3SNq/p/KZUd/1kfPY.k/XL49QVB4VycYoyR9NO26E/SGz1F31"
set system services ftp
set system services ssh
set system host-name spine2
set system syslog file messages any notice
set system syslog file messages authorization info
set system syslog file interactive-commands interactive-commands any
set system extensions providers juniper license-type juniper deployment-scope commercial
set system extensions providers chef license-type juniper deployment-scope commercial
set interfaces xe-0/0/0 unit 0 family inet address 172.16.1.38/30
set interfaces xe-0/0/1 unit 0 family inet address 172.16.1.6/31
set interfaces xe-0/0/2 unit 0 family inet address 172.16.1.8/31
set interfaces xe-0/0/3 unit 0 family inet address 172.16.1.10/31
set interfaces em0 unit 0 family inet address 172.25.11.2/24
set interfaces em1 unit 0 family inet address 169.254.0.2/24
set interfaces irb unit 10 virtual-gateway-accept-data
set interfaces irb unit 10 family inet address 10.1.1.102/24 virtual-gateway-address 10.1.1.254
set interfaces lo0 unit 0 family inet address 192.168.100.2/32
set forwarding-options storm-control-profiles default all
set policy-options policy-statement Export-Directs term loopback from protocol direct
set policy-options policy-statement Export-Directs term loopback from route-filter 192.168.100.0/
24 orlonger
set policy-options policy-statement Export-Directs term loopback then accept
set policy-options policy-statement Load-Balance-Policy term Load-Balance-Policy then load-balance per-packet
set policy-options policy-statement Load-Balance-Policy term Load-Balance-Policy then accept
set routing-options router-id 192.168.100.2
set routing-options autonomous-system 65000
set routing-options forwarding-table export Load-Balance-Policy
set protocols bgp group underlay type external
set protocols bgp group underlay export Export-Directs
set protocols bgp group underlay local-as 65102
set protocols bgp group underlay multipath multiple-as
set protocols bgp group underlay neighbor 172.16.1.11 peer-as 65203
set protocols bgp group overlay type internal
set protocols bgp group overlay local-address 192.168.100.2
set protocols bgp group overlay family evpn signaling
set protocols bgp group overlay cluster 2.2.2.2
set protocols bgp group overlay local-as 65000
set protocols bgp group overlay neighbor 192.168.100.13
set protocols evpn encapsulation vxlan
set protocols evpn extended-vni-list all
set switch-options vtep-source-interface lo0.0
set switch-options route-distinguisher 192.168.100.2:1
set switch-options vrf-target target:65000:1
set switch-options vrf-target auto
set vlans default vlan-id 1
set vlans v10 vlan-id 10
set vlans v10 l3-interface irb.10
set vlans v10 vxlan vni 5010


```

