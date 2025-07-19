###########################
Configuring Jupyter kernels
###########################

First follow the setup steps in :doc:`conda` to create a new conda environment which you will use for your kernel. Once 
that is working you can make it available as a jupyter kernel.

-----------------------
Personal Jupyter Kernel
-----------------------

Once you have created and activated a conda environment (following the steps in :doc:`conda`) you will need to ensure 
the ``ipykernel`` package is installed in your new conda environment. see below:

    .. code-block:: bash

        (base) [<User ID>@gondor ~]$ conda activate my-conda-env
        (my-conda-env) [<User ID>@gondor ~]$ conda install ipykernel
        ... follow prompts to install ...

You will then invoke the ``ipykernel`` module to install the kernel to your user directory. You will need a unique identifier 
and a name to display in the jupyter kernel dropdown to run this command.

    .. code-block:: bash

        (my-conda-env) [<User ID>@gondor ~]$ python -m ipykernel install \
            --user \
            --name my_kernel_name \
            --display-name "My Magic Bean Kernel"

You can now refresh jupyter in your browser and see the new python kernel available on all compute nodes.

------------------------
Sharing a Jupyter Kernel
------------------------

First you should create a `Personal Jupyter Kernel`_ and test that it works correctly for you. 

When you are ready to share the environment, activate the corresponsindg conda environment, and install the kernel as in the 
`Personal Jupyter Kernel`_ instructions, but without the ``--user`` flag.

    .. code-block:: bash
    
        (base) [<User ID>@gondor ~]$ conda activate my-conda-env
        (my-conda-env) [<User ID>@gondor ~]$ python -m ipykernel install \
            --name my_kernel_name \
            --display-name "My Magic Bean Kernel"

Permissions on your home directory and the location of your conda environment will need to be correct in order to allow others to 
use your jupyter kernel. If you used :doc:`conda` to set up your conda environment, the following commands will add a minimal
set of permissions which will allow others to access your new kernel.
    
    .. code-block:: bash
    
        (base) [<User ID>@gondor ~]$ chmod a+x ~
        (base) [<User ID>@gondor ~]$ chmod a+x ~/miniforge3
        (base) [<User ID>@gondor ~]$ chmod a+x ~/miniforge3/envs
        (base) [<User ID>@gondor ~]$ chmod -R a+rx ~/miniforge3/envs/my-conda-env

--------------------
List Jupyter Kernels
--------------------

Jupyter Kernels can be listed with the command ``jupyter kernelspec list`` This command will list all personal kernels and all 
global kernels, as well as the location where each kernel is installed. Kernels installed in your home directory are your 
personal kernels.

    .. code-block:: bash
    
        (my-conda-env) [<User ID>@gondor ~]$ jupyter kernelspec list
        Available kernels:
        python3                        /astro/users/<User ID>/miniforge3/envs/<my-conda-env>/share/jupyter/kernels/python3
        my-kernel-name                 /astro/users/<User ID>/.local/share/jupyter/kernels/<my-kernel-name>
        lsst-premap                    /usr/local/share/jupyter/kernels/LSST-premap
        ...

-----------------------
Remove a Jupyter Kernel
-----------------------

**DANGER!** **Removing a globally accessible kernel can negatively affect other folks on the cluster. DO NOT remove other people's global kernels.**

You need the name of the kernel to remove it, which you can find by `listing the jupyter kernels <List Jupyter Kernel>`_.  You can then
remove a jupyter kernel by name using the command below:

    .. code-block:: bash

        (my-conda-env) [<User ID>@gondor ~]$ jupyter kernelspec remove my-kernel-name