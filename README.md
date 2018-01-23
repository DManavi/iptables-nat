# NAT via iptables in linux

sudo iptables -A FORWARD -i eth0 -o eth1 -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

sudo iptables -A FORWARD -i eth1 -o eth0 -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

sudo iptables -P FORWARD DROP






sudo iptables -A FORWARD -i eth0 -o eth1 -p (tcp,udp) --syn --dport (1234,15000:15100) -m conntrack --ctstate NEW -j ACCEPT

sudo iptables -t nat -A PREROUTING -i eth0 -p (tcp,udp) --dport (1234,15000:15100) -j DNAT --to-destination (target ip e.g. 10.195.84.40)

sudo iptables -t nat -A POSTROUTING -o eth1 -p (tcp,udp) --dport (1234,15000:15100) -d (target ip e.g. 10.195.84.40) -j SNAT --to-source (source ip (eth0 ip) 10.195.84.1)
