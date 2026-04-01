# Iptables



```bash
sudo iptables -t nat -A PREROUTING -p tcp --dport PORT -j DNAT --to-destination HOST:PORT
sudo iptables -t nat -A POSTROUTING -p tcp -d HOST --dport 443 -j MASQUERADE
sudo iptables -A FORWARD -p tcp -d HOST --dport 443 -j ACCEPT
```
