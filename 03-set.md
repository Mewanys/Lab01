1: Команда 'Ip a' – показывает сетевые интерфейсы системы, их состояние, MAC-адреса и назначенные IP-адреса.
В нашем случае при вводе данной команды был обнаружен интерфейс  <LOOPBACK,UP,LOWER_UP>, его состояние <UNKNOWN>?
С IP адресом 192.168.248.255 и IPv4 адрес 127.0.0.1/8.

 lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
       
2: Ip r – Команда показывает таблицу маршрутизации ОС.
Здесь используются шлюзы, они нужны для передачи пакетов в сети которые не входят в вашу локальную подсеть ВМ.
Шлюз: 192.168.248.255

ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:59:51:42 brd ff:ff:ff:ff:ff:ff
    altname enp3s0
    altname enx000c29595142
    inet 192.168.248.137/24 brd 192.168.248.255 scope global dynamic noprefixroute ens160
       valid_lft 1408sec preferred_lft 1408sec
    inet6 fe80::8d66:54f1:8181:2684/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
       
3: Команда cat /etc/resolv.conf используется для проверки параметров разрешённых доменных имён:

default via 192.168.248.2 dev ens160 proto dhcp src 192.168.248.137 metric 20100 
192.168.248.0/24 dev ens160 proto kernel scope link src 192.168.248.137 metric 100 

4: Команда ping -c 4 8.8.8.8 использовалась для проверки доступности узла по IP адресу. В результате ввода данной команды отправлено 4 пакета:

PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=128 time=75.1 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=128 time=75.8 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=128 time=75.2 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=128 time=74.6 ms

--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2998ms
rtt min/avg/max/mdev = 74.647/75.179/75.806/0.412 ms

5: Комнада ping -c 4 ya.ru используется для проверки связи с узлом по доменному имени, в результате использования данной команды мы получили вот что: PING ya.ru (77.88.44.242), потери пакетов составили 0%.

PING ya.ru (77.88.44.242) 56(84) bytes of data.
64 bytes from ya.ru (77.88.44.242): icmp_seq=1 ttl=128 time=54.6 ms
64 bytes from ya.ru (77.88.44.242): icmp_seq=2 ttl=128 time=54.7 ms
64 bytes from ya.ru (77.88.44.242): icmp_seq=3 ttl=128 time=55.5 ms
64 bytes from ya.ru (77.88.44.242): icmp_seq=4 ttl=128 time=55.3 ms

--- ya.ru ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2997ms
rtt min/avg/max/mdev = 54.596/55.036/55.519/0.394 ms

6: Команда ss -tulpn показывает сетевые сокеты,протоколы,локальные адреса и порты, в нашем случае мы получили:

Netid State  Recv-Q Send-Q   Local Address:Port    Peer Address:Port Process 
udp   UNCONN 0      0              0.0.0.0:5353         0.0.0.0:*            
udp   UNCONN 0      0              0.0.0.0:5355         0.0.0.0:*            
udp   UNCONN 0      0           127.0.0.54:53           0.0.0.0:*            
udp   UNCONN 0      0        127.0.0.53%lo:53           0.0.0.0:*            
udp   UNCONN 0      0            127.0.0.1:323          0.0.0.0:*            
udp   UNCONN 0      0                 [::]:5353            [::]:*            
udp   UNCONN 0      0                 [::]:5355            [::]:*            
udp   UNCONN 0      0                [::1]:323             [::]:*            
tcp   LISTEN 0      4096        127.0.0.54:53           0.0.0.0:*            
tcp   LISTEN 0      4096           0.0.0.0:5355         0.0.0.0:*            
tcp   LISTEN 0      4096         127.0.0.1:631          0.0.0.0:*            
tcp   LISTEN 0      10             0.0.0.0:27500        0.0.0.0:*            
tcp   LISTEN 0      4096     127.0.0.53%lo:53           0.0.0.0:*            
tcp   LISTEN 0      4096              [::]:5355            [::]:*            
tcp   LISTEN 0      4096             [::1]:631             [::]:*            

This is /run/systemd/resolve/stub-resolv.conf managed by man:systemd-resolved(8).
# Do not edit.
#
# This file might be symlinked as /etc/resolv.conf. If you're looking at
# /etc/resolv.conf and seeing this text, you have followed the symlink.
#
# This is a dynamic resolv.conf file for connecting local clients to the
# internal DNS stub resolver of systemd-resolved. This file lists all
# configured search domains.
#
# Run "resolvectl status" to see details about the uplink DNS servers
# currently in use.
#
# Third party programs should typically not access this file directly, but only
# through the symlink at /etc/resolv.conf. To manage man:resolv.conf(5) in a
# different way, replace this symlink by a static file or a different symlink.
#
# See man:systemd-resolved.service(8) for details about the supported modes of
# operation for /etc/resolv.conf.

nameserver 127.0.0.53
options edns0 trust-ad
search localdomain

