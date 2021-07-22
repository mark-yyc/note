#### 记录一些常用的shell指令

+ service --status-all 查看所有服务
+ netstat -ano | grep (关键字)

端口转发：将外网的某个端口访问转发到内网的某个端口

```bash
sysctl net.ipv4.ip_forward=1
iptables -t nat -A PREROUTING -p tcp -d 10.0.0.10 --dport 30551 -j DNAT --to-destination 10.0.0.10:31793
iptables -t nat -A POSTROUTING -j MASQUERADE
```

+ sudo scutil --set HostName localhost 修改主机名字