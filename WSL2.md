#### Neovim 在 WSL2 不能将文本内容拷贝到系统剪贴板

Ubuntu 一般安装了 xsel，但是 WSL 其他的发行版没有的话需要手动安装。

```bash
apt install xsel
```

#### WSL2 的 `/tmp` 目录没有自动清理

```bash
systemctl start systemd-tmpfiles-clean.service
```

下次启动就会清理掉 `/tmp` 了。
