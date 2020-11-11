.. _windows_tools_vm:

----------------
Windows Tools VM
----------------

Overview
+++++++++

This Windows Server 2012 R2 image comes pre-installed with a number of tools, including:

- Microsoft Remote Server Administration Tools (RSAT)
- PuTTY, CyberDuck, WinSCP
- Sublime Text 3, Visual Studio Code
- OpenOffice
- Python
- pgAdmin
- Chocolatey Package Manager

Deploy this VM on your assigned cluster if directed to do so as part of **Lab Setup**.

.. raw:: html

  <strong><font color="red">Only deploy the VM once, it does not need to be cleaned up as part of any lab completion.</font></strong>

Deploying Windows Tools VM
++++++++++++++++++++++++++++++++++++

Upload the following image to your cluster using a CVM

Logon to the bash shell of a CVM and run the following command:

.. code-block:: bash

  ssh -l nutanix <CVM IP ADDRESS>
  acli image.create WinToolsVM container=Images image_type=kDiskImage source_url=http://10.42.194.11/workshop_staging/WinToolsVM.qcow2

.. note::

 If the container ``Images`` doesn't exist in your cluster. Create it using the following commands:

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


In **Prism Central** > select :fa:`bars` **> Virtual Infrastructure > VMs**, and click **Create VM**.

Fill out the following fields:

- **Name** - *Initials*-Windows-ToolsVM
- **Description** - (Optional) Description for your VM.
- **vCPU(s)** - 1
- **Number of Cores per vCPU** - 2
- **Memory** - 4 GiB

- Select **+ Add New Disk**
    - **Type** - DISK
    - **Operation** - Clone from Image Service
    - **Image** - WinToolsVM
    - Select **Add**

- Select **Add New NIC**
    - **VLAN Name** - Primary
    - Select **Add**

Click **Save** to create the VM.

Power on the VM.

Login to the VM via RDP or Console session, using the following credentials:

- **Username** - Administrator
- **password** - nutanix/4u
