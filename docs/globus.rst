##########################################
Globus Access
##########################################

Middle Earth runs a Globus Endpoint connected to Shire, which allows large data transfers from national labs, and easy data 
transfer to Hyak Klone or Tillicum

-----------------------------
Finding the Globus Collection
-----------------------------

In the Globus file browser, look for the "UW Astronomy DiRAC Storage" collection. You can use this collection as the source or 
destination for a transfer from any other collection that is available to you through Globus. The collection gives you access
to both the ``shire`` and ``shiren`` storage areas in Middle Earth.

Please be aware that ``shiren`` is very small and cannot accommodate a large amount of data. It is only available to optimize 
access to large numbers of small files. 

-----------
Permissions
-----------

For incoming transfers you must use ``/shire/globus-incoming`` or ``/shiren/globus-incoming`` as the parent directory of your 
transfer. Once files are transferred you can ``mv`` them into place on either filesystem and set permissions as appropriate.

For outgoing transfers, all of your files must be readable by all users in order for globus to see them. You can achieve this
with ``chmod -R o+rx <directory-to-my-files>`` If your files are deep in a subdirectory you may need to run this same command
on directories above your directory in order for the gobus file browser to be able to navigate to your directory.
