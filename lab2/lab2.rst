.. _lab2:

AHV Networking
+++++++++++++++

Changing Network Bond modes in AHV
-----------------------------------

In this lab we would like to show you what it takes to set your bonds from the default active-backup to balance-slb (active/passive to active/active)

.. figure:: images/ncsc-4.png

Changing Bond from Active/backup to balance-slb
----------------------------------------------------------------------

#. ssh into one of your CVMs

   .. code-block:: bash

     ssh nutanix@CVM-IP

#. To show the bond mode of the host run the following command:

   .. code-block:: bash

    ssh root@192.168.5.1 "ovs-appctl bond/show br0-up"

   Notice the bond_mode should default to active-backup

#. Change the bond mode to balance-slb run the following command:

   .. code-block:: bash

    ssh root@192.168.5.1 "ovs-vsctl set port br0-up bond_mode=balance-slb"

#. Set the recommended rebalance-interval to 30 sec with the following command:

   .. code-block:: bash

    ssh root@192.168.5.1 "ovs-vsctl set port br0-up other_config:bond-rebalance-interval=30000"

#. Verify the proper bond mode again:

   .. code-block:: bash

    ssh root@192.168.5.1 "ovs-appctl bond/show br0-up"

   Notice the next rebalance should be less than 30000ms bond_mode should be balance-slb

#. Repeat steps 1-5 for the remaining CVMs in order to change all ports modes to balance-slb

   .. note::

   	You can set the network mode on all AHV hosts from a single CVM using the ``hostssh`` command (note that the cluster services need to running for this command to work)

    Test usage of ``hostssh`` command

    .. code-block:: bash

      hostssh <command to run on AHV host>

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

      hostssh ovs-appctl bond/show br0-up
      # ============= 10.42.8.27 ============ << 1/4 AHV node
      # ---- br0-up ----
      # bond_mode: active-backup
      # bond may use recirculation: no, Recirc-ID : -1
      # bond-hash-basis: 0
      # updelay: 0 ms
      # downdelay: 0 ms
      # lacp_status: off
      # active slave mac: 0c:c4:7a:59:cf:cf(eth3)
      #
      # slave eth0: disabled
      # 	may_enable: false
      #
      # slave eth1: disabled
      # 	may_enable: false
      #
      # slave eth2: enabled
      # 	may_enable: true
      #
      # slave eth3: enabled
      # 	active slave
      # 	may_enable: true
      #
      # ============= 10.42.8.25 ============ << 2/4 AHV node
      # ---- br0-up ----
      # bond_mode: active-backup
      # bond may use recirculation: no, Recirc-ID : -1
      # bond-hash-basis: 0
      # updelay: 0 ms
      # downdelay: 0 ms
      # lacp_status: off
      # active slave mac: 0c:c4:7a:59:d1:fd(eth3)
      #
      # slave eth0: disabled
      # 	may_enable: false
      #
      # slave eth1: disabled
      # 	may_enable: false
      #
      # slave eth2: enabled
      # 	may_enable: true
      #
      # slave eth3: enabled
      # 	active slave
      # 	may_enable: true
      #
      # ============= 10.42.8.28 ============ << 3/4 AHV node
      # ---- br0-up ----
      # bond_mode: active-backup
      # bond may use recirculation: no, Recirc-ID : -1
      # bond-hash-basis: 0
      # updelay: 0 ms
      # downdelay: 0 ms
      # lacp_status: off
      # active slave mac: 0c:c4:7a:59:d3:7d(eth3)
      #
      # slave eth0: disabled
      # 	may_enable: false
      #
      # slave eth1: disabled
      # 	may_enable: false
      #
      # slave eth2: enabled
      # 	may_enable: true
      #
      # slave eth3: enabled
      # 	active slave
      # 	may_enable: true
      #
      # ============= 10.42.8.26 ============ << 4/4 AHV node
      # ---- br0-up ----
      # bond_mode: active-backup
      # bond may use recirculation: no, Recirc-ID : -1
      # bond-hash-basis: 0
      # updelay: 0 ms
      # downdelay: 0 ms
      # lacp_status: off
      # active slave mac: 0c:c4:7a:59:d3:7f(eth3)
      #
      # slave eth0: disabled
      # 	may_enable: false
      #
      # slave eth1: disabled
      # 	may_enable: false
      #
      # slave eth2: enabled
      # 	may_enable: true
      #
      # slave eth3: enabled
      # 	active slave
      # 	may_enable: true
