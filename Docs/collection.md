

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

```shell
steps:
- name: Mirror the Github organization repos to Gitee.
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