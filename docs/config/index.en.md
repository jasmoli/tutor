---
comments: true
---
# Modify configuration file
The configuration file is in the **/data/adb/sfm/src/** (Android) or the **src** folder of the directory where the module is placed on your computer.

After modifying the configuration, click **Restart Core**, or **Close the core** first and then modify it, or after modification, go to **Settings** -> **Module Settings** and click **Reload Core Configuration**; After modification, click **Close Core** and the original configuration will overwrite the changed configuration** causing the changes to be invalid**

For detailed modifications, please see [Official Document](https://sing-box.sagernet.org/zh/).

The format used by the official document configuration is JSON, which is a common data format, while the configuration of the mysterious module uses YAML as the configuration language.

YAML is a superset of JSON and is very different except for the single-line syntax.

Compared with JSON, YAML does not need to use double quotes for strings. For example, `"text": "Hello, this is a piece of text"` should look like this in YAML: `text: Hello, this is A piece of text` (all colons are English colons).

Because it is unnecessary, `text: "Hello, this is a piece of text"` is also legal.

Another example, in JSON you can write like this
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

But in YAML, you should write it like this (one way of writing, the other is not recommended, easy to confuse)
```yaml
name: 喵喵
age: 25
sex: 男
married: true
phone:
  - 1xxxxxxxxxx
  - 1xxxxxxxxxx
```