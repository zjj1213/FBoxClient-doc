#### **FBox-4G-VPN透传-西门子1500**  

测试环境  
操作系统：win7 64位  
软件：PORATL v13 sp1  

1.首先设置FBox-4G上线  
使用最新版FS软件，设置使用“GPRS/3G/4G远程连接”，任意固定ip即可，用USB下载到FBox-4G中  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABERM1.png)  

2.准备好4GSIM卡（大卡），网络支持4G（移动/联通/电信）、3G（移动/联通）、2G（移动/联通），卡槽边上按钮弹出卡槽，将卡插入卡槽中，使用4G专用天线，上电等待RF灯常亮  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABERM2.png)  

3.启动“FlexManager”客户端，客户端显示FBox-4G已经上线后，点击“远程下载”，使用“VPN透传”,输入和现场PLC同网段的IP，点击“连接”，等待连接状态显示“VPN透传已经准备好”即可。例如PLC的IP地址是192.168.11.11，我们在VPN里设置的IP为192.168.11.21，只要同网段且不与现场冲突的IP即可  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/MP1.png)  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/MP2.png)  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/MP3.png)  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/MP4.png)  

4.打开PROATL V13 SP1软件，选择PLC，设置好IP地址，点击下载按钮，PG/PC接口类型选择PN/IE，PG/PC接口选择VPN透传专用网卡“TAP-Win32 Adapter V9”，在下方的设备地址处手动输入PLC的IP地址，然后点击空白处，等待连接。建立好连接后，直接点击下载即可。  

![添加盒子分组](../Images/Trans/TranExplain/STEP7MicroWIN/PORATL10.png)  
![添加盒子分组](../Images/Trans/TranExplain/STEP7MicroWIN/PORATL11.png)  
![添加盒子分组](../Images/Trans/TranExplain/STEP7MicroWIN/PORATL12.png)  
