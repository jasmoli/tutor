# 常见问题
## 本机有网，热点没网？

<details>
  <summary>本机有网，热点没网？</summary>
  <p>请检查是否开启热点模式，如果开了还没网，请尝试关闭或者开启兼容模式，最新版神秘一般不需要开启兼容模式。</p>
  <p>如果热点不能访问面板，请开启兼容模式。</p>
  <p>喵佬原话：“某些人热点没网就再开起来吧（我也不知道为啥）”</p>
</details>

## 神秘 TProxy 模式怎么开？
找到 tun 入站（建议搜索 `tag: tun`），如下：

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

把 **enabled** 后的 **true** 改为 **false**，如下：

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

接着找到 tun 入站下的 tproxy 入站，如下：

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

把 **enabled** 后的 **false** 改为 **true**，如下所示：

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

修改完后保存，打开神秘面板=>设置=>神秘，点击**重载核心配置**，接着返回主页点击**重启核心**。

不出所料，已经成功了。

如果想改回去，修改 enabled 后的值，**false** 改 **true**，**true** 改 **false**，再重载+重启核心即可。

## WiFi 放行怎么做？
### MacroDroid
下载 [MacroDroid](https://t.me/xireikisub/66) 和 [MacroDroid 备份](https://t.me/xireikisub/68)

安装 [MacroDroid](https://t.me/xireikisub/66) 后，导入 [备份文件](https://t.me/xireikisub/68) 到 [MacroDroid](https://t.me/xireikisub/66)

## 怎么放行应用？
修改 **packages_list** 里的 black 或 white，它们分别是黑名单（放行列表内的应用）和白名单（只代理列表内的应用）。默认是**黑名单**。

如果你闲麻烦，可以使用我的[半成品面板](https://tpanel.netlify.app)，点击动图进入设置-名单里给对应的应用启用即可。

**packages_list** 原始内容

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

### 黑名单
**mode** 默认为黑名单，无须修改，如果要修改，参考白名单。

在 black 中添加包名，一行一个。

例如微信是 **com.tencent.mm**，原神是 **com.miHoYo.Yuanshen**（发现了吗？大小写敏感），这是手机应用的唯一名称。在小米手机中，长按桌面应用图标 => 应用详情 => 右上角ⓘ，就可以看见包名，点击复制即可。

如下所示。


```yaml
  black:
    - com.tencent.mm
    - com.miHoYo.Yuanshen
```

### 白名单
修改 **mode** 为 white。像下面这样

```yaml
packages_list:
  mode: white
  black: []
  white: []
```

在 white 中添加包名，一行一个，如下所示。

```yaml
  white:
    - com.tencent.mm
    - com.miHoYo.Yuanshen
```

## 怎么开启/关闭 fakeip?
### 关闭
第一步：打开 **/data/adb/sfm/src/baseConfig.yaml** 配置文件，给以下规则中的 `enabled` 从 `true` 改为 `false` 即可，理论来说其他步骤不用执行。执行只是关闭得更为彻底。
```yaml
    - enabled: true
      query_type:
        - A
        - AAAA
      server: fakedns
      rewrite_ttl: 1
      disable_cache: true
      notice: 对 A 和 AAAA 类型的 DNS 请求返回 fake-ip 以尽量减少本地 dns 解析并尽可能的将域名送向远端。
```

改完之后是这样：
```yaml
    - enabled: false
      query_type:
        - A
        - AAAA
      server: fakedns
      rewrite_ttl: 1
      disable_cache: true
      notice: 对 A 和 AAAA 类型的 DNS 请求返回 fake-ip 以尽量减少本地 dns 解析并尽可能的将域名送向远端。
```

改完之后前往面板 => **设置** => **模块设置**，点击**重载核心配置**。

以下步骤只是补充，非必要。

第二步: 打开神秘面板（或者神秘套壳app），进入**设置** => **DMS设置** => **修改FakeIP设置**，取消勾选**启动 FakeIP 支持**

第二步: 进入面板 => **设置** => **DMS设置** => **修改 DNS 服务器** => **fakedns**，取消勾选**启用 DNS 服务器**

### 开启
与关闭相反，将 `false` 改为 `true`，然后重载核心配置。

如果有取消勾选（执行第二步、第三步），请勾选回来。

## Geo 数据库报错？
如果你在 **开唱**/**重启核心**之后报错了，报错中有 **geo** 字眼，很有可能是 geo 数据库下载错误，请尝试更新 geo 数据库。具体方案：设置 - 模块配置 - 自动更新 Geo 数据库，关了再开即可

如问题未得到解决，请检查 geo 数据库格式和链接

## 遇到 parse outbound[n]: missing tags and uses 怎么办？

**Puer 是只喵 喵**：“你该死，一个 手动选择/自动选择 又不嵌套其他出站又不引用出站提供者，你拿头用”

请在没有嵌套任何出站、出站提供者的出站内嵌套出站、出站提供者，它不能为空！

## 关于报错中出现 1.8.0
报错：
```
cache_file and related fields in Clash API is deprecated in sing-box 1.8.0, use experimental.cache_file instead.
```
如果你的报错是这个，请遵循[迁移指南](https://sing-box.sagernet.org/zh/migration)修改配置或者重新安装神秘。

## 关于 NoTermux 版本的神秘
此版本不需要 Termux，请忽略环境配置步骤，从原版神秘覆盖安装时需要重启，其他与原版相同。

下载请前往[我的频道](https://t.me/xiayinlily)，不保证更新。

**这是修改版，不是原版**

**这是修改版，不是原版**

**这是修改版，不是原版**

## 强制重启手机后，神秘无法启动？启动失败 node.log 里有 Valid JSON 关键字?
原因可能是强制重启手机后导致 **appLables.json** 文件损坏，前往 **/data/adb/sfm/src** 删除这个文件后重新刷模块即可解决。
