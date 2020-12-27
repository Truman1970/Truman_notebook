<!-- TOC -->

- [Scoop](#scoop)
- [You-Get](#you-get)
- [Github](#github)
  - [GitHub Actions](#github-actions)
- [Sqlmap](#sqlmap)
- [vscodium](#vscodium)
  - [插件](#插件)
  - [vscodium 配置python环境](#vscodium-配置python环境)
- [F-Droid](#f-droid)
  - [使用注意](#使用注意)
  - [存储库](#存储库)
  - [常用软件](#常用软件)
- [文件传输](#文件传输)
  - [在线局域网传输（待考验）](#在线局域网传输待考验)

<!-- /TOC -->


## Scoop
<https://scoop-docs.now.sh/docs/>

```shell
alias       Manage scoop aliases # 别名
bucket      Manage Scoop buckets # 管理软件仓库
cache       Show or clear the download cache # 查看与管理缓存
checkup     Check for potential problems # 检测潜在问题
cleanup     Cleanup apps by removing old versions # 清理旧版本软件包
config      Get or set configuration values # 配置Scoop
create      Create a custom app manifest # 创建自定义软件包
depends     List dependencies for an app # 查看依赖
export      Exports (an importable) list of installed apps # 导出软件包列表
help        Show help for a command # 显示帮助指令
hold        Hold an app to disable updates # 禁止软件包更新
unhold      Unhold an app to enable updates # 启动软件包更新
home        Opens the app homepage # 打开软件包主页
info        Display information about an app # 显示软件包信息
install     Install apps # 安装软件包的指令
list        List installed apps # 列出所有已安装软件包
prefix      Returns the path to the specified app # 查看软件包路径
reset       Reset an app to resolve conflicts # 恢复软件包版本
search      Search available apps # 搜索软件
status      Show status and check for new app versions # 查看软件包更新状态
uninstall   Uninstall an app # 卸载
update      Update apps, or Scoop itself # 更新
virustotal  Look for app hash on virustotal.com # 查看哈希值
which       Locate a shim/executable (similar to 'which' on Linux) # 查看可执行程序路径


scoop config aria2-enabled false # 禁用aria2
scoop config aria2-enabled true # 启用aria2
```

```shell
#注意，之前我用的_Scoop_2命名出错，可能和下划线影响ps语法了，总是出错
#aria2比较坑，还不如不安装

#修改PowerShell的安全策略，让后面的命令正常执行
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
#自定义安装位置
$env:SCOOP='D:\Scoop'
[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')
#自定义全局安装位置
$env:SCOOP_GLOBAL='D:\Scoop_G'
[Environment]::SetEnvironmentVariable('SCOOP_GLOBAL', $env:SCOOP_GLOBAL, 'Machine')

#准备阶段
scoop install git sudo
scoop bucket add extras 
scoop bucket add dorado https://github.com/h404bi/dorado
scoop install innounp dark lessmsi aria2
#安装阶段
scoop install shadowsocksr-csharp wox keepassxc vscodium windows-terminal
scoop install everything geekuninstaller googlechrome notepadplusplus qimgv snipaste
scoop install baka-mplayer ccleaner typora telegram 
scoop install python 
pip install you-get
```



## You-Get
<https://github.com/soimort/you-get>

```shell
you-get url
you-get -i url
you-get -l url  --download a playlist--
you-get -o "output-dir" url
you-get -u url
```

## Github
<https://docs.github.com/cn>


### GitHub Actions

```shell

name: 'GitHub Actions Mirror'
on: [push, delete]
jobs:
  mirror_to_gitee:
    runs-on: ubuntu-latest
    steps:
      - name: Mirror the Github organization repos to Gitee
        uses: Yikun/hub-mirror-action@master
        with:
          src: github/Truman1970
          dst: gitee/Truman1970
          dst_key: ${{ secrets.GITEE_PRIVATE_KEY }}
          dst_token: ${{ secrets.GITEE_TOKEN }}
          account_type: user

```




## Sqlmap
<http://sqlmap.org/>

```shell
python sqlmap.py -u url    #检查注入点
python sqlmap.py -u url --dbs    #爆所有数据库信息
python sqlmap.py -u url --current-db    #爆当前数据库信息：
python sqlmap.py -u url -D pikachu --tables    #指定库名列出所有表
python sqlmap.py -u url -D pikachu -T users --columns    #指定库名表名列出所有字段
python sqlmap.py -u url -D pikachu -T users -C username,password --dump    #列出表里的值

python sqlmap.py --update       #更新

```


## vscodium

### 插件
```shell
# 汉化
Chinese (Simplified) Language Pack for Visual Studio Codium
# markdown相关
Auto Markdown TOC
Markdown All in One
markdownlint
# Python环境
Python
```

### vscodium 配置python环境
参考：<https://blog.csdn.net/Zhangguohao666/article/details/105040139>

## F-Droid
<https://f-droid.org/zh_Hans/docs/>  
<https://forum.f-droid.org/t/known-repositories/721>  

### 使用注意
> 在收录的自由软件中，官方特别标示了一些带有垃圾特性〔anti-feature〕的应用，默认无法被搜索到。需要在设置 – 应用兼容性 – 包括带有 anti-feature 的应用中调整。  

### 存储库
清华大学开源软件镜像站  
<https://mirrors.tuna.tsinghua.edu.cn/fdroid/repo/?fingerprint=43238D512C1E5EB2D6569F4A3AFBF5523418B82E0A3ED1552770ABB9A9C9CCAB>  
Archive 库  
<https://mirrors.tuna.tsinghua.edu.cn/fdroid/archive?fingerprint=43238D512C1E5EB2D6569F4A3AFBF5523418B82E0A3ED1552770ABB9A9C9CCAB>   

南京大学镜像    
<https://mirrors.nju.edu.cn/fdroid/repo/?fingerprint=43238D512C1E5EB2D6569F4A3AFBF5523418B82E0A3ED1552770ABB9A9C9CCAB​>  

第三方库  
<https://apt.izzysoft.de/fdroid/repo>   
<https://fdroid.rakshazi.me/repo?fingerprint=80BF9EC0BCCED7DA2C9B272FA9B53A30E5B79282CFD629BDE14AB1FF1658C02E>  
> IzzyOnDroid，Rakshazi F-Droid等第三方库并无国内源，所以下载速度较慢。  


### 常用软件
```shell
andOTP
Tusky
Telegram FOSS
Keepass2Android
NewPipe
Tor
AntennaPod
Foxy Droid
Aurora Store
同文输入法
LBRY
```

## 文件传输
### 在线局域网传输（待考验）
<https://www.ssavr.com/>  
<https://airportal.cn/>  