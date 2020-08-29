# 远程控制Linux

## 通过SSH连接远程Linux机器

```python
import paramiko

# 创建一个 ssh 对象
ssh = paramiko.SSHClient()

# 连接方式
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy)

# 连接远程主机
ssh.connect("127.0.0.1", 22, "gabriel", "qwerty456ab")

# 运行多个命令时，命令与命令之间用 ; 分隔
stdin, stdout, stderr = ssh.exec_command('cd /data;touch a.txt')
print(stdout.read().decode('utf-8'))

ssh.close()

```

## 本地和远程机器文件互传

```python
import paramiko

# 创建一个 ssh 对象
ssh = paramiko.SSHClient()

# 连接方式
ssh.set_missing_host_key_policy(paramiko.AutoAddPolicy)

# 连接远程主机
ssh.connect("127.0.0.1", 22, "gabriel", "password")

sftp = ssh.open_sftp()

# 将本地文件传到远程机器
# 第一个参数是本地文件的路径
# 第二个参数是远程机器想要存放在这个文件的路径
sftp.put("local_source_path", "remote_destination_path")

# 将远程文件下载到本地
# 第一个参数是远程机器的文件路径
# 第二个参数是本地想要存根这个文件的路径
sftp.get("remote_source_path", "local_destination_path")

ssh.close()
```

