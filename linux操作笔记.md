# linux操作笔记

## 磁盘操作

### 卸载磁盘

umount /home

### 查看磁盘分区类型

df -T

### 挂载磁盘

mount /dev/mapper/cl-home /home

### 删除文件

rm -rf /root/home.img

### 定时关机

```
1、crontab -e 回车
2、添加任务，并保存
#每天下午19:00定时关机
55 18 * * * /sbin/shutdown -h 19:00
3、查看任务列表
crontab -l
4、取消
sudo shutdown -c
```