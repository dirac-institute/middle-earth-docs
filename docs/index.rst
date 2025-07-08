
.. middleearthdocs documentation main file.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Middle Earth's documentation!
========================================================================================

Getting Started
---------------------------

If you had access to ``epyc`` you also have access to Middle Earth. If you need access contact mjuric@uw.edu with your UW NetID.

Basic Jupyterhub and shell access are as follows:

* `Arnor Juptyerhub <https://arnor.astro.washington.edu/jupyter>`_
* `Gondor Jupyterhub <https://gondor.astro.washington.edu/jupyter>`_
* Arnor SSH: ``ssh -CYA <NetID>@arnor.astro.washington.edu``
* Gondor SSH: ``ssh -CYA <NetID>@gondor.astro.washington.edu``

Data access
-----------------------------
Home directories are your astro home directory, the same one as was available from epyc.

You have access to all of your files from ``epyc`` at ``/astro/store/`` on either machine.

System Specs
------------------------------

.. list-table:: Compute Nodes
   :header-rows: 1

   * - | Hostname
     - | CPUs
     - | Mem
     - | GPUs
     - | GPU Mem
       | (Per GPU)
     - | Network 
       | Speed
   * - `Arnor <https://arnor.astro.washington.edu/jupyter>`_
     - | 128 core 
       | EPYC 9555
     - 1536 GB
     - N/A
     - N/A
     - 10 Gbps
   * - `Gondor <https://gondor.astro.washington.edu/jupyter>`_
     - | 128 core 
       | EPYC 9555
     - 768 GB 
     - 2 x NVIDIA L40
     - 48 GB
     - 1 Gbps

.. list-table:: Storage Locations
   :header-rows: 1

   * - | Directory 
     - | Total Space
     - | Served By
     - | Network 
       | (general)
     - | Storage 
       | Hardware
   * - `/astro/store/epycn`
     - 11 TB
     - Epyc
     - 10 Gbps
     - NVME SSD
   * - `/astro/store/epyc`
     - 145 TB
     - Epyc
     - 10 Gbps

     - JBOD
   * - `/astro/store/epyc2`
     - 175 TB
     - Epyc
     - 10 Gbps

     - JBOD
   * - `/astro/store/epyc3`
     - 393 TB
     - Epyc
     - 10 Gbps
     - JBOD   
   * - `/astro/store/epyc4`
     - 241 TB
     - Epyc
     - 10 Gbps
     - JBOD
   * - N/A
     - 1.4 PB
     - Shire
     - | 1 Gbps (internet)
       | 100 Gbps (Arnor)
       | 100 Gbps (Gondor)
     - RAID 6+0
     


.. toctree::
   :hidden:

   Home page <self>