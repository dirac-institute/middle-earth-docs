#################
Check Utilization
#################
Middle Earth is a shared resource with no automated means of allocation such as ``slurm`` or ``condor``. You can check on current usage directly at a 
Jupyterhub console or over SSH.

Storage
^^^^^^^

You can see a quick readout of shared filesystem utilization with ``df -h | grep -vE 'user|tmp|efi'``. When run on ``arnor`` or 
``gondor`` you will see something like this:

.. code-block:: text

    $ df -h | grep -vE 'user|tmp|efi'
    Filesystem        Size  Used Avail Use% Mounted on
    /dev/nvme0n1p2     64G   13G   52G  20% /
    /dev/nvme0n1p4    798G  7.1G  791G   1% /local
    epyc:/data/epyc   146T  145T  823G 100% /astro/store/epyc
    epyc:/nvme         11T  8.0T  2.6T  77% /astro/store/epycn
    epyc:/data3/epyc  393T  385T  8.2T  98% /astro/store/epyc3
    epyc:/data4/epyc  241T  240T  339G 100% /astro/store/epyc4
    epyc:/data2/epyc  175T  155T   20T  89% /astro/store/epyc2

Note that the first entry which is mounted on ``/`` is the boot drive. **Filling up the 
boot drive will cause the compute node to become unstable for other users**. 

If you are trying to figure out which filesystem a file is located on, run ``df -h <filename>`` which will return a single line 
table showing you the relevant filesystem and that filesystem's availability statistics. See below:

.. code-block:: text

    $ df -h filename.txt
    Filesystem      Size  Used Avail Use% Mounted on
    epyc:/nvme       11T  8.0T  2.6T  77% /astro/store/epycn

If you want to know how big a set of files is, you can use the ``du`` utility to count up the size of files on disk. **Beware this 
may take a long time** if you are counting up the space usage of many small files. For example:

.. code-block:: text

    $ du -sh my-research-directory
    234G	my-research-directory

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