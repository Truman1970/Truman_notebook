<https://www.jianshu.com/p/01bfce3239e6>  

### ibus-rime： 基于 IBus 輸入法框架

**安装**
```bash
# 安装
sudo apt-get install ibus-rime
```

**重启**
```bash
# 安装完毕需要重启输入法，或者注销用户重新登录
ibus restart
```

**配置**
```bash
# 本配置适用于Linux（朙月拼音·简化字）配置
git clone https://github.com/jayknoxqu/ibus-rime.git
# 复制配置文件
cp -r ibus-rime/* ~/.config/ibus/rime
# 部署配置文件
ibus-daemon -drx
```

Ubuntu包管理工具整理 - weaming - 博客园
<https://www.cnblogs.com/weaming/p/5079032.html>