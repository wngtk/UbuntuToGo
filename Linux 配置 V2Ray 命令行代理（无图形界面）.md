# Linux 配置 V2Ray 命令行代理（无图形界面）

references: [Linux 配置 V2Ray 和 ProxyChains 实现命令行代理（无图形界面）](https://github.com/gukaifeng/gukaifeng.cn/blob/05eb846dbd5ee55c2b3fbedf35a4de0e36ad5522/_posts/Linux%20%E9%85%8D%E7%BD%AE%20V2Ray%20%E5%92%8C%20ProxyChains%20%E5%AE%9E%E7%8E%B0%E5%91%BD%E4%BB%A4%E8%A1%8C%E4%BB%A3%E7%90%86%EF%BC%88%E6%97%A0%E5%9B%BE%E5%BD%A2%E7%95%8C%E9%9D%A2%EF%BC%89.md)

## 1. 安装并配置 V2Ray

### 1.1 安装 V2Ray

执行下面的命令安装（更新也可）V2Ray：

```bash
sudo bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)
```

Fish 用户：
```sh
sudo bash (curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh | psub)
```

这个执行的脚本里面会有在 GitHub 下载 v2ray-core 的 release 版的操作，所以可能会比较慢。

> 另附卸载 V2Ray 的命令：
>
> ```sh
> sudo bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh) --remove
> ```
>
> Fish 用户：
> ```sh
> sudo bash (curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh | psub) --remove
> ```

### 1.2 修改配置文件

从其他的 V2Ray 客户端导出配置文件，替换掉 `/usr/local/etc/v2ray/config.json` 中的内容：

```sh
sudo vim /usr/local/etc/v2ray/config.json
```

### 1.3 启动 V2Ray

启动 V2Ray：

```sh
systemctl start v2ray
```

## 2. 设置 http & https 代理

一般来说，socks 代理走的是 `10808` 端口，http 代理走的是 `10809` 端口。

终端设置 http & https 代理：

```sh
export http_proxy=http://localhost:10809
export https_proxy=http://localhost:10809
```

设置代理后就能正常使用 pip，npm，docker，git 等等下载依赖了。

取消 http & https 代理：

```sh
unset http_proxy
unset https_proxy
```

Fish 用户取消 http & https 代理：

```sh
set -e http_proxy
set -e https_proxy
```
