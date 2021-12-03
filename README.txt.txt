nodes
******
available nodes are:
c0 h1 h2 h3 h4 h5 h6 h7 h8 s1 s2 s3 s4 s5 s6 s7

net
******
h1 h1-eth0:s3-eth2
h2 h2-eth0:s3-eth3
h3 h3-eth0:s4-eth2
h4 h4-eth0:s3-eth4
h5 h5-eth0:s6-eth2
h6 h6-eth0:s6-eth3
h7 h7-eth0:s7-eth2
h8 h8-eth0:s7-eth3
s1 lo:  s1-eth1:s2-eth1 s1-eth2:s5-eth1
s2 lo:  s2-eth1:s1-eth1 s2-eth2:s3-eth1 s2-eth3:s4-eth1
s3 lo:  s3-eth1:s2-eth2 s3-eth2:h1-eth0 s3-eth3:h2-eth0 s3-eth4:h4-eth0
s4 lo:  s4-eth1:s2-eth3 s4-eth2:h3-eth0
s5 lo:  s5-eth1:s1-eth2 s5-eth2:s6-eth1 s5-eth3:s7-eth1
s6 lo:  s6-eth1:s5-eth2 s6-eth2:h5-eth0 s6-eth3:h6-eth0
s7 lo:  s7-eth1:s5-eth3 s7-eth2:h7-eth0 s7-eth3:h8-eth0
c0

h7 ifconfig
******
h7-eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.0.7  netmask 255.0.0.0  broadcast 10.255.255.255
        inet6 fe80::101a:b3ff:fe1e:74be  prefixlen 64  scopeid 0x20<link>
        ether 12:1a:b3:1e:74:be  txqueuelen 1000  (Ethernet)
        RX packets 75  bytes 5706 (5.7 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 12  bytes 936 (936.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

Function call graph:
start switch
_handle_PacketIn() -> act_like_hub() -> resend_packet() -> send(msg)

h1 ping -c100 h2
avg/min/max/mdev: 1.698/3.323/13.564/1.548

h1 ping -c100 h8
min/avg/max/mdev: 10.613/16.014/30.790/3.511

h1 only has one switch in between itself and h2, where there are several hops between h1 and h8, having to go through switches s3, s2, 1, 5, 7

*** Iperf: testing TCP bandwidth between h1 and h2
*** Results: ['9.16 Mbits/sec', '10.8 Mbits/sec']

*** Iperf: testing TCP bandwidth between h1 and h8
*** Results: ['2.94 Mbits/sec', '3.48 Mbits/sec']



