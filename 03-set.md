 1: Команда `Ip a` – показывает сетевые интерфейсы системы, их состояние, MAC-адреса и назначенные IP-адреса.
```
 lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
```
В нашем случае при вводе данной команды был обнаружен интерфейс  <LOOPBACK,UP,LOWER_UP>, его состояние <UNKNOWN>?
С IP адресом 192.168.248.255 и IPv4 адрес 127.0.0.1/8.

 2: `Ip r` – Команда показывает таблицу маршрутизации ОС.
Здесь используются шлюзы, они нужны для передачи пакетов в сети которые не входят в вашу локальную подсеть ВМ.
```
ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 00:0c:29:59:51:42 brd ff:ff:ff:ff:ff:ff
    altname enp3s0
    altname enx000c29595142
    inet 192.168.248.137/24 brd 192.168.248.255 scope global dynamic noprefixroute ens160
       valid_lft 1408sec preferred_lft 1408sec
    inet6 fe80::8d66:54f1:8181:2684/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever
```
Шлюз: 192.168.248.255

 3: Команда `cat /etc/resolv.conf` используется для проверки параметров доменных имён. 
```
default via 192.168.248.2 dev ens160 proto dhcp src 192.168.248.137 metric 20100 
192.168.248.0/24 dev ens160 proto kernel scope link src 192.168.248.137 metric 100 
```
IP адрес компьютера 192.168.248.137, подключён он к сети 192.168.248.0/24, а для доступа к другим сетям использует шлюз 192.168.248.2.

 4: Команда `ping -c 4 8.8.8.8` использовалась для проверки доступности узла по IP адресу. 
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=128 time=75.1 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=128 time=75.8 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=128 time=75.2 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=128 time=74.6 ms

--- 8.8.8.8 ping statistics ---

4 packets transmitted, 4 received, 0% packet loss, time 2998ms
rtt min/avg/max/mdev = 74.647/75.179/75.806/0.412 ms
```
В результате ввода данной команды отправлено 4 пакета, вот пример 1 пакета : 64 bytes from 8.8.8.8: icmp_seq=1 ttl=128 time=75.1 ms, в выводе написано, icmp_seq=1, 1 это номер запроса, сам icmp запрос это сообщение,которым проверяется доступен ли другой пк/сервер,или нет. TTL(Time To Live) запрос, значение 128 используется виндовс системами,но это не означает что устройство работает на винде. time=75.1 ms это то сколько было затрачено времени в мс туда и обратно. 

 5: Комнада `ping -c 4 ya.ru` используется для проверки связи с узлом по доменному имени.
```
PING ya.ru (77.88.44.242) 56(84) bytes of data.
64 bytes from ya.ru (77.88.44.242): icmp_seq=1 ttl=128 time=54.6 ms
64 bytes from ya.ru (77.88.44.242): icmp_seq=2 ttl=128 time=54.7 ms
64 bytes from ya.ru (77.88.44.242): icmp_seq=3 ttl=128 time=55.5 ms
64 bytes from ya.ru (77.88.44.242): icmp_seq=4 ttl=128 time=55.3 ms

--- ya.ru ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 2997ms
rtt min/avg/max/mdev = 54.596/55.036/55.519/0.394 ms
```
 в результате использования данной команды мы получили вот что: PING ya.ru (77.88.44.242), потери пакетов составили 0%. icmp_seq=1 ttl=128 time=54.6 ms, в выводе написано, icmp_seq=1, 1 это номер запроса, сам icmp запрос это сообщение,которым проверяется доступен ли другой пк/сервер,или нет. TTL(Time To Live) запрос, значение 128 используется виндовс системами,но это не означает что устройство работает на винде. time=54.6 ms это то сколько было затрачено времени в мс туда и обратно. Сервер ya.ru доступен.
 
 6: Команда `ss -tulpn` показывает сетевые соеденения, открытые порты пк. 
```
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
```
в выводе данной команде работают службы DNS, mDNS, LLMNR, NTP и печати, а так же открыт TCP порт 27500. DNS преобразует имена сайтов в IP адреса, mDNS позволяет находить устройства и службы в локальной сети без обычного DNS, LLMNR как обычный DNS, но исп для поиска имён в локальной сети, NTP исп для синхронизации времени в пк, TCP используется для передачт данных с установлением соеденения.
``` 
This is /run/systemd/resolve/stub-resolv.conf managed by man:systemd-resolved(8).
nameserver 127.0.0.53
options edns0 trust-ad
search localdomain
```

