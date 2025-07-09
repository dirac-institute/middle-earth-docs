
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

Shared Resources
-----------------------------
Middle Earth is a shared resource with no automated means of allocation. You can check on current usage directly at a 
Jupyterhub console or over SSH.

Compute
^^^^^^^
You can use ``top`` to check on CPU Usage. Usernames and unix process ids of the processes using the most memory 
and CPU are displayed. The load average displayed is a measure of how many processes are running or waiting for a CPU, and is the 
best measure for whether you will be able to get CPU time for your process. You can learn more about load averages 
`from this blog post <https://www.brendangregg.com/blog/2017-08-08/linux-load-averages.html>`_.

If compute nodes run out of CPU, they will generally run slowly.


Memory
^^^^^^
You can use ``free -h`` to see a readout of the free memory on Linux. ``top`` can give you some hints on which processes are 
using memory (Look at the RES column); however, ``free -h`` is better for system-wide statistics. For more info on linux memory 
usage consult `this blog post <https://linuxblog.io/free-vs-available-memory-in-linux/>`_.

If compute nodes run out of memory, they will usually run slowly for a time and then linux will kill processes in order to free 
up memory.


GPUs
^^^^
On GPU nodes you can use ``nvidia-smi -l 1`` to show a looping readout of the compute and memory utilization across all GPUs on 
the system. Processes and owning users are also shown in this view. For more information on how to query GPU data at the command 
line consult `this Nvidia support article <https://enterprise-support.nvidia.com/s/article/Useful-nvidia-smi-Queries-2>`_.

If there are no available GPU resources, programs that use the GPU will experience errors. Many GPU enabled programs allow you to 
choose which device they run on. If you are experiencing errors running a GPU enabled program you might try running it on a 
different GPU.

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
   * - *Coming Soon...*
     - 1.4 PB
     - Shire
     - | 1 Gbps (internet)
       | 100 Gbps (Arnor)
       | 100 Gbps (Gondor)
     - RAID 6+0
     


.. toctree::
   :hidden:

   Home page <self>