---
comments: true
---
# 修改配置文件
配置文件在 **/data/adb/sfm/src/**（安卓）或者你电脑上放模块的目录的**src**文件夹中。

修改配置后点击**重启核心**，或者先**关闭核心**再修改或者修改完后前往**设置** -> **模块设置**，点击**重载核心配置**；修改完后点击**关闭核心**会发生原配置覆盖更改后的配置**导致更改无效**

详细修改可看[官方文档](https://sing-box.sagernet.org/zh/)，或者等我更新。

官方文档配置使用的格式是 JSON，是一种常见的数据格式，而神秘模块的配置使用 YAML 作为配置语言。

YAML 是 JSON 的超集，除了单行语法外，很不一样。

与 JSON 相比，YAML 对于字符串可以不需要使用双引号包含起来，比如 `"text": "你好，这是一段文本"` 在 YAML 中应该是这样的：`text: 你好，这是一段文本`（所有的冒号都是英文冒号）。

因为是可以不需要，所以 `text: "你好，这是一段文本"` 也是合法的。

又如，在 JSON 中你可以这么写
```json
{
  "name": "喵喵",
  "age": 25,
  "sex": "男",
  "married": true,
  "phone": [
    "1xxxxxxxxxx",
    "1xxxxxxxxxx"
  ]
}
```

但在 YAML 中，你应该这么写（写法之一，其他不推荐，易混淆）
```yaml
name: 喵喵
age: 25
sex: 男
married: true
phone:
  - 1xxxxxxxxxx
  - 1xxxxxxxxxx
```
