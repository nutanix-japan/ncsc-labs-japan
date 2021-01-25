.. _dc_tools_vm:

---------------
Domain Controller Tools VM
---------------

Overview
+++++++++

This VM image will be staged with packages used to support multiple lab exercises.

Deploy this Linux based Domain Controller VM on your assigned cluster if directed to do so as part of **Lab Setup**.

.. raw:: html

  <strong><font color="red">The DC VM is only deployed once by your instructor. Follow these steps to deploy if DC VM is not present in your cluster.</font></strong>

Deploying Domain Controller
++++++++++++++++++++++++++++++++

#. Upload the following image to your cluster using a CVM

#. Logon to the bash shell of a CVM and run the following command:

   .. code-block:: bash

    ssh -l nutanix <CVM IP ADDRESS>
    acli image.create AutoDC container=Images image_type=kDiskImage source_url=http://10.55.251.38/workshop_staging//AutoDC2.qcow2

    .. note::

     If the container ``Images`` doesnt exist in your cluster. Create it using the following commands:

     .. code-block:: bash

        #Obtain your stroage pool ID by running this command

        nutanix@NTNX-15SM65260061-C-CVM:10.42.x.x:~$ ncli sp ls

        # Id                        : 0005a9c2-82e0-d3f0-0000-0000000076ac::`11`
        # Uuid                      : 606d0b93-03d9-4bf6-bae6-b62715d69786
        # Name                      : default-storage-pool-30380

        #Here `11` is your storage pool id (GUID followed by a number)
        #Storage pool ID could different for you

        #Create the Images container
        #Use storage pool ID from the previous commands

        nutanix@NTNX-15SM65260061-C-CVM:10.42.x.x:~$ ctr add sp-id=11 rf=2 enable-compression=true name=Images

#. In **Prism Central** > select :fa:`bars` **> Virtual Infrastructure > VMs**, and click **Create VM**.

#. Fill out the following fields:

   - **Name** - DC
   - **Description** - (Optional) Description for your VM.
   - **vCPU(s)** - 1
   - **Number of Cores per vCPU** - 2
   - **Memory** - 2 GiB
   - Select **+ Add New Disk**
     - **Type** - DISK
     - **Operation** - Clone from Image Service
     - **Image** - AutoDC
     - Select **Add**
   - Select **Add New NIC**
     - **VLAN Name** - Primary
     - Select **Add**

#. Click **Save** to create the VM.

#. Power on the VM.

Verify DC Install and Reset Domain Controller
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

#. Open Console session for your DC VM from Prism Element > VM > DC

#. Watch as the init script is run, and once you see the following screen

   .. figure:: images/dc1.png

#. Note the domain's password displayed on the console - user name is **Administrator**

#. Click anywhere on the console

#. Key in the combination of ``ctrl + x`` in your keyboard

#. You will see the following menu

#. Select **Re-initialize Domain**

   .. figure:: images/dc2.png

#. Select **OK** in the confirmation prompt

#. Domain will re-initalize now

#. You are ready use this domain controller for your labs
