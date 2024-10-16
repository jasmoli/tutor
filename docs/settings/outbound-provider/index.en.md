---
comments: true
---
![](../../assets/20231007232750279.jpg)

## Option explanation

| Option | Explain |
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
  - Link format using protocol
For example：
```
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIkBTU1JTVUItVjE1LeS7mOi0ueaOqOiNkDpzdW8ueXQvc3Nyc3ViIiwNCiAgImFkZCI6ICJqcDQuYWY0OWM0ZTRjMmVmLnNhbmZlbjAwNC5tZSIsDQogICJwb3J0IjogIjQ0MyIsDQogICJpZCI6ICJjNDg2OGI4YS0xZjVjLTQ1MzYtYjE5MS1kNTQyOWMyZTE0YjciLA0KICAiYWlkIjogIjAiLA0KICAic2N5IjogImF1dG8iLA0KICAibmV0IjogInRjcCIsDQogICJ0eXBlIjogIm5vbmUiLA0KICAiaG9zdCI6ICJqcDQuYWY0OWM0ZTRjMmVmLnNhbmZlbjAwNC5tZSIsDQogICJwYXRoIjogIiIsDQogICJ0bHMiOiAidGxzIiwNCiAgInNuaSI6ICIiLA0KICAiYWxwbiI6ICIiDQp9
hy2://962144c6@proxy.114514.com:9265/?insecure=1&sni=www.baidu.com#🇰🇷日本-Hysteria2
```
For details, please refer to the link format of Baidu/Google corresponding agreement.

  - Use clash/mihomo configuration
For example：
```yaml
proxies:
  # - {name: "Outbound Name", type: protocol type, server: IP address, port: port, udp: Is it the underlying protocol of udp, tls: false, skip-cert-verify: Whether to skip certificate verification, headers: {Request header}}
  # one line writing
  - {name: HK, type: http, server: 112.47.20.215, port: 443, udp: false, tls: false, skip-cert-verify: false, headers: {}}
  # multi-line writing
  - name: HK1
    type: ss
    server: 114.5.1.4
    port: 9265
    tls: true
    sni: baidu.com
    password: lYEiyacJG4m3UozsejfhRiwIjXfdnO4R+oflSfbl1G8=
```
Please check [mihomo wiki](https://wiki.metacubex.one) for details

  - Use sing-box configuration format
For example：
```json
{
	"outbounds": [
		// one line writing
		{ "tag": "HK", "type": "hysteria2", "server": "proxy.example.com", "server_port": 23333, "password": "937a450d-b5e7-4a34-b671-ac9899abb7a47", "tls": { "enabled": true }, "tcp_fast_open": false },
		// multi-line writing
		{
			"tag": "HK",
			"type": "hysteria2",
			"server": "proxy.xireiki.com",
			"server_port": 23333,
			"password": "937a450d-b5e7-4a34-b671-ac9899abb7a47",
			"tls": {
				"enabled": true
			},
			"tcp_fast_open": false
		}
	]
}
```
For details, please check [sing-box wiki](https://sing-box.sagernet.org)
