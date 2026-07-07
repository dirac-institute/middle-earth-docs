****************************
Other UW HPC for DiRAC
****************************

Hyak Klone
^^^^^^^^^^
Through the Astronomy Department, DiRAC has 30 slices of Klone distributed between 
``cpu-g2``, ``cpu-g2-mem2x``, and ``compute-bigmem`` `type nodes <https://hyak.uw.edu/docs/compute/start-here#partitions>`_. 
`Checkpoint resources <https://hyak.uw.edu/docs/compute/checkpoint>`_ are available on Klone as well to astro users.

To be added to the astro departmental group e-mail one 
(or all) of ajc26@uw.edu (Andy Connolly), jrad@uw.edu (Jim Davenport) or mjuric@uw.edu (Mario Juric). 
Specify the NetID, who they’re working with, and a brief explanation (1 sentence) of why access is needed.

.. warning ::

    Klone is known to have a slow filesystem. Only around 4000 IOPS can be sustained across all users at the University.
    Packing your conda environment or research data into a small number of large files is preferable. Compressing these directories
    of small files and copying them to/from the node's local filesystem in your slurm script will help, as will containerizing your 
    job using `apptainer/singularity <https://hyak.uw.edu/docs/tools/containers#apptainer-formerly-singularity>`_ or 
    `ngc <https://hyak.uw.edu/docs/gpus/nvidia_ngc>`_


At the moment there is no high-bandwidth communication channel for files between Hyak and Middle Earth, your best bet is rsync. 
Hyak currently has `globus connectivity <https://hyak.uw.edu/docs/storage/globus/>`_, but Middle Earth does not.


Hyak Tillicum
^^^^^^^^^^^^^

`Tillicum <https://hyak.uw.edu/docs/tillicum/architecture/>`_ offers GPUs for $0.90/ GPU hr. DiRAC institute has an account 
which is accessible by emailing ajc26@uw.edu (Andy Connolly) with your UW NetID and a short rationale for why access is needed.

The DiRAC account has a hard usage cap of $1000/mo account-wide and soft usage caps of $200/mo on each account. Current settings
can be checked with the ``hyakusage`` `command <https://hyak.uw.edu/docs/tillicum/monitoring-jobs#budget-enforcement>`_ 

.. note ::

    If you need to get in touch directly with Hyak admins, you can use the 
    `Research computing club Slack <https://depts.washington.edu/uwrcc/>`_, 
    `Office hours <https://calendar.washington.edu/sea_uwit-rc>`_, or file a ticket thorugh help@uw.edu with "Hyak" 
    in the subject line

Epyc
^^^^

Epyc is the legacy compute system which Middle Earth is superceding. An overview of Epyc's capabilities is 
`available here. <https://drive.google.com/drive/u/0/folders/15oxHVrO6TubKwO9J1ofzXln7p4dzxeS5>`_
