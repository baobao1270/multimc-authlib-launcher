# mmcai.sh - 基于 bash 的 MultiMC x Authlib Injector 登录器

MultiMC / Prism Launcher 本身不支持 Authlib Injector 登录，并且官方表示永远不会实现。因此自己写了一个 Shell 来实现这个功能。

仅限 Linux / macOS 使用。

## 依赖
 - `base64`
 - `jq`
 - `curl`
 - `sed`, Linux 上为 GNU sed，macOS 上必须安装 `gsed`
 - `uuidgen`
 - `dd`
 - `bash` - Bash 不需要是你的默认 Shell，但是应该在你的电脑上被安装

您的设备应该存在 `/dev/urandom`。

如果是 macOS 用户，以上依赖必须使用 Homebrew 安装。

## 安装

```bash
git clone https://github.com/baobao1270/mmcai.sh.git
mg mmcai.sh ~/.mmcai.sh
cd ~/.mmcai.sh
chmod +x mmcai-login
chmod +x mmcai-launch-minecraft
```

以下所有说明假设您将 mmcai.sh 安装到 `~/.mmcai.sh`。如果您安装到其他位置，请自行替换。

## 登录
```
$ cd ~/.mmcai.sh
$ ./mmcai-login https://skim.mc.example.com/api/yggdrasil
Using server endpoint: https://skim.mc.example.com/api/yggdrasil
Waiting for server response...
Server name: Blessing Skin 皮肤站
Note: when entering password, there is no echo on the screen.
Username: Luo_Tianyi
Password:
Getting client token...
1+0 records in
1+0 records out
512 bytes transferred in 0.000074 secs (6918919 bytes/sec)
Login Success!
```

注意输入密码时没有回显。

## 启动 Minecraft
在 MultiMC / Prism Launcher 中，编辑实例，选择「设置」——「自定义命令」，填写「包装器命令」为：
```
~/.mmcai.sh/mmcai-launch-minecraft
```

其中，将 `~` 替换为你的 Home 目录的绝对路径。
