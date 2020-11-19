

.. _lab5:

.. title:: Fit Check Services

Run diagnostics.py
++++++++++++++++++++++++++++++

#. SSH to CVM

   .. code-block:: bash

    ssh -l nutanix <CVM IP ADDRESS>

#. Run the following script

   .. code-block:: bash

     /home/nutanix/diagnostics/diagnostics.py run

#. View output from the following directory ``/home/nutanix/diagnostics/results``

#. Run script script to cleanup files generated during diagnostics

   .. code-block:: bash

     /home/nutanix/diagnostics/diagnostics.py cleanup

#. Review the output

Run Nutanix X-Ray
++++++++++++++++++++++++++++++

.. note::
 If X-Ray is already deployed in your labs skip Steps 1-5

#. Go to Nutanix Support Portal (https://portal.nutanix.com/page/downloads/list)

   .. figure:: images/xray1.png

#. Download latest X-Ray version for AHV

   .. figure:: images/xray2.png

#. Import the QCOW2 image v-disk into **Image Configurations** in **Settings** menu

#. Build a new VM with 8 vCPUs, 1 Core, and 8GB RAM

#. Clone the new disk from to Image Service

#. Add a NIC and power on VM

#. The VM should pickup an IP and you can browse to that IP to access XRAY

#. Run the “Four Corners Microbenchmark” tests to get an idea of just one of the many tests that X-RAY can provide. This should take about 20 minutes to run.

#. You can export the output to document and review the output.

Run Nutanix Collector
++++++++++++++++++++++++++++++

#. Download “Nutanix Collector” from Support Portal

   .. figure:: images/collector.png

#. Extract the package and launch application

#. Choose the IP of the cluster and correct port and Username and password and choose **Connect**

#. Review the output and how it could be useful for most fit check services

Run NCC Healthchecks
++++++++++++++++++++++++++++++

#. SSH to CVM and run the following command

   .. code-block:: language

     ncc heath_check run_all

#. NCC output logs can be found in the following path on the CVM : ``/home/nutanix/data/logs/ncc-output.log``

   .. note::

   	Note how you can repeat and run individual tests.  Identify how to gather resolution steps and solutions for your Fit Check report.
