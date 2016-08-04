# 网络

### 获取当前服务器的公网IP
* 浏览器访问 
    - ifconfig.me
    - www.ip138.com
* Shell 命令
    - `curl -s ifconfig.me`
    - `curl -s members.3322.org/dyndns/getip`

### 查看当前服务器网络情况
* ping （网络层协议）
    - 使用[ICMP](https://www.wikiwand.com/zh-hans/%E4%BA%92%E8%81%94%E7%BD%91%E6%8E%A7%E5%88%B6%E6%B6%88%E6%81%AF%E5%8D%8F%E8%AE%AE) 协议 Internet Control Message Protocol
    - ping 无法检查系统端口是否开放。
* telnet 协议 （应用层协议）
    - 使用TCP 协议