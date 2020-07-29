#### **FBox-4G-VPN透传-ABMicro850**  

测试环境  
操作系统：win7 64位  
软件：CCW8.0,RSLinx3.71  

1.首先设置FBox-4G上线  
使用最新版FS软件，设置使用“GPRS/3G/4G远程连接”，任意固定ip即可，用USB下载到FBox-4G中  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABERM1.png)  

2.准备好4GSIM卡（大卡），网络支持4G（移动/联通/电信）、3G（移动/联通）、2G（移动/联通），卡槽边上按钮弹出卡槽，将卡插入卡槽中，使用4G专用天线，上电等待RF灯常亮  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABERM2.png)  

3.启动“FlexManager”客户端  
客户端显示FBox-4G已经上线后，点击“远程下载”，使用“VPN透传”，输入和现场PLC同网段的IP，点击“连接”，等待连接状态显示“VPN透传已经准备好”即可。例如PLC的IP地址是192.168.11.11，我们在VPN里设置的IP为192.168.11.21，只要同网段且不与现场冲突的IP即可。  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABERM3.png)![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABERM4.png)  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABERM5.png)  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABERM6.png)  

4.首先打开RSLinx，然后打开CCW软件，点击“连接”，选择plc后，点击下方的确认，确认下载即可  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABMicro1.png)  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABMicro2.png)  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABMicro3.png)  

![添加盒子分组](../Images/Trans/TranExplain/AB1769L36ERM/ABMicro4.png)  
