################
Setting Up Conda
################

----------------
First Time Setup
----------------

First ssh to either ``arnor`` or ``gondor``. Which one does not matter, because these steps will only alter your 
home directory, which is accessible from either machine equally.

    .. code-block:: bash

        $ ssh -CYA <UW NetID>@arnor.astro.washington.edu

**Note: The steps in this section MUST be done from an SSH terminal, NOT the terminal in Jupyterhub.**

We are going to be replacing the default conda install from the system with an install which is local to your home directory.
This will allow you to create and update your own conda environments (and therefore Jupyter kernels), as well as control what 
version of python and other packages are in use for your scientific code.

First download the Miniforge installer, and run it:

    .. code-block:: bash

        [<UW NetID>@arnor]$ curl -L -O "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
            % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
          100 89.3M  100 89.3M    0     0  90.7M      0 --:--:-- --:--:-- --:--:--  101M
        [<UW NetID>@arnor]$ bash Miniforge3-$(uname)-$(uname -m).sh

You will need to accept the license agreement and the default install directory of ``/astro/users/<your NetID>/miniforge3``. 
It will then take a few minutes to install.

At the end it will ask if you want to update your shell profile to automatically initialize conda. Type "yes" at the prompt and 
hit enter. If you mess up and accept the default of "no", you can remove the ``miniforge3`` directory and re-run setup.

You will be directed to restart your shell. Please do so by exiting and logging in again.

You may then need to run ``source ~/.bashrc``. You should see the ``(base)`` environment show up in your prompt string either 
immediately upon login or after running ``source ~/.bashrc``. 

If you request the current ``conda`` version, you should see a number ``25.3.0`` or better. If you request the current ``mamba`` 
version you should see a number ``2.1.1`` or better:

    .. code-block:: bash

        [<UW NetID>@arnor ~]$ source .bashrc
        (base) [<UW NetID>@arnor ~]$ conda --version
        conda 25.3.0
        (base) [<UW NetID>@arnor ~]$ mamba --version
        2.1.1

In order to make these changes persist to new terminals, you will need to ensure the ``source .bashrc`` line is in ``~/.profile``
so that it will be run on every new login. You can check if these lines exist by looking at ``~/.profile``. If they are not 
present, you can add the needed functionality with the following multi-line command:

    .. code-block:: bash

        (base) [<UW NetID>@arnor ~]$ cat >> ~/.profile <<-EOF
        if [ -n "\$BASH_VERSION" ]; then
            if [ -f "\$HOME/.bashrc" ]; then
            . "\$HOME/.bashrc"
            fi
        fi
        EOF

At this point if you login to a new SSH session or a new Jupyterhub shell you should have the base conda environment active by 
default and both ``conda`` and ``mamba`` should be available at current version numbers.

-----------------------
New Conda Environment
-----------------------

Once you have completed the `First Time Setup`_, and are on a modern version of conda you can create a named conda environment in your 
home directory's ``miniforge3`` directory with the following command:

    .. code-block:: bash

        conda create -n <name-of-my-conda-environment> python=3.12

This will crete a new conda environment starting with the ``python`` package at the version ``3.12`` and installing everything 
that version of python needs to run. The install command will direct you how to activate the environment. You can use the 
commands specified at the end of the install to activate the environment. Once the environment is active, you can install python 
packages with ``pip`` or ``conda``, as well as any additional scientific software you need. These installs will be scoped to your 
environment and will not affect anyone else.

If you need to place your environment in a shared filesystem, rather than your home directory, you can use the ``-p`` option to 
``conda create`` to specify a path where the environment should live. The path is provided instead of a name, and you need to 
provide the path to activate the environment. You might do this to share a common environment with a collaborator, or to place a 
large environment on a shared storage location to avoid running over the storage quota of your home directory.


-----------
Using mamba
-----------

