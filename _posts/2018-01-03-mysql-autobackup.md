---
layout: post
title: 'MySQL每天固定几个时段自动备份数据库并压缩'
date: 2018-01-03
author: wutong
tags:  linux php mysql mariadb apache
cover: '/assets/img/hero.jpg'
---

感觉自己越来越像个运维了，3台服务器公司又不做快照，基于负责任的态度，写个脚本每天自动备份3台业务服务器的数据库并自动同步到备份服务器，然后每天上班自己机器在自动拉取备份数据到硬盘 ^_^

### 创建要备份的数据库列表

创建 `databases.txt` 并每一行写个数据库名称

### 创建备份脚本

创建 `mysql-auto-backup` 文件，赋予执行权限并填写如下命令

```bash
#!/usr/bin/env sh
#author : wutong
#date : 2018-01-03

#数据库连接的相关信息，需要有导出权限
db_user="root"
db_password="root"
db_host="127.0.0.1"
db_port="3306"

#当前时间
current_date=`date "+%Y%m%d"`
current_time=`date "+%H%M%S"`

#当前目录
current_directory=`dirname $0`

#保存目录
backup_base="/web/backup/${current_date}"
if [[ ! -d ${backup_base} ]]; then
    mkdir -p ${backup_base}
fi

#要备份的数据库列表
databases=`cat "${current_directory}/databases.txt" | cut -f 1`

#循环备份
for database in ${databases}
do
    echo "备份 ${database} ..."
    database_file="${backup_base}/${database}-${current_time}.sql"
    database_zip="${database_file}.zip"
    if [[ -f ${database_zip} ]]; then
        echo "数据库 ${database_zip} 已经存在，导出忽略"
        continue
    fi
    mysqldump --host=${db_host} --port=${db_port} --user=${db_user} --password=${db_password} --databases ${database} --add-drop-table --create-options --hex-blob --events --add-locks --lock-tables  > ${database_file}
    zip -j9 ${database_zip} ${database_file}
    if [[ -f ${database_zip} ]]; then
        rm -rf ${database_file}
    fi
done
```

### 创建cron任务

敲 `crontab -e` 并填写如下命令

```bash
1 */6 * * * 备份脚本全路径
```

### 备份服务器自动拉取备份

```bash
rsync -aP 账户信息:远程目录 本地目录
```