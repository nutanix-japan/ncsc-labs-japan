.. _command_reference:

.. title:: Nutanix Certified Services Consultant - Command References

Generic AHV/ESX and CVM Commands Reference
+++++++++++++++++++++++++++++++++++++++++++

These commands are used to execute the same command on all the hypervisor nodes or CVM in a Nutanix Cluster. These commands will only work if the Nutanix cluster services are up and running in all CVM(s).

- `allssh` - used to execute a command on all CVMs and
- `hostssh`- used to execute a command on all hypervisor nodes

.. caution::

  Use these commands with extreme caution as it will affect all the hypervisor nodes and CVMs in a cluster causing data loss.
  You will need to understand the command before actually running it. Nutanix recommends that these are only used if you are an advanced user and can take responsibility for your actions.

Some examples for ``hostssh`` commands:

.. code-block:: bash

  hostssh <command to run on AHV host>

  # this command gets the OS version of all AHV hosts in the Nutanix cluster

  hostssh uname -a  #this will return the OS version on all AHV hosts

  #the command output will look as follows:

  # ============= 10.42.8.27 ============
  # Linux PHX-POC008-3 4.4.77-1.el6.nutanix.20170830.301.x86_64 #1 SMP Wed Jun 26 17:05:47 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
  # ============= 10.42.8.25 ============
  # Linux PHX-POC008-1 4.4.77-1.el6.nutanix.20170830.301.x86_64 #1 SMP Wed Jun 26 17:05:47 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
  # ============= 10.42.8.28 ============
  # Linux PHX-POC008-4 4.4.77-1.el6.nutanix.20170830.301.x86_64 #1 SMP Wed Jun 26 17:05:47 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
  # ============= 10.42.8.26 ============
  # Linux PHX-POC008-2 4.4.77-1.el6.nutanix.20170830.301.x86_64 #1 SMP Wed Jun 26 17:05:47 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux

  # this command gets all IPMI settings from all the hypervisor nodes in a cluster

  hostssh ipmitool lan print 1
  #
  # ============= 10.42.8.27 ============
  # Set in Progress         : Set Complete
  # Auth Type Support       : NONE MD2 MD5 PASSWORD
  # Auth Type Enable        : Callback : MD2 MD5 PASSWORD
  #                         : User     : MD2 MD5 PASSWORD
  #                         : Operator : MD2 MD5 PASSWORD
  #                         : Admin    : MD2 MD5 PASSWORD
  #                         : OEM      : MD2 MD5 PASSWORD
  # IP Address Source       : Static Address
  # IP Address              : 10.42.8.35
  # Subnet Mask             : 255.255.255.128
  # MAC Address             : 0c:c4:7a:66:fa:f0
  # SNMP Community String   : public
  # IP Header               : TTL=0x00 Flags=0x00 Precedence=0x00 TOS=0x00
  # BMC ARP Control         : ARP Responses Enabled, Gratuitous ARP Disabled
  # Default Gateway IP      : 10.42.8.1
  # Default Gateway MAC     : 00:1c:73:00:00:99
  # Backup Gateway IP       : 0.0.0.0
  # Backup Gateway MAC      : 00:00:00:00:00:00
  # 802.1q VLAN ID          : Disabled
  # 802.1q VLAN Priority    : 0
  # RMCP+ Cipher Suites     : 1,2,3,6,7,8,11,12
  # Cipher Suite Priv Max   : XaaaXXaaaXXaaXX
  #                         :     X=Cipher Suite Unused
  #                         :     c=CALLBACK
  #                         :     u=USER
  #                         :     o=OPERATOR
  #                         :     a=ADMIN
  #                         :     O=OEM
  # Bad Password Threshold  : Not Available
  # ============= 10.42.8.25 ============
  # Set in Progress         : Set Complete
  # Auth Type Support       : NONE MD2 MD5 PASSWORD
  # Auth Type Enable        : Callback : MD2 MD5 PASSWORD
  #                         : User     : MD2 MD5 PASSWORD
  #                         : Operator : MD2 MD5 PASSWORD
  #                         : Admin    : MD2 MD5 PASSWORD
  #                         : OEM      : MD2 MD5 PASSWORD
  # IP Address Source       : Static Address
  # IP Address              : 10.42.8.33
  # Subnet Mask             : 255.255.255.128
  # MAC Address             : 0c:c4:7a:3d:37:30
  # SNMP Community String   : public
  # IP Header               : TTL=0x00 Flags=0x00 Precedence=0x00 TOS=0x00
  # BMC ARP Control         : ARP Responses Enabled, Gratuitous ARP Disabled
  # Default Gateway IP      : 10.42.8.1
  # Default Gateway MAC     : 00:1c:73:00:00:99
  # Backup Gateway IP       : 0.0.0.0
  # Backup Gateway MAC      : 00:00:00:00:00:00
  # 802.1q VLAN ID          : Disabled
  # 802.1q VLAN Priority    : 0
  # RMCP+ Cipher Suites     : 1,2,3,6,7,8,11,12
  # Cipher Suite Priv Max   : XaaaXXaaaXXaaXX
  #                         :     X=Cipher Suite Unused
  #                         :     c=CALLBACK
  #                         :     u=USER
  #                         :     o=OPERATOR
  #                         :     a=ADMIN
  #                         :     O=OEM
  # Bad Password Threshold  : Not Available
  # ============= 10.42.8.28 ============
  # Set in Progress         : Set Complete
  # Auth Type Support       : NONE MD2 MD5 PASSWORD
  # Auth Type Enable        : Callback : MD2 MD5 PASSWORD
  #                         : User     : MD2 MD5 PASSWORD
  #                         : Operator : MD2 MD5 PASSWORD
  #                         : Admin    : MD2 MD5 PASSWORD
  #                         : OEM      : MD2 MD5 PASSWORD
  # IP Address Source       : Static Address
  # IP Address              : 10.42.8.36
  # Subnet Mask             : 255.255.255.128
  # MAC Address             : 0c:c4:7a:3c:cb:f1
  # SNMP Community String   : public
  # IP Header               : TTL=0x00 Flags=0x00 Precedence=0x00 TOS=0x00
  # BMC ARP Control         : ARP Responses Enabled, Gratuitous ARP Disabled
  # Default Gateway IP      : 10.42.8.1
  # Default Gateway MAC     : 00:1c:73:00:00:99
  # Backup Gateway IP       : 0.0.0.0
  # Backup Gateway MAC      : 00:00:00:00:00:00
  # 802.1q VLAN ID          : Disabled
  # 802.1q VLAN Priority    : 0
  # RMCP+ Cipher Suites     : 1,2,3,6,7,8,11,12
  # Cipher Suite Priv Max   : XaaaXXaaaXXaaXX
  #                         :     X=Cipher Suite Unused
  #                         :     c=CALLBACK
  #                         :     u=USER
  #                         :     o=OPERATOR
  #                         :     a=ADMIN
  #                         :     O=OEM
  # Bad Password Threshold  : Not Available
  # ============= 10.42.8.26 ============
  # Set in Progress         : Set Complete
  # Auth Type Support       : NONE MD2 MD5 PASSWORD
  # Auth Type Enable        : Callback : MD2 MD5 PASSWORD
  #                         : User     : MD2 MD5 PASSWORD
  #                         : Operator : MD2 MD5 PASSWORD
  #                         : Admin    : MD2 MD5 PASSWORD
  #                         : OEM      :
  # IP Address Source       : Static Address
  # IP Address              : 10.42.8.34
  # Subnet Mask             : 255.255.255.128
  # MAC Address             : 0c:c4:7a:3d:32:85
  # SNMP Community String   : public
  # IP Header               : TTL=0x40 Flags=0x40 Precedence=0x00 TOS=0x10
  # BMC ARP Control         : ARP Responses Enabled, Gratuitous ARP Disabled
  # Default Gateway IP      : 10.42.8.1
  # Default Gateway MAC     : 00:1c:73:00:00:99
  # Backup Gateway IP       : 0.0.0.0
  # Backup Gateway MAC      : 00:00:00:00:00:00
  # 802.1q VLAN ID          : Disabled
  # 802.1q VLAN Priority    : 0
  # RMCP+ Cipher Suites     : 1,2,3,6,7,8,11,12
  # Cipher Suite Priv Max   : XaaaXXaaaXXaaXX
  #                         :     X=Cipher Suite Unused
  #                         :     c=CALLBACK
  #                         :     u=USER
  #                         :     o=OPERATOR
  #                         :     a=ADMIN
  #                         :     O=OEM
  # Bad Password Threshold  : Not Available

Some examples for ``allssh`` (CVM) commands:

.. code-block:: bash

  allssh <command to run on AHV host>

  # run this to list log files on all CVM(s)

  allssh ls -l /home/nutanix/*.log

  # ================== 10.42.8.29 =================
  # -rw-------. 1 nutanix nutanix 333 Aug 25 02:29 /home/nutanix/ncli.log
  # ================== 10.42.8.30 =================
  # ls: cannot access /home/nutanix/ncli.log: No such file or directory
  # ================== 10.42.8.32 =================
  # ls: cannot access /home/nutanix/ncli.log: No such file or directory
  # ================== 10.42.8.31 =================
  # -rw-------. 1 nutanix nutanix 3137 Sep 25 10:47 /home/nutanix/ncli.log

  # run this to get dates on all CVM(s)

  allssh date

  #  ================== 10.42.8.29 =================
  # Tue Oct 20 07:28:41 UTC 2020
  # ================== 10.42.8.30 =================
  # Tue Oct 20 07:28:42 UTC 2020
  # ================== 10.42.8.32 =================
  # Tue Oct 20 07:28:42 UTC 2020
  # ================== 10.42.8.31 =================
  # Tue Oct 20 07:28:43 UTC 2020

  # run this to get NTP sync. status on all CVM(s)

  allssh ntpq -pn

  # ================== 10.42.8.29 =================
  #      remote           refid      st t when poll reach   delay   offset  jitter
  # ==============================================================================
  # *10.42.8.30      216.126.233.109  3 u   28 1024  377    0.815    1.138   0.739
  # ================== 10.42.8.30 =================
  #      remote           refid      st t when poll reach   delay   offset  jitter
  # ==============================================================================
  # *216.126.233.109 128.227.205.3    2 u  596 1024  267   63.850    1.126   0.512
  #  127.127.1.0     .LOCL.          10 l  24d   64    0    0.000    0.000   0.000
  # ================== 10.42.8.32 =================
  #      remote           refid      st t when poll reach   delay   offset  jitter
  # ==============================================================================
  # *10.42.8.30      216.126.233.109  3 u  361 1024  377    0.719    1.073   0.416
  # ================== 10.42.8.31 =================
  #      remote           refid      st t when poll reach   delay   offset  jitter
  # ==============================================================================
  # *10.42.8.30      216.126.233.109  3 u  699 1024  377    0.854    1.238   0.451
