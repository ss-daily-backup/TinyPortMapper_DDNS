# TinyPortMapper_KeepAlive_backup
lmc999 的 TinyPortMapper 转发脚本备份以及各种修改版

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
- 重定向 crontab 日志，并增加时间戳，以免引发MTA安装时的邮件轰炸灾难，crontab 日志在 /root/logTinyPortMapper_cronjob

# 用法
    wget https://raw.githubusercontent.com/ss-daily-backup/TinyPortMapper_KeepAlive_backup/master/tinymapper-mod.sh
    bash tinymapper-mod.sh

#### 如遇到定时保活脚本不自动执行，可手动创建任务
    crontab -e
    # 然后在底部添加以下两行
    echo "*/5 * * * * root bash /tinyPortMapper/ip_keepalive.sh >> /root/logTinyPortMapper_cronjob 2>&1" >> /etc/crontab
    echo "*/10 * * * * root bash /tinyPortMapper/domain_keepalive.sh >> /root/logTinyPortMapper_cronjob 2>&1" >> /etc/crontab

