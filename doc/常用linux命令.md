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