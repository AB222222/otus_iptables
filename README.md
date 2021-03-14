# otus_iptables

Всё работает, вроде бы.

## Port knocking на первый маршрутизатор

```
me@me-HP-260-G3-DM:~/otus-linux/DZ_FIREWALL_IPTABLES$ vagrant ssh centralRouter
[vagrant@centralRouter ~]$ ssh 192.168.255.1 -l vagrant
^C
[vagrant@centralRouter ~]$ knock 192.168.255.1 8881 7777 9991 -d 1000
[vagrant@centralRouter ~]$ ssh 192.168.255.1 -l vagrant
The authenticity of host '192.168.255.1 (192.168.255.1)' can't be established.
ECDSA key fingerprint is SHA256:DsFNDU4XgppfGPewuF3ZXax9Apjk5POJXH+fCvSz7o4.
ECDSA key fingerprint is MD5:da:90:fe:f3:ab:5c:4c:26:dc:d8:4f:23:37:26:ce:93.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '192.168.255.1' (ECDSA) to the list of known hosts.
vagrant@192.168.255.1's password:
[vagrant@inetRouter ~]$
 
```

## Проброс порта через второй маршрутизатор

```
me@me-HP-260-G3-DM:~$ curl -I localhost:1234
HTTP/1.1 200 OK
Server: nginx/1.16.1
Date: Sun, 14 Mar 2021 10:03:16 GMT
Content-Type: text/html
Content-Length: 4833
Last-Modified: Fri, 16 May 2014 15:12:48 GMT
Connection: keep-alive
ETag: "53762af0-12e1"
Accept-Ranges: bytes

me@me-HP-260-G3-DM:~$ 
 
```

## Default router через первый маршрутизатор

```
me@me-HP-260-G3-DM:~/otus-linux/DZ_FIREWALL_IPTABLES$ vagrant ssh inetRouter2
[vagrant@inetRouter2 ~]$ traceroute ya.ru
traceroute to ya.ru (87.250.250.242), 30 hops max, 60 byte packets
 1  gateway (192.168.255.1)  1.371 ms  1.113 ms  0.968 ms
 2  * * *
 3  * * *
 4  95-165-128-1.static.spd-mgts.ru (95.165.128.1)  4.796 ms  7.875 ms  11.397 ms
 5  mpts-a197-51.msk.mts-internet.net (212.188.1.106)  10.691 ms  10.076 ms  8.913 ms
 6  a197-cr04-be12.51.msk.mts-internet.net (212.188.1.105)  8.155 ms  7.804 ms  6.192 ms
 7  212.188.33.199 (212.188.33.199)  6.376 ms  7.873 ms  6.581 ms
 8  ya.ru (87.250.250.242)  13.289 ms 10.4.3.1 (10.4.3.1)  12.847 ms *
[vagrant@inetRouter2 ~]$ 

```

