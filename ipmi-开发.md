#�ο����ϣ�
http://www.gnu.org/software/freeipmi/
http://netkiller.github.io/monitoring/ipmitool.html
http://www.chenshake.com/summary-of-ipmi/
http://www.openfusion.net/linux/ipmi_on_centos
http://www.ibm.com/developerworks/cn/linux/l-ipmi/

#����
	�鿴������Ϣ��dmidecode | more

	����ƽ̨������棨IPMI��Intelligent Platform Management Interface���ǹ������
	Intel�ṹ����ҵ��ϵͳ����ʹ�õ���Χ�豸���õ�һ�ֹ�ҵ��׼��
	�û��ܹ�����IPMI��ط����������������������¶ȡ���ѹ�����ȹ���״̬����Դ״̬�ȡ�
	�ñ�׼������Ӣ�ض������գ�Hewlett-Packard����NEC�������������Ժ�SuperMicro�ȹ�˾���ơ�
	�µİ汾�� IPMI2.0��http://www.intel.com/design/servers/ipmi/����
##1��������Ӳ�������ṩ�� ipmi ��֧��
	Ŀǰ���ա������� NEC �ȴ�������̵ķ�������֧�� IPMI 2.0��
	�����������з�������֧�֣�����Ӧ����ͨ����Ʒ�ֲ���� BIOS ��ȷ���������Ƿ�֧�� ipmi��
	Ҳ����˵��������������Ҫ���� BMC ��Ƕ��ʽ�Ĺ���΢��������
##2������ϵͳ�ṩ��Ӧ�� ipmi ����
	ͨ������ϵͳ��ط���������� ipmi ��Ϣʱ��Ҫϵͳ�ں��ṩ��Ӧ��֧�֣�
	linux ϵͳͨ���ں˶� OpenIPMI��ipmi ��������֧�����ṩ�� ipmi ��ϵͳ�ӿڡ�
	��ʹ������֮ǰ������������������

	service ipmi start
	��������ģ�飺
	modprobe ipmi_msghandler
	modprobe ipmi_devintf
	modprobe ipmi_si
	modprobe ipmi_poweroff
	modprobe ipmi_watchdog
##3��ipmi ������
	���ǵļ�Ⱥѡ����� Linux �µ������з�ʽ�� ipmi ƽ̨������ ipmitool����http://ipmitool.sourceforge.net/��
	ipmitool ������Ҫͨ����Ӧ��interface������BMC���ڱ��ػ�ȡ��Ϣʱ����õ���-I open��
	��ΪOpenIPMI�ӿڣ�IPMItool��������Ľӿ���open��lan��lanplus��
	����open��ָ����OpenIPMI�� BMCͨ�ţ�Lan��ͨ��Ethernet LAN����IPV4��udpЭ����BMCͨ�š�
	UDP�����ݶΰ�����IPMI request/resoponse��Ϣ����Ϣ����һ��IPMI session ͷ��RMCP ͷ��

	IPMIʹ��Remote Management Control Protocol (RMCP) �汾1֧�ֲ���ϵͳ�رգ�pre-OS��OS-absent����RMCP�Ѱ����ݷ��͵�UDP��623�˿ڡ�
	��lan�ӿ�һ����lanplusͬ��ʹ�� Ethernet LAN ��UDPЭ����BMCͨ�ţ�����lanplusʹ��RMCP��Э�飨��IPMIV20����������ͬ�£�RMCP+����ʹ�øľ�����֤��ʽ�����������Լ�顣
	Open�˿����ڱ��ؼ��ϵͳʹ�õģ�Lan/lanplusͨ���������Զ�̼�ء�

##4��ipmitool���ؼ��ʹ������
	ipmitool -I open command������-I open��ʾʹ��OpenIPMI�ӿڣ�command�������
	a)   raw������һ��ԭʼ��IPMI���󣬲��Ҵ�ӡ�ظ���Ϣ��
	b)   lan���������磨lan���ŵ�(channel)
	c)   chassis ���鿴���̵�״̬�����õ�Դ
	d)   event����BMC����һ���Ѷ�����¼���event���������ڲ������õ�SNMP�Ƿ�ɹ�
	e)   mc��  �鿴MC��Management Contollor��״̬�͸����������
	f)   sdr����ӡ�������ֿ��е��κμ����ʹӴ�������ȡ����ֵ��
	g)   sensor����ӡ����Ĵ�������Ϣ��
	h)   Fru����ӡ�ڽ���Field Replaceable Unit (FRU)��Ϣ
	i)   sel�� ��ӡ System Event Log (SEL)      
	j)   pef�� ���� Platform Event Filtering (PEF)���¼�����ƽ̨�����ڼ��ϵͳ������eventʱ����PEF�еĲ��Խ����¼����ˣ�Ȼ���Ƿ���Ҫ������
	k)   sol/isol����������ͨ�����ڵ�Lan���м��
	l)   user������BMC���û�����Ϣ ��
	m)   channel������Management Controller�ŵ���

	ipmitool -I open sensor list 	 #�����ܹ���ȡ�������еĸ��ּ��ֵ�͸�ֵ�ļ����ֵ��������CPU�¶ȣ���ѹ������ת�٣���Դ����ģ���¶ȣ���Դ��ѹ����Ϣ��
	ipmitool -I open sensor thresh   #����IDֵ����id�ļ����ĸ�������ֵ��
	ipmitool -I open chassis status  #�鿴����״̬�����а����������Դ��Ϣ�����幤��״̬��
	ipmitool -I open chassis restart_cause  �鿴�ϴ�ϵͳ������ԭ��
	ipmitool -I open chassis policy list  �鿴֧�ֵĵ��̵�Դ��ز��ԡ�
	ipmitool -I open chassis power on �������̣��ô������ܹ�Զ�̿���
	ipmitool -I open chassis power off �رյ��̣��ô������ܹ�Զ�̹ػ�
	ipmitool -I open chassis power resetʵ��Ӳ�������ô������ܹ�Զ������
	ipmitool -I open mc reset 	ʹBMC����Ӳ���� 
	ipmitool -I open mc info 	�鿴BMCӲ����Ϣ
	ipmitool -I open mc setenables =[on|off]������bmc��Ӧ������/��ֹѡ�
	ipmitool -I open mc getenables �г�BMC�κ������ѡ��
	ipmitool -I open lan print 1 ��ӡ����channel 1����Ϣ �����channel��̫��Ҫ�ˣ������ҵ�����Ҳ���������ϣ��������Ǿ�����ϸ���⣺

##5��Զ�̻�ȡ�����������Ϣ
	Զ�̻�ȡ�����������Ϣʱ����ҪϵͳӲ��֧��ipmiV1.5��IPMIV2.0��
	��ȡ��Ϣʱ������Ҫ�ڷ������ϰ�װ���������ֻ��Ҫ�ڼ�صĿͻ����ϰ�װipmi�����������ipmitool��
	����Ҫ����Ӧ�����м���Զ�˷����������ֻ��ߵ�ַ��Ipmitool����ͨ��LANԶ�̼��ϵͳ��
	ͬʱBMC�б�����һ�����û��������룬ͨ��LAN����Զ�˷�����Ҫ�û��������롣
	Զ�̻�ȡ�����������Ϣʱ����Ҫ����Զ�̷������ĵ�ַ��ʹ�����µ������ʽ��

	ipmitool -H 169.254.0.2 -U root -P 123456 -I lan command�� 
	-H��ʾ��������Ƿ������ĵ�ַ
	-U��ʾ��������û���
	-P��ʾ��������û�����
	command�ͱ��ػ�ȡ��Ϣ��ͬ

##6�����ñ���BMC��IP���û������� 
	ipmitool -I open lan print 1                             ��ʾBMCͨ������Ϣ�������֪��BMCʹ�õ����ĸ�ͨ������ʹ�����������ȷ�ϣ�
	ipmitool -I open channel info 1							 ��ʾ�ŵ���Ϣ
	ipmitool -I open lan set 1 ipsrc static                  ���ñ���BMC��ַΪ��̬����������IP
	ipmitool -I open lan set 1 ipaddr 192.168.70.233         ���ñ���BMC��IP��ַ
	ipmitool -I open lan set 1 netmask 255.255.255.0         �������룬��������
	ipmitool -I open lan set 1 defgw ipaddr 192.168.70.254   ���أ�����ɲ��裬����һ��Ҫȷ��������Ļ���λ��ͬһ·��

	ipmitool user list 1     �鿴BMC���û��б�
	ipmitool user set name 1 username ��BMC��1���û������û���username
	ipmitool user set password 1 123456 ��BMC��1���û���������123456

	���潲���ҽ������������⣺
	���ڱ���ض����ú���IPMI��ַ���������롢�û����������
	���ǣ��ڼ�ض�ȴ���������ϣ������������Ϣ��
	Error: Unable to establish LAN session
	Get Device ID command failed
	���˰��죬����MAC��ַ�Ϸ�����������
	[root@localhost ~]# ipmitool -I open lan print 1
	Set in Progress         : Set Complete
	Auth Type Support       : NONE MD2 MD5 OEM 
	Auth Type Enable        : Callback : NONE MD2 MD5 OEM 
							: User     : NONE MD2 MD5 OEM 
							: Operator : NONE MD2 MD5 OEM 
							: Admin    : NONE MD2 MD5 OEM 
							: OEM      : 
	IP Address Source       : DHCP Address
	IP Address              : 10.53.11.61
	Subnet Mask             : 255.255.255.0
	MAC Address             : 00:30:48:c9:61:60
	SNMP Community String   : AMI
	IP Header               : TTL=0x00 Flags=0x00 Precedence=0x00 TOS=0x00
	BMC ARP Control         : ARP Responses Enabled, Gratuitous ARP Disabled
	Gratituous ARP Intrvl   : 0.0 seconds
	Default Gateway IP      : 10.53.11.254
	Default Gateway MAC     : 00:00:00:00:00:00
	Backup Gateway IP       : 0.0.0.0
	Backup Gateway MAC      : 00:00:00:00:00:00
	802.1q VLAN ID          : Disabled
	802.1q VLAN Priority    : 0
	RMCP+ Cipher Suites     : 1,2,3,6,7,8,11,12,0
	Cipher Suite Priv Max   : aaaaXXaaaXXaaXX
							:     X=Cipher Suite Unused
							:     c=CALLBACK
							:     u=USER
							:     o=OPERATOR
							:     a=ADMIN
							:     O=OEM

	���ԣ����ڼ�ض˼������MAC��ַ��arp������

	arp -s 10.53.11.28 00:30:48:c9:61:60


 
#һ����Դ��ʵ����openipmi��ipmitool

#����ʹ��ipmitool ���в���
	dntcloud-mgr01:~ # ipmitool user list 1
	Could not open device at /dev/ipmi0 or /dev/ipmi/0 or /dev/ipmidev/0: No such file or directory
	Get User Access command failed (channel 1, user 1)
	dntcloud-mgr01:~ # 

#������Ҫ��������ں�ģ��
	[root@server~]# modprobe ipmi_watchdog
	[root@server~]# modprobe ipmi_poweroff
	[root@server~]# modprobe ipmi_devintf
	[root@server~]# modprobe ipmi_si
	[root@server~]# modprobe ipmi_msghandler
	modprobe ipmi_watchdog ipmi_poweroff ipmi_devintf ipmi_si ipmi_msghandler

	��Ӻ���ԣ�
	dntcloud-mgr01:~ # ipmitool user list 1
	ID  Name	     Callin  Link Auth	IPMI Msg   Channel Priv Limit
	2   root             true    true       true       ADMINISTRATOR
	dntcloud-mgr01:~ # 

#�ġ���������
	dntcloud-mgr01:~ # ipmitool -I lan -H 192.168.70.77 -U root -P superuser chassis power status
	Error: Unable to establish LAN session
	Unable to get Chassis Power Status
	dntcloud-mgr01:~ # 

##192.168.70.166
	heidsoft:~ # modprobe ipmi_si
	FATAL: Error inserting ipmi_si (/lib/modules/3.0.13-0.27-default/kernel/drivers/char/ipmi/ipmi_si.ko): No such device
	heidsoft:~ # 


#�塢��192.168.70.77�ϲ���
##1��ipmitool����IpΪ��̬
	dntcloud-mgr01:~ # ipmitool lan set 1 ipsrc dhcp
	dntcloud-mgr01:~ # ipmitool lan print 1
	Set in Progress         : Set Complete
	Auth Type Support       : NONE MD2 MD5 PASSWORD 
	Auth Type Enable        : Callback : MD2 MD5 
							: User     : MD2 MD5 
							: Operator : MD2 MD5 
							: Admin    : MD2 MD5 
							: OEM      : MD2 MD5 
	IP Address Source       : DHCP Address
	IP Address              : 169.254.0.2
	Subnet Mask             : 255.255.0.0
	MAC Address             : 00:1a:a0:21:f5:3c
	SNMP Community String   : public
	IP Header               : TTL=0x40 Flags=0x40 Precedence=0x00 TOS=0x10
	Default Gateway IP      : 0.0.0.0
	Default Gateway MAC     : 00:00:00:00:00:00
	Backup Gateway IP       : 0.0.0.0
	Backup Gateway MAC      : 00:00:00:00:00:00
	802.1q VLAN ID          : Disabled
	802.1q VLAN Priority    : 0
	RMCP+ Cipher Suites     : 0,1,2,3,4,5,6,7,8,9,10,11,12,13,14
	Cipher Suite Priv Max   : aaaaaaaaaaaaaaa
							:     X=Cipher Suite Unused
							:     c=CALLBACK
							:     u=USER
							:     o=OPERATOR
							:     a=ADMIN
							:     O=OEM
	dntcloud-mgr01:~ # 

##2��ipmitool����IpΪ��̬
	dntcloud-mgr01:~ # ipmitool lan set 1 ipsrc static
	dntcloud-mgr01:~ # ipmitool lan print 1
	Set in Progress         : Set Complete
	Auth Type Support       : NONE MD2 MD5 PASSWORD 
	Auth Type Enable        : Callback : MD2 MD5 
							: User     : MD2 MD5 
							: Operator : MD2 MD5 
							: Admin    : MD2 MD5 
							: OEM      : MD2 MD5 
	IP Address Source       : Static Address
	IP Address              : 0.0.0.0
	Subnet Mask             : 0.0.0.0
	MAC Address             : 00:1a:a0:21:f5:3c
	SNMP Community String   : public
	IP Header               : TTL=0x40 Flags=0x40 Precedence=0x00 TOS=0x10
	Default Gateway IP      : 0.0.0.0
	Default Gateway MAC     : 00:00:00:00:00:00
	Backup Gateway IP       : 0.0.0.0
	Backup Gateway MAC      : 00:00:00:00:00:00
	802.1q VLAN ID          : Disabled
	802.1q VLAN Priority    : 0
	RMCP+ Cipher Suites     : 0,1,2,3,4,5,6,7,8,9,10,11,12,13,14
	Cipher Suite Priv Max   : aaaaaaaaaaaaaaa
							:     X=Cipher Suite Unused
							:     c=CALLBACK
							:     u=USER
							:     o=OPERATOR
							:     a=ADMIN
							:     O=OEM
	dntcloud-mgr01:~ #

##3��ipmitool �����û�����
	ipmitool user set password 2 123456
##4��ipmitool �鿴��Դ״̬
	ipmitool -I lan -H 192.168.70.233 -U root -P 123456 chassis power status
	arp -s 192.168.70.233 00:1a:a0:21:f5:3c
##5��ipmitool ȷ���������� LAN channel
	dntcloud-mgr01:~ # ipmitool -l open channel info 1
	Channel 0x1 info:
		Channel Medium Type   : 802.3 LAN
		Channel Protocol Type : IPMB-1.0
		Session Support       : multi-session
		Active Session Count  : 0
		Protocol Vendor ID    : 7154
		Volatile(active) Settings
		Alerting            : disabled
		Per-message Auth    : disabled
		User Level Auth     : enabled
		Access Mode         : always available
		Non-Volatile Settings
		Alerting            : disabled
		Per-message Auth    : disabled
		User Level Auth     : enabled
		Access Mode         : always available
#���ͼ
##ͼһ
![ipmi-01](./image/ipmi-01.jpg)
##ͼ��
![ipmi-02](./image/ipmi-02.jpg)