---
comments: true
---
![](../../assets/20231007232750279.jpg)

## 选项解释

| 名称 | 解释 |
| :---- | :---- |
| 网络订阅 | Airport network subscription, obtain node information from the airport server |
| 本地文件 | Local node files are generally used to build self-built nodes and avoid streaming. The file storage location is located at `/data/adb/sfm/src/FileProviders/`, which can now be modified through the panel without opening the directory. |
| 修改文件 | Modify the local node file. For details on the syntax, see [Local node file writing method] (#Local node file writing method) |
| 订阅链接 | Subscription link, recommended Clash subscription |
| 可否被引用 | Whether to enable this outbound provider, enabling means using this subscription. Miao Lao's original words: "(Not enabled) will not be added to the configuration file at all." |
| 订阅拉取间隔 | How often to update the airport subscription, the default is 3600, which is one hour |
| 拉取订阅时查询订阅信息 | Check airport traffic and usage status |
| 修改提供者内出站设置 | The following are all modification requests, used to avoid streaming, and will not be introduced. |

## How to write local node files
  - One node per line

For example：
```
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIkBTU1JTVUItVjE1LeS7mOi0ueaOqOiNkDpzdW8ueXQvc3Nyc3ViIiwNCiAgImFkZCI6ICJqcDQuYWY0OWM0ZTRjMmVmLnNhbmZlbjAwNC5tZSIsDQogICJwb3J0IjogIjQ0MyIsDQogICJpZCI6ICJjNDg2OGI4YS0xZjVjLTQ1MzYtYjE5MS1kNTQyOWMyZTE0YjciLA0KICAiYWlkIjogIjAiLA0KICAic2N5IjogImF1dG8iLA0KICAibmV0IjogInRjcCIsDQogICJ0eXBlIjogIm5vbmUiLA0KICAiaG9zdCI6ICJqcDQuYWY0OWM0ZTRjMmVmLnNhbmZlbjAwNC5tZSIsDQogICJwYXRoIjogIiIsDQogICJ0bHMiOiAidGxzIiwNCiAgInNuaSI6ICIiLA0KICAiYWxwbiI6ICIiDQp9
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIkBTU1JTVUItVjE2LeS7mOi0ueaOqOiNkDpzdW8ueXQvc3Nyc3ViIiwNCiAgImFkZCI6ICIxMDQuMjIuNTkuMTk1IiwNCiAgInBvcnQiOiAiNDQzIiwNCiAgImlkIjogImExNTYwYjUyLWI1ODAtNGFhZC1iOGNkLTljZDJlYzUyNjRiNCIsDQogICJhaWQiOiAiMCIsDQogICJzY3kiOiAiYXV0byIsDQogICJuZXQiOiAid3MiLA0KICAidHlwZSI6ICJub25lIiwNCiAgImhvc3QiOiAiMS4yMzkwMDAueHl6IiwNCiAgInBhdGgiOiAiL3ZtZXNzd3MiLA0KICAidGxzIjogInRscyIsDQogICJzbmkiOiAiIiwNCiAgImFscG4iOiAiIg0KfQ==
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIkBTU1JTVUItVjE3LeS7mOi0ueaOqOiNkDpzdW8ueXQvc3Nyc3ViIiwNCiAgImFkZCI6ICJjZmNkbi5zYW5mZW5jZG4ubmV0IiwNCiAgInBvcnQiOiAiNDQzIiwNCiAgImlkIjogImM0ODY4YjhhLTFmNWMtNDUzNi1iMTkxLWQ1NDI5YzJlMTRiNyIsDQogICJhaWQiOiAiMCIsDQogICJzY3kiOiAiYXV0byIsDQogICJuZXQiOiAid3MiLA0KICAidHlwZSI6ICJub25lIiwNCiAgImhvc3QiOiAidXMxLnNhbmZlbmNkbi5uZXQiLA0KICAicGF0aCI6ICIvemgtY24iLA0KICAidGxzIjogInRscyIsDQogICJzbmkiOiAiIiwNCiAgImFscG4iOiAiIg0KfQ==
```

  - yaml 写法
如：
```yaml
proxies:
  # - {name: Node Name, type: Agreement Type, server: IP Address, port: Port, udp: true | false, tls: false, skip-cert-verify: true | false, headers: {HTTP Request Headers}}
  - {name: Free Node, type: http, server: 112.47.20.215, port: 443, udp: false, tls: false, skip-cert-verify: false, headers: {}}
```
