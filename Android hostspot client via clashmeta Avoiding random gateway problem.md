# 任意机器使用安卓热点并且使用固定的代理地址配置

## 解决的痛点
- 多数android手机的热点是随机的网关地址,甚至dhcp段
- Vpn hotspot 神器需要root, 但是不能root
- root机器使用vpnhotspot 和adguard的严格防火墙策略冲突

## 实现的效果
任意客户端连接热点的时候,配置一次代理地址, 后续都不需要配置,默认直接走clashmeta. 

## 面向的使用者
+ adguard + clash/mihomo 组合的重度用户
+ 热点机是安卓, 想要客户端免配置使用clash

## 步骤
### clashmeta 
settings-->override--->general
mixed port 设置 1134 (可自定义)
Allow Lan 设置 Enabled
Bind Address 设置 0.0.0.0

### adguard (只需确认)
settings --> general -->Advanced-->low level settings-->Local Vpn settings-->IPv4 address
确认为 172.18.11.218 , 不是的话就自己修改.

### 连接热点
该机器打开自带的热点,
客户端连接这个热点的时候 proxy 设置 172.18.11.218 端口1134

## 总结
借用adguard本来就会创建tun, 实现客户端使用这个tun ip代替随机的网关ip.

并且clashmeta监听0.0.0.0覆盖了所有网卡ip,所以端口使用1134 就连到了clashmeta
