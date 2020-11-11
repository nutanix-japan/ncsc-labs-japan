.. _lab2:

.. title:: Nutanix Certified Services Consultant - Lab 2

AHV Networking
+++++++++++++++

Changing Network Bond modes in AHV
-----------------------------------

In this lab we would like to show you what it takes to set your bonds from the default active-backup to balance-slb (active/passive to active/active)

.. figure:: images/ncsc-4.png

Changing Bond from Active/backup to `balance-slb`
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

   	You can set the network mode on all AHV hosts from a single CVM using the ``hostssh`` command (note that the cluster services need to running for this command to work).

    See :ref:`all_host_ssh` for command reference.

Setting the VLANs from command line (Optional Reference Lab)
-------------------------------------------------------------

.. note::

  This lab is important as you will need to change the VLANs when systems are in Trunked production networks this is the case with most production environments.

  It’s recommend connecting by remote console in IPMI because you may lose connection if you are SSH into the node.


#. Assign port br0 to the VLAN that you want the host be on.

.. code-block:: bash

  root@ahv# ovs-vsctl set port br0 tag=host_vlan_tag #(w/VLAN tag for hosts.)

#. Confirm VLAN tagging on port br0.

.. code-block:: bash

  root@ahv# ovs-vsctl list port br0

#. From host console Log on to the Controller VM.

.. code-block:: bash

  root@host# ssh nutanix@192.168.5.254

#. Assign the public interface of the Controller VM to a VLAN.

.. code-block:: bash

  nutanix@cvm$ change_cvm_vlan vlan_id #(w/VLAN tag for CVM)

VM Snapshot Management
+++++++++++++++++++++++

Local Snapshot and Recovery
------------------------------------------

For this lab you will need some test virtual machines. Follow the steps to create new VM.

#. Locate Windows 2012 VM and add a CDROM

   Click **Update**

   Click **+Add New Disk** under Disks

#. Choose **CDROM**

#. Power on the Windows2012 VM

#. Launch Console and configure windows 2012

#. Login and verify it is on the network

#. Install NGT:

   Click the Windows 2012 VM and choose **Manage Guest Tools**

   Select all options and click **Submit**

   .. figure:: images/ncsc-5.png

#. From the System browse to the CDROM drive and run the installation with all defaults

#. Eject CDROM

#. Create two clones of this system to have more test systems

Purpose: Explore the rich set of integrated data protection and disaster recovery capabilities in the Nutanix solution.

#. Log into Prism

#. Click on **+ Protection Domain** button > **Async DR**

#. Create a protection domain with a unique name by going through the wizard

#. Name the protection domain **PD-Prod**

#. Choose VMs to include in the protection domain

#. Choose the cloned VM you created in the last lab

#. Choose “Protect Selected Entities” click Next

#. Click “New Schedule” Setup a schedule for the protection domain

#. Choose **Repeat every 1 day**

#. Create Schedule

#. Click on **close**

#. Simulate a few days of snapshots by selecting the Async DR you created in table view

#. Select **Take Snapshot** and hit **save** and repeat a few times.

   - Hint: You may modify the VM so that you can snapshot different version of your VM

   - Under “Local Snapshots” for this Protection Domain you should see a few listed

We will now restore VM from Replication:

#. Select the Protection Domain containing the VM snapshot

#. Choose the Local Snapshot under **Local Snapshots** with the timestamp and click **Restore**

#. Choose all VMs or just certain VMs that you wish to restore

#. Create new entities:

   - Choose to create new entity to restore to a new VM. (Prefix: Nutanix-Clone-)
   - Look at VMs to see there are new VMs restore from your snapshots

#. Overwrite Existing Entities (remember to use a clone to have a copy of your VM):

   - Choose to overwrite your VM while online
   - The VM should boot into the VM at the point in time of the snapshot.

Self Service Restore (SSR)
---------------------------

#. Console to your VM

#. Launch SSR Icon from the desktop

#. Login with your local administrator account

#. Notice you should see all snapshots available to you for that VM

#. Select a snapshot and choose to mount it as a drive letter

#. Windows File Explorer should see the snapshot as a local drive

#. Unmount and exit

Replicate to Remote Site & Recover Remote and Migrate/Activate
---------------------------------------------------------------

Follow these steps to create a Remote Site to replicate to.

#. From Data Protection Click **Remote Site** and select **Physical Cluster**

#. Give Remote Site a name **<Your Initials-REMOTE>**

#. Choose Capabilities **Disaster Recovery** this will allow Remote Recovery

#. Enter the IP address  of your partners cluster and choose **Add Site**

#. Choose Cluster to Cluster network mapping

#. Choose vStore A to VStore B.

.. note::

You must make a remote site from your partners cluster to your cluster and they should go from vStore B to vStore A

Modify your Data Protection Group
---------------------------------------------------------------

#. Select your Protection Domain and click **update**

#. Modify your Schedule and you will now see a remote site

#. Select to keep last 30 on Remote site

#. Then click **Create Schedule**

Take a few snapshots
---------------------------------------------------------------

#. Select your Protection Domain

#. Click **Take Snapshot**

#. Make sure the Remote site is selected and hit Save

#. Repeat step 2 & 3 a few times (at least 5 times)

#. The first replication should take the longest, click under “Replications” to watch the status


Restoring from Remote Snapshots
---------------------------------------------------------------

When replications are done, a full copy and its deltas are sent to the remote site.

To recover remote snapshot from local site A:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Select **Remote Snapshots**

#. Select a remote snapshot to bring back as a local snapshot for local recovery

Snapshot to Remote Site & use Migrate/Activate
---------------------------------------------------------------

Scenario #1: To move the VM from site A to Site B
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. From Site A, select your Protection Domain

#. Choose **Migrate** and notice all the VMs in that Protection Domain should be removed from Site A and powered on in Site B (Fail-Over)

#. Feel free to continue work on the VM and make changes and repeat those steps 1&2 to migrate the Protection Domain back to Site A (Fail-Back)

Scenario #2: when Site A has Failed and went down on its own and you want to bring it back online in Site B
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. From Site B, select your Protection Domain

#. Choose **Activate**

#. This will bring the protection domain’s VMs online on remote site

   .. note::

     you may need to power on the VMs after activation of the Protection Domain

#. When Site A is considered back online the Migrate button should now be able to send the latest back to Site A

Snapshot to Remote Site
---------------------------------------------------------------

Recover a snapshot at Remote Site B
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. From the site B look at “local snapshots”
#. Recover one of your snapshots in Site B


Run NCC Healthchecks
---------------------------------------------------------------

#. SSH to CVM and run the following command

   .. code-block:: language

     ncc heath_check run_all

#. NCC output logs can be found in the following path on the CVM : ``home/nutanix/data/logs/ncc-output.log``

   .. note::

   	Note how you can repeat and run individual tests.  Identify how to gather resolution steps and solutions for your Fit Check report.
