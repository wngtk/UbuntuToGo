# Ubuntu To Go

## 介绍 Ubuntu To Go

Ubuntu To Go 是将 Ubuntu 安装在U盘或移动硬盘设备上。以 Ubuntu To Go 作为 Linux 环境可以完全利用电脑的 CPU 和内存，通常比使用虚拟机的体验更好，同时不会破坏电脑原本的硬盘分区和Windows。

Ubuntu 开箱即用，而且 Ubuntu 有开箱即用的安全启动，不需要关闭BIOS中的安全启动。同时使用 Ubuntu 的人多，安装和配置过程中遇到的问题容易找到解决办法。

## Ubuntu To Go 会影响到 Windows 的时间不对

```sh
timedatectl set-local-rtc 1 --adjust-system-clock
```

## keyboard remap

https://askubuntu.com/questions/19558/what-are-the-meta-super-and-hyper-keys

ESC could be the Meta key.

Use Caps Lock as ESC.

## 安装字体

```sh
sudo apt install fonts-firacode
```

## 安装中文输入法

sudo apt install -y fcitx5 fcitx5-frontend-gtk4 fcitx5-chinese-addons

安装完后打开图形的Configuration程序，配置好拼音输入法即可。

[Setup Fcitx 5](https://fcitx-im.org/wiki/Setup_Fcitx_5#Environment_variables)

自动启动： im-config 在 Ubuntu 上没有生效！

set autostart in gnome-tweaks for fcitx5

Best option if you does not care about modifying a file with root. This file is generally supported by all distribution. The code snippet that you need to append to the end of /etc/profile is same as login shell. 
```sh
export XMODIFIERS=@im=fcitx
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
```

## Firefox 

在设置中启用 smooth_scrolling, `about:config` 中的 browser.fullscreen.autohide 设置为 false, 即可全屏下依然显示标签页。

通过 snap 安装的 Firefox 在 Ubuntu 22.04 上不能在设置`MOZ_ENABLE_WAYLAND=1`时正常使用 fcitx5。
卸载 snap 版 Firefox，安装 .deb 版的 Firefox，如果在正常安装后还是不能使用 Fcitx5。参考：
https://www.mail-archive.com/kde-bugs-dist@kde.org/msg808886.html

https://askubuntu.com/questions/1447009/control-scrolling-speed-in-webpages-in-firefox

at address bar type: about:config
`mousewheel.default.delta_multiplier_y` reduce it to `10`.

Improve scroll speed for firefox

https://askubuntu.com/questions/1413750/how-to-change-2-finger-touchpad-scroll-speed-on-ubuntu-22-04

```sh
MOZ_ENABLE_WAYLAND=1
```

## VS Code

使用 deb 包安装便可使用 fcitx5.

## tmux config

see ~/.tmux.conf

## 字体渲染配置

为了避免未知的问题，在安装Ubuntu的时候选择语言为English。然而系统语言是英文的时候，中文字体的渲染可能会有日文字形的情况出现。为了解决这个问题，修改`/etc/fonts/conf.d/64-language-selector-prefer.conf`。[^ubuntu-fonts]

```diff
diff --git a/64-language-selector-prefer.conf.bak b/64-language-selector-prefer.conf
index bce3696..b7293e9 100644
--- a/64-language-selector-prefer.conf.bak
+++ b/64-language-selector-prefer.conf
@@ -4,11 +4,11 @@
 	<alias>
 		<family>sans-serif</family>
 		<prefer>
-			<family>Noto Sans CJK JP</family>
-			<family>Noto Sans CJK KR</family>
 			<family>Noto Sans CJK SC</family>
 			<family>Noto Sans CJK TC</family>
 			<family>Noto Sans CJK HK</family>
+			<family>Noto Sans CJK JP</family>
+			<family>Noto Sans CJK KR</family>
 			<family>Lohit Devanagari</family>
 			<family>Noto Sans Sinhala</family>
 		</prefer>
@@ -16,10 +16,10 @@
 	<alias>
 		<family>serif</family>
 		<prefer>
-			<family>Noto Serif CJK JP</family>
-			<family>Noto Serif CJK KR</family>
 			<family>Noto Serif CJK SC</family>
 			<family>Noto Serif CJK TC</family>
+			<family>Noto Serif CJK JP</family>
+			<family>Noto Serif CJK KR</family>
 			<family>Lohit Devanagari</family>
 			<family>Noto Serif Sinhala</family>
 		</prefer>
@@ -27,11 +27,11 @@
 	<alias>
 		<family>monospace</family>
 		<prefer>
-			<family>Noto Sans Mono CJK JP</family>
-			<family>Noto Sans Mono CJK KR</family>
 			<family>Noto Sans Mono CJK SC</family>
 			<family>Noto Sans Mono CJK TC</family>
 			<family>Noto Sans Mono CJK HK</family>
+			<family>Noto Sans Mono CJK JP</family>
+			<family>Noto Sans Mono CJK KR</family>
 		</prefer>
 	</alias>
 </fontconfig>
 ```

[^ubuntu-fonts]: https://bediverezero.github.io/ubuntu/2021/06/04/ubunt-fonts.html
