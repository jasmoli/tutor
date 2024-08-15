---
comments: true
---
# common problem
## This machine has internet, but the hotspot doesn’t?

<details>
  <summary>This machine has internet but the hotspot doesn’t?</summary>
  <p>Please check whether the hotspot mode is turned on. If there is no Internet connection, please try to turn off or turn on the compatibility mode. The latest version of Mystery generally does not need to turn on the compatibility mode.</p>
  <p>If the hotspot cannot access the panel, please enable compatibility mode.</p>
  <p>Author's words：“Some people’s hotspots can be turned on again if they don’t have internet access (I don’t know why)”</p>
</details>

## How to enable mysterious TProxy mode?
Find the tun inbound (it is recommended to search for `tag: tun`), as follows:

```yaml
  - enabled: true
    tag: tun
    type: tun
    interface_name: tun1
    inet4_address: 172.19.0.0/16
    inet6_address: 2001:10::/28
    strict_route: true
    auto_route: true
    stack: mixed
    sniff: true
    sniff_override_destination: false
    sniff_override_rules:
      - type: logical
        mode: and
        rules:
          - domain_keyword: .
          - rule_set:
              - 跳过覆写
              - 推送服务-IP
              - 推送服务-域名
            invert: true
```

Change **true** after **enabled** to **false**, as follows:

```yaml
  - enabled: false
    tag: tun
    type: tun
    interface_name: tun1
    inet4_address: 172.19.0.0/16
    inet6_address: 2001:10::/28
    strict_route: true
    auto_route: true
    stack: mixed
    sniff: true
    sniff_override_destination: false
    sniff_override_rules:
      - type: logical
        mode: and
        rules:
          - domain_keyword: .
          - rule_set:
              - 跳过覆写
              - 推送服务-IP
              - 推送服务-域名
            invert: true
```

Then find the tproxy inbound under tun inbound, as follows:

```yaml
inbounds:
  - enabled: false
    tag: tproxy
    type: tproxy
    listen: '::'
    listen_port: 10086
    sniff: true
    sniff_override_destination: false
    sniff_override_rules:
      - type: logical
        mode: and
        rules:
          - domain_keyword: .
          - rule_set:
              - 跳过覆写
              - 推送服务-IP
              - 推送服务-域名
            invert: true
```

Change **false** after **enabled** to **true**, as shown below:

```yaml
inbounds:
  - enabled: true
    tag: tproxy
    type: tproxy
    listen: '::'
    listen_port: 10086
    sniff: true
    sniff_override_destination: false
    sniff_override_rules:
      - type: logical
        mode: and
        rules:
          - domain_keyword: .
          - rule_set:
              - 跳过覆写
              - 推送服务-IP
              - 推送服务-域名
            invert: true
```

Save after modification, open the Mystery panel => Settings => Mystery, click **Reload Core Configuration**, then return to the homepage and click **Restart Core**.

As expected, it has worked.

If you want to change it back, modify the value after enabled, change **false** to **true**, change **true** to **false**, and then reload + restart the core.

## How to release WiFi?
### MacroDroid
Download [MacroDroid](https://t.me/xireikisub/66) and [MacroDroid Backup](https://t.me/xireikisub/68)

After installing [MacroDroid](https://t.me/xireikisub/66), import [backup file](https://t.me/xireikisub/68) to [MacroDroid](https://t.me/ xireikisub/66)

## How to release the application?
Modify black or white in **packages_list**, which are respectively the blacklist (applications in the release list) and the whitelist (only applications in the proxy list). The default is **blacklist**.

If you have time and trouble, you can use my [TPanel](https://tpanel.xireiki.com), click on the animation to enter the settings-list and enable the corresponding application.

**packages_list** Original content

```yaml
packages_list:
  mode: black
  black: []
  white: []
  notice: |-
    mode 有两个值，black or white
    两个数组分别对应黑名单和白名单，目前名单里只允许填写包名
    上个版本的 list 会根据 mode 自动转换成 black 和 white 两个数组里的值
```

### blacklist
**mode** defaults to the blacklist and does not need to be modified. If you want to modify it, refer to the whitelist.

Add package names in black, one per line.

For example, WeChat is **com.tencent.mm**, Genshin Impact is **com.miHoYo.Yuanshen** (did you find it? Case sensitive), which are the only names of mobile applications. In Xiaomi mobile phones, long press the desktop application icon => Application details => ⓘ in the upper right corner, you can see the package name, click to copy.

As follows.

```yaml
  black:
    - com.tencent.mm
    - com.miHoYo.Yuanshen
```

### whitelist
Modify **mode** to white. Like below

```yaml
packages_list:
  mode: white
  black: []
  white: []
```

Add the package names in white, one per line, as shown below.

```yaml
  white:
    - com.tencent.mm
    - com.miHoYo.Yuanshen
```

## How to enable/disable fakeip?
Open the mysterious panel, enter **操控核心** -> **Lower Left Corner Gear** at startup, and modify the mode at **切换路由模式**.

## Geo database error?
If you report an error after **starting**/**restarting the core** and there is the word **geo** in the error, it is most likely a geo database download error. Please try to update the geo database. Specific solution: Settings - Module Configuration - Automatically update Geo database, just turn it off and on again

If the issue is not resolved, please check the geo database format and links

## What should I do if I encounter "parse outbound[n]: missing tags and uses"?

**Puer 是只喵 喵~**(Module Author): "Damn it, you use manual selection/automatic selection without nesting other outbound or citing outbound providers."

Please nest outbound, outbound providers within an outbound that does not nest any outbound, outbound providers, it cannot be empty!

## Keyword 1.8.0 appears in the error report
Error reported:
```
cache_file and related fields in Clash API is deprecated in sing-box 1.8.0, use experimental.cache_file instead.
```
If your error is this, please follow the [Migration Guide](https://sing-box.sagernet.org/zh/migration) to modify the configuration or reinstall sing-box.

## The 神秘 about NoTermux version
This version does not require Termux. Please ignore the environment configuration steps. You need to restart when installing from the original mysterious overlay. Everything else is the same as the original version.

To download, please go to [My Channel](https://t.me/xiayinlily), updates are not guaranteed.

**This is a modified version, not the original version**

**This is a modified version, not the original version**

**This is a modified version, not the original version**

## After force restarting the phone, it mysteriously fails to start? Startup failed. Is there Valid JSON keyword in node.log?
The reason may be that the **appLables.json** file is damaged after a forced restart of the phone. Go to **/data/adb/sfm/src** to delete this file and re-flash the module to solve the problem.
