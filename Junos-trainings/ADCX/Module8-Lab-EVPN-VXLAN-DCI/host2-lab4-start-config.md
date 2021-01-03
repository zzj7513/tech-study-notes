```bash
lab@host2:~$ source lab4-start.sh 
[sudo] password for lab: 
Cannot find device "lag1"
Cannot find device "vlan.10"
Applying new interface configuration...
New interface configuration applied.
ens4: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.1.1.2  netmask 255.255.255.0  broadcast 10.1.1.255
        inet6 fe80::5054:ff:fe2c:4ba2  prefixlen 64  scopeid 0x20<link>
        ether 52:54:00:2c:4b:a2  txqueuelen 1000  (Ethernet)
        RX packets 799  bytes 47932 (47.9 KB)
        RX errors 809  dropped 0  overruns 0  frame 809
        TX packets 210  bytes 42296 (42.2 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

default via 172.25.11.254 dev ens3 proto static 
10.1.1.0/24 dev ens4 proto kernel scope link src 10.1.1.2 
172.25.11.0/24 dev ens3 proto kernel scope link src 172.25.11.22 
lab@host2:~$ 
```

```bash
lab@host2:~$ cat lab4-start.sh 
#!/bin/bash
sudo ip link set ens4 down
sudo ip link set ens5 down
sudo ip link set lag1 down
sudo ip link set vlan.20 down
sudo ip link set vlan.10 down
cd /home/lab/
sudo cp ./interface-configs/lab4-start.yaml /etc/netplan/network.yaml
echo 'Applying new interface configuration...'
sleep 5
sudo netplan apply
echo 'New interface configuration applied.'
sleep 5
ifconfig ens4
ip route
lab@host2:~$ 
```

```yaml
lab@host2:~$ cat ./interface-configs/lab4-start.yaml 
#Lab 4 EVPN interface configuration for Host2
network:
        version: 2
        renderer: networkd
        ethernets:
                # Management interface to student workstation br-ext interface
                ens3:
                        dhcp4: no
                        addresses: [172.25.11.22/24]
                        gateway4: 172.25.11.254
                        nameservers:
                                addresses: [8.8.8.8, 8.8.4.4]
                ens4:
                        dhcp4: no
                        addresses: [10.1.1.2/24]
                        routes:
                                - to : 10.1.1.0/24
                                  via : 10.1.2.254
                ens5:
                        dhcp4: no
lab@host2:~$
```

