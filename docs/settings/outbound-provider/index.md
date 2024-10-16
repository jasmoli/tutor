---
comments: true
---
![](../../assets/20231007232750279.jpg)

## 选项解释

| 名称 | 解释 |
| :---- | :---- |
| 网络订阅 | 机场网络订阅，从机场服务器获取节点信息 |
| 本地文件 | 本地节点文件，一般用于自建节点，免流。文件存放位置位于 `/data/adb/sfm/src/FileProviders/`，现在已经可以通过面板修改，无需打开目录 |
| 修改文件 | 修改本地节点文件，语法详见[本地节点文件写法](#本地节点文件写法) |
| 订阅链接 | 订阅链接，推荐 Clash 的订阅 |
| 可否被引用 | 是否启用该出站提供者，启用表示使用这个订阅。喵佬原话：“（不启用）是根本不会被加入配置文件” |
| 订阅拉取间隔 | 多久更新一次机场订阅，默认 3600，也就是一个小时 |
| 拉取订阅时查询订阅信息 | 查询机场流量及使用情况 |
| 修改提供者内出站设置 | 下面的都是修改请求的，用于免流，不介绍 |

## 本地节点文件写法
  - 使用节点链接
如：
```
vmess://ew0KICAidiI6ICIyIiwNCiAgInBzIjogIkBTU1JTVUItVjE1LeS7mOi0ueaOqOiNkDpzdW8ueXQvc3Nyc3ViIiwNCiAgImFkZCI6ICJqcDQuYWY0OWM0ZTRjMmVmLnNhbmZlbjAwNC5tZSIsDQogICJwb3J0IjogIjQ0MyIsDQogICJpZCI6ICJjNDg2OGI4YS0xZjVjLTQ1MzYtYjE5MS1kNTQyOWMyZTE0YjciLA0KICAiYWlkIjogIjAiLA0KICAic2N5IjogImF1dG8iLA0KICAibmV0IjogInRjcCIsDQogICJ0eXBlIjogIm5vbmUiLA0KICAiaG9zdCI6ICJqcDQuYWY0OWM0ZTRjMmVmLnNhbmZlbjAwNC5tZSIsDQogICJwYXRoIjogIiIsDQogICJ0bHMiOiAidGxzIiwNCiAgInNuaSI6ICIiLA0KICAiYWxwbiI6ICIiDQp9
hy2://962144c6@proxy.114514.com:9265/?insecure=1&sni=www.baidu.com#🇰🇷日本-Hysteria2
```
具体请自行百度/谷歌对应协议的链接格式

  - 使用 clash/mihomo 配置
如：
```yaml
proxies:
  # - {name: 节点名称, type: 协议类型, server: IP地址, port: 端口, udp: 是否是udp底层协议, tls: false, skip-cert-verify: 是否跳过证书验证, headers: {请求头}}
  # 一行写法
  - {name: 免费节点, type: http, server: 112.47.20.215, port: 443, udp: false, tls: false, skip-cert-verify: false, headers: {}}
  # 多行写法
  - name: 免费节点1
    type: ss
    server: 114.5.1.4
    port: 9265
    tls: true
    sni: baidu.com
    password: lYEiyacJG4m3UozsejfhRiwIjXfdnO4R+oflSfbl1G8=
```
具体请查看 [mihomo wiki](https://wiki.metacubex.one)

  - 使用 sing-box 配置格式
如：
```json
{
	"outbounds": [
		// 一行写法
		{ "tag": "香港", "type": "hysteria2", "server": "proxy.example.com", "server_port": 23333, "password": "937a450d-b5e7-4a34-b671-ac9899abb7a47", "tls": { "enabled": true }, "tcp_fast_open": false },
		// 多行写法
		{
			"tag": "香港",
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
具体请查看 [sing-box wiki](https://sing-box.sagernet.org)
