## Installing the [Termux](https://github.com/termux/termux-app/releases) Application
Termux has two release channels, [Github](https://github.com/termux/termux-app/releases) and [F-Droid](https://f-droid.org/packages/com.termux/ ), novices are advised to download the version of [F-Droid](https://f-droid.org/packages/com.termux/) (click on the text to go to the corresponding download channel)

Tip: If you don’t want to do this step, you can use [my modified version](https://t.me/xiayinlily)(NoTermux), which removes environment dependencies.

## Install nodejs and aapt (please view README.md for PC version)
Open Termux and execute the following commands in sequence. I will explain them one by one.

Prior statement: **Since the official source is slow, please consider accessing through a proxy as appropriate! **

Tip: You can also search for the source replacement method yourself (not recommended).

This command is used to update all software packages currently in Termux. If you get stuck during the installation process, please use the input method, enter a lowercase `y` and press Enter:
```bash
pkg up -y
```

The last step is to install nodejs and aapt
```bash
pkg in nodejs aapt -y
```

Check whether nodejs is installed. As shown in the figure, the installation is successful.
```bash
node -v
```

![](../assets/20230505102753101.jpg)

This picture comes from: [Introduction to Mysterious Module Tutorial (Android)](https://telegra.ph/%E7%A5%9E%E7%A7%98%E6%A8%A1%E5%9D%97%E7 %AE%80%E6%98%8E%E6%95%99%E7%A8%8BAndroid%E7%AB%AF-04-06)

Check whether aapt is installed successfully. If a lot of text is output as shown in the figure, it is successful.
```bash
aapt
```

![Installation successful](../assets/20230906153119436.jpg)

If you are prompted that **aapt 环境损坏** when installing a module, please execute `pkg uninstall aapt` to uninstall **aapt** and then execute `pkg up && pkg in aapt` to reinstall **aapt**.

If you are prompted that **node 环境损坏** when installing a module, please execute `pkg uninstall nodejs` to uninstall **nodejs** and then execute `pkg up && pkg in nodejs` to reinstall **nodejs**.
