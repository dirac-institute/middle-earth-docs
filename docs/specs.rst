************
System Specs
************


Compute Nodes
-------------

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
     - | 2x64 core 
       | EPYC 9555
       | @ 3.2 Ghz
     - 1536 GB
     - N/A
     - N/A
     - 10 Gbps
   * - `Gondor <https://gondor.astro.washington.edu/jupyter>`_
     - | 1x64 core 
       | EPYC 9555 
       | @ 3.2 Ghz
     - 768 GB 
     - 2 x NVIDIA L40
     - 48 GB
     - 1 Gbps


Storage Locations
-----------------

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
   * - `/astro/store/shire`
     - 1.4 PB
     - Shire
     - 100 Gbps
     - RAID 6+0
   * - `/astro/store/shiren`
     - 7 TB
     - Shire
     - 100 Gbps
     - NVME SSD
     