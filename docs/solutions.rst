**********************
Problems and Solutions
**********************

GPU code hangs on Gondor
^^^^^^^^^^^^^^^^^^^^^^^^
On Gondor if your previously-working GPU code hangs, it may be because it is seeing 2 GPUs for the first time. 
Set ``CUDA_VISIBLE_DEVICES=0`` or ``CUDA_VISIBLE_DEVICES=1`` in your environment to make only GPU 0 or GPU 1 
available to your code. You can do this from Jupyterlab or the terminal as shown below:

.. tabs::

    .. group-tab:: JupyterHub

        .. code-block:: python

          import torch, os
          os.environ["CUDA_VISIBLE_DEVICES"] = "0"
          torch.cuda.device_count()

    .. group-tab:: CLI

        .. code-block:: bash

          $ CUDA_VISIBLE_DEVICES=0 python -c 'import torch; print(torch.cuda.device_count())'

          OR

          $ set CUDA_VISIBLE_DEVICES=0
          $ python -c 'import torch; print(torch.cuda.device_count())'

To tell which GPU to use, check the current GPU utilization with ``nvidia-smi`` at the command line.


My collaborator cannot access a file or directory
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Almost universally the answer to this is to check permissions on the file or directory itself **as well as ALL directories in the 
full path**.

To get the full path to the file, ``cd`` into the directory where the file exists and run ``pwd``. This should give you the full 
path of the file.

.. code-block:: bash

    $ pwd
    /astro/users/mtauraso/miniforge3/envs/myresearchproject

Starting with the directory on the far right of the path, check each directory by running ``ls -ld`` on the path. 
As you go through the paths it will look like this:

.. code-block:: bash

    $ ls -ld /astro/users/<username>/miniforge3/envs/myresearchproject
    drwxr-xr-x. 11 <username> <username> 189 Jul 14 16:45 /astro/users/<username>/miniforge3/envs/myresearchproject

    $ ls -ld /astro/users/<username>/miniforge3/envs/
    drwxr-xr-x. 3 <username> <username> 71 Jul 14 16:44 /astro/users/<username>/miniforge3/envs/

    $ ls -ld /astro/users/<username>/miniforge3/
    drwxr-x--x. 19 <username> <username> 4096 Jul 14 16:18 /astro/users/<username>/miniforge3/

Note the section of the ``ls -ld`` output at the beginning of each line. The final three letters specify what permissions another 
user will have. ``r`` is for read, ``w`` is for write, and ``x`` is for execute. For directories "execute" means being able to 
list the files in the directory. ``-`` means the permission is denied.

Note the lack of read permisssion on the final line in the example above.

You can fix the permissions of a single directory or an entire directory tree with the commands below:

.. code-block:: bash

    # Single directory or file
    $ chmod a+r /astro/users/<username>/miniforge3/

    # Single directory or file AND everything below it
    $ chmod -R a+r /astro/users/<username>/miniforge3/

The ``a+r`` in the commands above can be read as: ``a`` means "all users", ``+`` means "Add a permission", and ``r`` means the 
"read" permission.  You can use ``-`` in place of ``+`` to remove a permission. The corresponding letter for the ``r`` ead, 
``w`` rite, or e ``x`` ecute permission can be supplied to affect that permission.

