##########################################
Globus Access
##########################################

Middle Earth runs a Globus Endpoint connected to Shire, which allows large data transfers from national labs, and easy data 
transfer to Hyak Klone or Tillicum

-----------------------------
Finding the Globus Collection
-----------------------------

In the Globus file browser, look for the `UW Astronomy DiRAC Storage <https://app.globus.org/file-manager?origin_id=02c929d1-e3ad-41b5-a173-d122507dce6e&origin_path=%2F&two_pane=true>`_ collection. 
You can use this collection as the source or destination for a transfer from any other collection that is available to you through Globus. The collection gives you access
to both the ``shire`` (`link <https://app.globus.org/file-manager?origin_id=02c929d1-e3ad-41b5-a173-d122507dce6e&origin_path=%2Fshire%2F&two_pane=true>`_) 
and ``shiren`` (`link <https://app.globus.org/file-manager?origin_id=02c929d1-e3ad-41b5-a173-d122507dce6e&origin_path=%2Fshiren%2F&two_pane=true>`_) storage areas in Middle Earth.

Please be aware that ``shiren`` is very small and cannot accommodate a large amount of data. It is only available to optimize 
access to large numbers of small files. 

-----------
Permissions
-----------

For incoming transfers you must use ``/shire/globus-incoming`` (`link <https://app.globus.org/file-manager?origin_id=02c929d1-e3ad-41b5-a173-d122507dce6e&origin_path=%2Fshire%2Fglobus-incoming%2F&two_pane=true>`_) 
or ``/shiren/globus-incoming`` (`link <https://app.globus.org/file-manager?origin_id=02c929d1-e3ad-41b5-a173-d122507dce6e&origin_path=%2Fshiren%2Fglobus-incoming%2F&two_pane=true>`_) 
as the parent directory of your transfer. Once files are transferred you can ``mv`` them into place on either filesystem and set permissions as appropriate.

For outgoing transfers, all of your files must be readable by all users in order for globus to see them. You can achieve this
with ``chmod -R o+rx <directory-to-my-files>`` If your files are deep in a subdirectory you may need to run this same command
on directories above your directory in order for the gobus file browser to be able to navigate to your directory.
