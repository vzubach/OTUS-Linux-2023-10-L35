### OTUS-Linux-2023-10-L35 | DNS

В репозитории Vagrantfile и необходимое окружение ansible для установки и настройки двух DNS-серверов и двух клиентов для проверки.  
Работоспособность разрешения имён, по отдельным для каждого клиента зонам, ниже:  

Клиент1 - видит обе зоны, но в зоне dns.lab только web1

		[root@client ~]# ping -c 2 www.newdns.lab
		PING www.newdns.lab (192.168.50.15) 56(84) bytes of data.
		64 bytes from client (192.168.50.15): icmp_seq=1 ttl=64 time=0.008 ms
		64 bytes from client (192.168.50.15): icmp_seq=2 ttl=64 time=0.018 ms
		
		--- www.newdns.lab ping statistics ---
		2 packets transmitted, 2 received, 0% packet loss, time 1001ms
		rtt min/avg/max/mdev = 0.008/0.013/0.018/0.005 ms
		[root@client ~]# 
		[root@client ~]# ping -c 2 web1.dns.lab
		PING web1.dns.lab (192.168.50.15) 56(84) bytes of data.
		64 bytes from client (192.168.50.15): icmp_seq=1 ttl=64 time=0.007 ms
		64 bytes from client (192.168.50.15): icmp_seq=2 ttl=64 time=0.019 ms
		
		--- web1.dns.lab ping statistics ---
		2 packets transmitted, 2 received, 0% packet loss, time 1001ms
		rtt min/avg/max/mdev = 0.007/0.013/0.019/0.006 ms
		[root@client ~]# 
		[root@client ~]# 
		[root@client ~]# ping -c 2 web2.dns.lab
		ping: web2.dns.lab: Name or service not known
		[root@client ~]#

Клиент2 видит только зону dns.lab:

		[root@client2 ~]# ping -c 2 www.newdns.lab
		ping: www.newdns.lab: Name or service not known
		[root@client2 ~]# 
		[root@client2 ~]# 
		[root@client2 ~]# ping -c 2 web1.dns.lab
		PING web1.dns.lab (192.168.50.15) 56(84) bytes of data.
		64 bytes from 192.168.50.15 (192.168.50.15): icmp_seq=1 ttl=64 time=0.984 ms
		64 bytes from 192.168.50.15 (192.168.50.15): icmp_seq=2 ttl=64 time=0.500 ms
		
		--- web1.dns.lab ping statistics ---
		2 packets transmitted, 2 received, 0% packet loss, time 1001ms
		rtt min/avg/max/mdev = 0.500/0.742/0.984/0.242 ms
		[root@client2 ~]# 
		[root@client2 ~]# 
		[root@client2 ~]# ping -c 2 web2.dns.lab
		PING web2.dns.lab (192.168.50.16) 56(84) bytes of data.
		64 bytes from client2 (192.168.50.16): icmp_seq=1 ttl=64 time=0.019 ms
		64 bytes from client2 (192.168.50.16): icmp_seq=2 ttl=64 time=0.018 ms
		
		--- web2.dns.lab ping statistics ---
		2 packets transmitted, 2 received, 0% packet loss, time 1002ms
		rtt min/avg/max/mdev = 0.018/0.018/0.019/0.004 ms
		[root@client2 ~]# 

