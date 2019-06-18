windows定时自动关机脚本
=======================
## .bat批处理脚本
#### 批处理介绍（batch）
批处理(Batch)，也称为批处理脚本。它是对某对象进行批量的处理，通常被认为是一种简化的脚本语言，应用于DOS和Windows系统中。批处理文件的扩展名为bat。
#### 新建批处理脚本
右键新建一个txt文本文件，写入命令语句，保存为.bat格式的文件，即可成功创建批处理脚本。

## Shutdown指令
windows系统，在命令行中输入“shutdown”指令，可以关闭或重新启动本地或远程计算机。
shutdown指令的参数如下：
```
shutdown /i 或 shutdown -i
```
显示图形用户界面，必须作为第一个参数才可生效
```
shutdown /m \远程计算机名 或 shutdown -m \远程计算机名
```
控制远程计算机
```
shutdown /s 或 shutdown -s
```
关闭计算机
```
shutdown /r 或 shutdown -r
```
重启计算机
```
shutdown /l 或 shutdown -l
```
注销当前用户，对远程计算机不适用。
```
shutdown /a 或 shutdown -a
```
取消关机操作
```
shutdown /f 或 shutdown -f
```
强行关闭应用程序
```
shutdown /t 时间 或 shutdown -t 时间
```
设置关机倒计时，以秒为单位
```
shutdown /c ”消息内容”  或 shutdown -c ”消息内容”
```
设置关机时，提示对话框中的消息内容(不能超127个字符)
注意：某些字符，如“-”，可能无法在消息提示中显示，导致该字符后的消息内容被截断。即使复用“ ”来也无法避免。例子见后文。

## AT指令编写定时自动关机脚本
适用于Win 7及更低版本
（部分win7有执行AT指令失败，执行SCHTASKS指令成功的情况）
#### AT指令脚本编写
新建一个脚本，命名为turnoff.bat
输入以下命令并保存
```
at 22:30 /every:Sunday,Monday,Tuesday,Wednesday,Thursday,Friday,Saturday shutdown /f /s /t 60 /c "60秒后自动关机,在命令行中输入[shutdown 短杠a]来取消"
```
#### AT指令脚本执行
编写完turnoff.bat脚本后，在本地计算机上，双击即可执行。

执行成功后，打开命令行，输入at指令，确认脚本已经完成安装。
```
at
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614214056989.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2lua2Zsb3c=,size_16,color_FFFFFF,t_70)
脚本执行成功后，到达设置时间22:30，计算机会弹出提示窗口
（由于显示规则限制，提示信息中短杠为“-”）
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061421414693.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2lua2Zsb3c=,size_16,color_FFFFFF,t_70)
如果想要取消，继续使用计算机，则在命令行中输入
```
shutdown –a
```
可取消自动关机
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614214214131.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2lua2Zsb3c=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614214222393.png)
删除已经启用的at指令脚本任务
```
at 序号 /d 或 at 序号 /delete 
```
此处序号为用at指令查出的任务对应的序号
## SCHTASKS指令编写定时自动关机脚本
适用于Win 7及更高版本
（部分win7有执行SCHTASKS指令失败，执行AT指令成功的情况）
#### SCHTASKS指令脚本编写
新建一个脚本，命名为turnoff.bat
输入以下命令并保存
```
SCHTASKS /Create /tn "turnoff" /tr "shutdown /s /t 60" /sc DAILY /st 22:30
```
或者
```
SCHTASKS /Create /tn "turnoff" /tr "shutdown -s -t 60" /sc DAILY /st 22:30
```
#### SCHTASKS指令脚本执行
编写完turnoff-schtasks.bat脚本后，在本地计算机上，双击即可执行。
执行成功后，打开命令行，输入以下指令，确认脚本已经完成安装。
```
SCHTASKS /Query /tn turnoff
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614214650159.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2lua2Zsb3c=,size_16,color_FFFFFF,t_70)
脚本执行成功后，到达设置时间22:30，计算机会弹出提示窗口
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019061421470052.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2lua2Zsb3c=,size_16,color_FFFFFF,t_70)
如果想要取消，继续使用计算机，则在命令行中输入下列指令，可取消自动关机
```
shutdown –a
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614214708364.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2lua2Zsb3c=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614214714790.png)
删除已经启用的SCHTASKS指令脚本任务
```
SCHTASKS /delete /tn 任务名
```
此处任务名为用SCHTASKS指令编写脚本时，/tn 参数后设置的任务名![在这里插入图片描述](https://img-blog.csdnimg.cn/20190614213033921.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2lua2Zsb3c=,size_16,color_FFFFFF,t_70)
## 脚本执行未成功的处理方案
在公司大批量地使用此脚本进行定时关机后，遇到了好几个脚本未生效或者生效未执行的情况，分享出来供各位参考。
#### 1、at指令关机脚本未生效（查询不到）
右键点击脚本，选择“以管理员身份运行”，再打开命令行，输入at指令查询，是否运行成功。
```
at
```
即使以管理员身份运行，有时候脚本也未生效，查询不到。对此，解决方案一是重复上述操作，多执行几次。如果还不行，重启电脑，然后重复上述多次运行操作，亲测有效。

**问题原因：公司的windows系统设置了管理员域用户的权限，所以以正常的user身份无法成功运行脚本；重启是为了避免有其他进程（如杀毒软件）中断了或关闭了脚本进程**

#### 2、SCHTASKS指令关机脚本未生效（查询不到）
SCHTASKS指令脚本未生效的问题背景类似。
右键点击脚本，选择“以管理员身份运行”，再打开命令行，输入SCHTASKS /Query指令查询，是否运行成功。
```
SCHTASKS /Query /tn turnoff（任务名）
```
即使以管理员身份运行，有时候脚本也未生效，查询不到。对此，解决方案一是重复上述操作，多执行几次。如果还不行，重启电脑，然后重复上述多次运行操作，亲测有效。

**问题原因：公司的windows系统设置了管理员域用户的权限，所以以正常的user身份无法成功运行脚本；重启是为了避免有其他进程（如杀毒软件）中断了或关闭了脚本进程**

#### 3、SCHTASKS /Query指令提示“错误：无法加载列资源。”
在命令行中输入SCHTASKS指令时，有可能会遇到这样的报错：“错误：无法加载列资源。”
在命名行中修改语言码制，输入chcp命令，将显示语言改为英文
```
chcp 437
```
再在命令行中输入SCHTASKS /Query指令即可查看到结果。
如果执行命令后
```
SCHTASKS /Query /tn turnoff（任务名）
```
命令行显示“ERROR：The system cannot find the file specified.”，说明turnoff.bat这个脚本并未生效，请参照解决方案2处理。
注意，处于437码制下，命令行窗口只能显示ASCII码字符，所有非ASCII码字符字符会显示为“？”，因此不能看到正常的中文信息（如果你增加了参数来显示中文消息提示、任务名是中文等……）
若之后想把显示语言改回中文，则在命令行中输入
```
chcp 936
```
**问题原因：多语言问题，显示语言设置为简体中文时会报此类错误**
#### 4、脚本生效后未成功执行
在公司的电脑中，部分系统在at脚本指令生效后（可以查询到），到达设置时间时并未自动关机，脚本未能成功执行。
避免此种情况，安装好at脚本后，对脚本进行测试。步骤如下：
将脚本中的定时时间改为此刻的下一分钟，并执行脚本。
确认脚本生效后，等待定时时间到来，如果到时间时，系统提示关机，则at脚本可以成功执行。
如果到时间后，系统并未提示关机，则说明at脚本执行失败。此种情况下，执行SCHTASKS指令脚本，按上述流程操作后，再次测试，会发现SCHTASKS脚本可以成功执行。
**问题原因：未明。怀疑是部分win 7系统虽未提示AT命令已弃用，但实际却不予执行**
