.. _lab3:

.. title:: Nutanix Certified Services Consultant - Lab 3

VM Migration
+++++++++++++

Manually Import a ESXi Virtual Disk
------------------------------------

.. note::

	This lab is important as you may need to import a Virtual Disk manually.  The steps are generally the same to import vDisks into Nutanix AHV.

  This is optional as tools like **Nutanix Move** will be used in most cases

A Prepare the VM on the ESXi host was installed with Nutanix VirtIO drivers
------------------------------------------------------------------------------------------------------------

#. Add the source hypervisor host IP address to the target AHV cluster Filesystem Whitelist.

#. Use can use Storage vMotion for the VM disks to Nutanix AHV container datastore.

Converting the Migrated Disks to AHV Format
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. In the Prism UI, click **Settings > Image** Configuration.

#. In the Image Configuration Dialog Box, click **Upload the Image**

#. In the Create Image dialog box, complete the indicated fields

#. Log in to the Prism UI using your Nutanix credentials

#. At the top left corner, click **Home > VM**  The VM page appears

#. Click **+ Create VM** in the corner of the page

#. Provide Name for the VM

#. Enter *2* as **vCPU** and *1* as **Number Of Cores Per vCPU**

#. Enter *4* as **Memory**

#. Click on **+Add New Disk**

   .. figure:: images/ncsc-6.png

#. Choose **Disk** as **Type** and **Operation** as **Clone From Image Service**

#. Click the drop-down menu and choose the image you created previously

   .. figure:: images/ncsc-7.png

#. Click **Add**

#. Click on **Save** in the main VM creation menu

#. Power on VM
