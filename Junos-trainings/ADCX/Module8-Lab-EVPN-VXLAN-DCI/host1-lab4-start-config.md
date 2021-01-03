```bash
lab@host1:~$ source lab4-start.sh 
[sudo] password for lab: 
Cannot find device "lag1"
Cannot find device "vlan.20"
copying interface configuration file

applying interface configuration file
ens4: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.1.1.1  netmask 255.255.255.0  broadcast 10.1.1.255
        inet6 fe80::5054:ff:fe5e:886a  prefixlen 64  scopeid 0x20<link>
        ether 52:54:00:5e:88:6a  txqueuelen 1000  (Ethernet)
        RX packets 79  bytes 4424 (4.4 KB)
        RX errors 235  dropped 0  overruns 0  frame 235
        TX packets 110  bytes 12368 (12.3 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

default via 172.25.11.254 dev ens3 proto static 
10.1.1.0/24 dev ens4 proto kernel scope link src 10.1.1.1 
10.1.2.0/24 via 10.1.1.254 dev ens4 proto static 
172.16.1.0/24 via 10.1.1.2 dev ens4 proto static 
172.25.11.0/24 dev ens3 proto kernel scope link src 172.25.11.21 
setup complete.
```

```bash
lab@host1:~$ cat lab4-start.sh 
#!/bin/bash
sudo ip link set ens4 down
sudo ip link set ens5 down
sudo ip link set lag1 down
sudo ip link set vlan.10 down
sudo ip link set vlan.20 down
cd /home/lab/
echo "copying interface configuration file"
sudo cp ./interface-configs/lab4-start.yaml /etc/netplan/network.yaml
sleep 2
echo "applying interface configuration file"
sudo netplan apply
sleep 2
ifconfig ens4
ip route
echo "setup complete."
lab@host1:~$
```

```yaml
lab@host1:~$ cat ./interface-configs/lab4-start.yaml 
# Lab 1 MC-LAG interface configuration for Host1
# Includes a bonded LAG interface on the host, with vlan trunking of VLANs 15 and 20
network:
        version: 2
        renderer: networkd
        ethernets:
                # Management interface to student workstation br-ext interface
                ens3:
                        dhcp4: no
                        addresses: [172.25.11.21/24]
                        gateway4: 172.25.11.254
                        nameservers:
                                addresses: [8.8.8.8, 8.8.4.4]
                ens4:
                        dhcp4: no
                        addresses: [10.1.1.1/24]
                        routes:
                                - to: 10.1.2.0/24
                                  via: 10.1.1.254
                                - to: 172.16.1.0/24
                                  via: 10.1.1.2

                ens5:
                        dhcp4: no

lab@host1:~$ 
```



