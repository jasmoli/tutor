# DNS
![DNS](../../assets/20231007232941235.jpg)

Option explanation:

| Option | Explain |
| :---- | :---- |
| DNS 服务器 | DNS server configuration list |
| DNS 规则 | in development |
| fakeip | in development |
| DNS 配置 | in development |

![DNS服务器](../../assets/23231007232958.jpg)

![新增DNS服务器](../../assets/20231007233008821.jpg)

**DNS 服务器** option explanation:

| Option | Explain |
| :---- | :---- |
| 新增 DNS 服务器 | Add DNS server configuration |
| 启用 DNS 服务器 | Check Enable current DNS server configuration |
| DNS 服务器名称 | DNS configuration name |
| DNS 服务器地址 | DNS server address, such as **8.8.8.8**, **https://1.12.12.12/dns-query **, **local**, etc. |
| DNS 服务器出站 | Specifies that outbound uses the current DNS configuration |
| 结果偏好 | Five options in total，**使用全局配置**、**优先4代**、**优先6代**、**仅4代**、**仅6代**，Correspond to **global configuration** respectively、**prefer_ipv4**、**prefer_ipv6**、**only_ipv4**、**only_ipv4**。 |
| DNS 服务器地址解析器 | DNS 地址（域名地址）解析的 DNS 配置，或者说，套娃解析？ |
| DNS 服务器解析偏好 | Used when resolving the current DNS configuration address. There are five options in total,**使用全局配置**、**优先 ipv4**、**优先 ipv6**、**仅 ipv4**、**仅 ipv6**，Correspond to **global configuration** respectively、**prefer_ipv4**、**prefer_ipv6**（IPv6 优先）、**only_ipv4**、**only_ipv4**。 |
| 备注 | Current configuration notes |
