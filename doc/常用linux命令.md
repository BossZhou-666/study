启动docker
```
systemctl start docker
```

关闭docker
```
systemctl stop docker
```

重启docker
```
systemctl restart docker
```

docker设置随服务启动而自启动
```
systemctl enable docker
```

查看docker 运行状态
------如果是在运行中 输入命令后 会看到绿色的active
```
systemctl status docker
```

查看docker 版本号信息
```
docker version
docker info
```

防火墙命令

查看防火墙状态
```
systemctl status firewalld
```

开启防火墙
```
systemctl start firewalld.service
```

关闭防火墙
```
systemctl stop firewalld.service
```

设置开机自启动
```
systemctl enable firewalld.service
```

查看防火墙的开放端口
```
firewall-cmd --zone=public --list-ports
```
允许防火墙放行443端口

命令含义：
```
--zone #作用域

--add-port=443/tcp #添加端口，格式为：端口/通讯协议

--permanent #代表永久生效，没有此参数重启后失效

firewall-cmd --zone=public --add-port=443/tcp --permanent
```

重启防火墙
```
firewall-cmd --reload
```

解压zip文件到指定目录
```
unzip mydata.zip -d mydatabak
```
端口占用
```
打开命令行工具，输入：netstat -aon|findstr 8080
taskkill /t /f /im 进程号（ ！！！注意是进程号，不是端口号）
```

拷贝命令
```
sshpass -p $Remote_PW scp -o StrictHostKeyChecking=no -P $Remote_Port -r $Local_dir/* root@$Remote_IP:$Remote_dir
sshpass -p 'rzx@1218' scp -o StrictHostKeyChecking=no -P 22 /data/minio/data/backUpSystemFile_20230216_115301.tar.gz root@10.12.109.112:/root/
```

远程控制创建文件夹
```
sshpass -p {密码} ssh -p {端口} -o StrictHostKeyChecking=no {用户名}@{主机IP} 'rm -rf /tmp/test'
sshpass -p 'rzx@1218' ssh -p 22 -o StrictHostKeyChecking=no root@10.12.109.112 'mkdir -p /data/backup/' 
```
备份导出sql
```
/usr/bin/mysqldump  --single-transaction  --opt -hlocalhost --user=root --password='3GDcn2lUFIRVEsXxljUfpK!kYIy&sOC1' -P3300 --databases tdsms --tables tdsms_logs_clipboard tdsms_logs_email tdsms_logs_file_opt tdsms_logs_file_send tdsms_logs_html tdsms_logs_im_msg tdsms_logs_print tdsms_logs_screen tdsms_logs_search tdsms_logs_user_auth tdsms_terminal_software_log tdsms_terminal_usb_log -w"act_time >= '2021-11-16 18:53:24'" --result-file=/data/mysql/backUpSystemLog_20230217_030000_sql.sql
```

使用ssh进入容器命令。不能加-it
```
docker exec rws-mgt /bin/su -c "mkdir -p /data/backup/"
```

```
nsenter -m -t 1
```
nsenter命令删除目录，千万不能带* 
比如：rm -rf /data/backup/* 需要写成 rm -rf /data/backup/  带*在容器里面不会去执行的