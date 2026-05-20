****************************
Other Compute
****************************

Hyak Klone
^^^^^^^^^^
DiRAC has a general use allocation of 30 slices of Klone distributed between ``cpu-g2`` and ``cpu-g2-mem2x`` type nodes. 
Avoid using the ``cpu-bigmem`` slice unless you are Ben William's student or otherwise have his permission.
Checkpoint resources are available on Klone as well to astro users. 

To be added to the astro departmental group e-mail one 
(or all) of ajc26@uw.edu (Andy Connolly), jrad@uw.edu (Jim Davenport) or mjuric@uw.ed (Mario Juric). 
Specify the NetID, who they’re working with, 
and a brief explanation (1 sentence) of why access is needed.

Klone is known to have a slow filesystem. Only around 4000 IOPS can be sustained across all users at the University. In order to 
make your jobs run quickly, it is highly recommended that you find ways to package your conda environment or research data into a 
small number of large files for transit from the main filesystem to your node. You can achieve this by tar-ing directories, 
copying, and then un-tarring to the local worker filesystem in your slurm script.

At the moment there is no high-bandwidth communication channel for files between Hyak and Middle Earth, your best bet is rsync. 
Hyak currently has `globus connectivity <https://hyak.uw.edu/docs/storage/globus/>`_, but Middle Earth does not.

If you need to get in touch directly with Hyak admins, you can use the 
`Research computing club Slack <https://depts.washington.edu/uwrcc/>`_, 
`Office hours <https://calendar.washington.edu/sea_uwit-rc>`_, or file a ticket thorugh help@uw.edu with "Hyak" in the subject line

Hyak Tillicum
^^^^^^^^^^^^^

`Tillicum <https://hyak.uw.edu/docs/tillicum/architecture/>`_ is Research Computing's newest compute cluster. 
If you are reading this before February 25, 2026 Andy Connally has some hours that he may let you use; however,
there is no general allocation for compute users.

epyc
^^^^

Epyc is the legacy compute system which Middle Earth is superceding. An overview of Epyc's capabilities is 
`available here. <https://drive.google.com/drive/u/0/folders/15oxHVrO6TubKwO9J1ofzXln7p4dzxeS5>`_