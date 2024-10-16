# btpanel-v7.7.0
btpanel-v7.7.0-backup  官方原版v7.7.0版本面板备份
## 原作者的
**Centos/Ubuntu/Debian安装命令 独立运行环境（py3.7）**

```Bash
curl -sSO https://raw.githubusercontent.com/8838/btpanel-v7.7.0/main/install/install_panel.sh && bash install_panel.sh
```

**备用安装链接，适用于不能访问GitHub的服务器。文件公开存放在[d.moe.ms](http://d.moe.ms/?btpanel-v7.7.0)**

```
curl -sSO http://d.moe.ms/AAAAA/btpanel-v7.7.0/install/install_panel.sh && bash install_panel.sh
```
## 我备份的
**Centos/Ubuntu/Debian安装命令 独立运行环境（py3.7）**

```Bash
curl -sSO https://raw.githubusercontent.com/xiefengshang/btpanel-v7.7.0/main/install/install_panel.sh && bash install_panel.sh
```

**彩虹优化脚本**
```Bash
curl -sSO https://raw.githubusercontent.com/Xiefengshang/btpanel-v7.7.0/main/scripts/optimize.sh && bash optimize.sh
```

# 手动破解：

1，屏蔽手机号

```
sed -i "s|bind_user == 'True'|bind_user == 'XXXX'|" /www/server/panel/BTPanel/static/js/index.js
```

2，删除强制绑定手机js文件

```
rm -f /www/server/panel/data/bind.pl
```

3，手动解锁宝塔所有付费插件为永不过期

文件路径：`/www/server/panel/data/plugin.json`
**该文件需要你先进入宝塔的软件商店之后才会生成**

搜索字符串：`"endtime": -1`全部替换为`"endtime": 999999999999`  
`GPT`写的脚本，没试过
```
sed -i 's/"endtime": -1/"endtime": 999999999999/g' /www/server/panel/data/plugin.json
```

4，给plugin.json文件上锁防止自动修复为免费版

```
chattr +i /www/server/panel/data/plugin.json
```
5. 净化面板
下载文件
```
wget -O /tmp/bt.zip https://github.com/xiefengshang/btpanel-v7.7.0/raw/main/bt.zip
```
解压文件并合并到目标目录 (选A 同意覆盖所有)
```
unzip -u /tmp/bt.zip -d /www/server/panel/BTPanel/templates/default
```
删除下载的压缩文件（如果需要）
```
rm /tmp/bt.zip
```
============================

！！如需取消屏蔽手机号

```
sed -i "s|if (bind_user == 'REMOVED') {|if (bind_user == 'True') {|g" /www/server/panel/BTPanel/static/js/index.js
```
## 解决宝塔面板SSL证书安装失败： Invalid version. The only valid version for X509Req is 0.
运行如下脚本
```
sed -i 's/X509Req\.set_version(2)/X509Req\.set_version(0)/' /www/server/panel/class/acme_v2.py
```
然后重启面板即可
```
bt restart
```
