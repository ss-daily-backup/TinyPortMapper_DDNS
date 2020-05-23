# TinyPortMapper_KeepAlive_backup
lmc999 的 TinyPortMapper 转发脚本备份

# 修改的地方
删除了不必要的改动
- 取消 disable_selinux
- 取消添加开机自启（已经有定时任务了，开机自启没有意义）
- 不更改防火墙
- 每 5分钟执行一次IP转发保活脚本
- 每 10 分钟执行一次域名转发保活脚本
- 更改源为本repo
- 强制https证书验证，不能下载的话请先执行 `yum install ca-certificates wget -y` 或 `apt-get install ca-certificates wget -y`。
- 修改 log 文件位置为 /root/logTinyPortMapper，并更改日志等级为error
- 增加简单的当前端口列表显示


# 用法
    wget https://raw.githubusercontent.com/ss-daily-backup/TinyPortMapper_KeepAlive_backup/master/tinymapper-mod.sh
    bash tinymapper-mod.sh

#### 如遇到定时保活脚本不自动执行，可手动创建任务
    crontab -e
    */5 *  *  *  * bash /tinyPortMapper/ip_keepalive.sh
    */10 *  *  *  * bash /tinyPortMapper/domain_keepalive.sh
   #每五分钟执行一次IP转发保活脚本 #每两分钟执行一次域名转发保活脚本
