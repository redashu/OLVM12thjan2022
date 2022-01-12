# A little understanding about VIrtualization 

<img src="vm1.png">

## Intro to Hypervisor 

<img src="hyper.png">

## TYpe 2 Hypervisor 

<img src="t2.png">

## TYpe 1 Hypervisor 

<img src="t1.png">

## Hypervisors 

<img src="hy.png">

## Checking virtualization features 

<img src="vir.png">

### The real Ovirt COmmunity 

[Ovirt Docs](https://www.ovirt.org/)

### Ovirt for RHVM / OLVM 

<img src="ovrt.png">

### OL virtaulization manager

<img src="olvm1.png">

### KVM \ Libvirt | cockpit 

<img src="cockpit.png">

### CHecking things before we install KVM -- ON OL8 

### Checking RAM -- Recommended is 8GB 
```
 free  -m
              total        used        free      shared  buff/cache   available
Mem:          29803         575       28197           8        1030       28819
Swap:          8191           0        8191

```

### Checking CPU support 
```
lscpu 
Architecture:        x86_64
CPU op-mode(s):      32-bit, 64-bit
Byte Order:          Little Endian
CPU(s):              4
On-line CPU(s) list: 0-3
Thread(s) per core:  2
Core(s) per socket:  2
Socket(s):           1
NUMA node(s):        1
Vendor ID:           GenuineIntel
BIOS Vendor ID:      QEMU
CPU family:          6
Model:               85
Model name:          Intel(R) Xeon(R) Platinum 8167M CPU @ 2.00GHz
BIOS Model name:     pc-i440fx-4.2
Stepping:            4
CPU MHz:             1995.312
BogoMIPS:            3990.62
Virtualization:      VT-x
Hypervisor vendor:   KVM
Virtualization type: full
L1d cache:           32K

```

### Checking cpu support 

<img src="cpu.png">

### Installing KVM with Libvirt 

```
 20  dnf  install  qemu-kvm  
   21  history 
   22  yum  install qemu-kvm 
   23  yum  install  libvirt
   24  history 
[root@ol8host1 ~]# systemctl  status libvirtd
● libvirtd.service - Virtualization daemon
   Loaded: loaded (/usr/lib/systemd/system/libvirtd.service; enabled; vendor preset: enabled)
   Active: inactive (dead)
     Docs: man:libvirtd(8)
           https://libvirt.org
[root@ol8host1 ~]# systemctl  start libvirtd
[root@ol8host1 ~]# systemctl  enable libvirtd
[root@ol8host1 ~]# systemctl  status libvirtd
● libvirtd.service - Virtualization daemon
   Loaded: loaded (/usr/lib/systemd/system/libvirtd.service; enabled; vendor preset: enabled)
   Active: active (running) since Wed 2022-01-12 05:43:53 GMT; 13s ago
     Docs: man:libvirtd(8)
           https://libvirt.org
 Main PID: 44202 (libvirtd)
    Tasks: 19 (limit: 32768)
```

### Network interface with DHCP by KVM 

```
# ifconfig
ens3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 9000
        inet 10.0.0.148  netmask 255.255.255.0  broadcast 10.0.0.255
        inet6 fe80::17ff:fe0d:182c  prefixlen 64  scopeid 0x20<link>
        ether 02:00:17:0d:18:2c  txqueuelen 1000  (Ethernet)
        RX packets 18539  bytes 238737178 (227.6 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 13976  bytes 3050850 (2.9 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 306  bytes 21501 (20.9 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 306  bytes 21501 (20.9 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
        ether 52:54:00:18:f3:50  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)


```

### Some storage root and conf files by KVM with LIbvirt 

```
 cd  /var/lib/libvirt/
[root@ol8host1 libvirt]# ls
boot  dnsmasq  filesystems  images  network  qemu  swtpm
[root@ol8host1 libvirt]# 
[root@ol8host1 libvirt]# 
[root@ol8host1 libvirt]# cd  /etc/libvirt/
[root@ol8host1 libvirt]# ls
libvirt-admin.conf  nwfilter         qemu.conf            virtlockd.conf     virtnodedevd.conf   virtqemud.conf
libvirt.conf        qemu             secrets              virtlogd.conf      virtnwfilterd.conf  virtsecretd.conf
libvirtd.conf       qemu-lockd.conf  virtinterfaced.conf  virtnetworkd.conf  virtproxyd.conf     virtstoraged.conf
[root@ol8host1 libvirt]# 

```
