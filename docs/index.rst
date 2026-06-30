
#######################
Welcome to Middle Earth
#######################

Middle Earth is the `DiRAC Institute's <https://dirac.astro.washington.edu/>`_ new compute cluster. It is the successor to ``epyc``.

***************
Getting Started
***************

If you had access to ``epyc`` you also have access to Middle Earth. If you need access, see :doc:`user_accounts` for the request process.

Basic Jupyterhub and shell access are as follows:

* `Arnor Jupyterhub <https://arnor.astro.washington.edu/jupyter>`_
* `Gondor Jupyterhub <https://gondor.astro.washington.edu/jupyter>`_
* Arnor SSH: ``ssh <NetID>@arnor.astro.washington.edu``
* Gondor SSH: ``ssh <NetID>@gondor.astro.washington.edu``

For hardware details and available resources, see :doc:`specs`.

Communication about system status is in the `#computing <https://uw-dirac.slack.com/archives/C8WRK67LY>`_ channel on the
`DiRAC Slack workspace <https://uw-dirac.slack.com/>`_.

If you are looking for astronomy-specific information about Klone, Hyak, or Tillicum look at :doc:`other_compute`


************
Environments
************
For setting up Python environments and notebook kernels, see:

* :doc:`conda` — installing Conda and creating environments
* :doc:`jupyterkernel` — configuring Jupyter kernels for JupyterHub

****
Data
****
Home directories are your astro home directory, the same one as was available from ``epyc``.

You have access to all of your files from ``epyc`` at ``/astro/store/`` on either machine.

New projects should use ``/astro/store/shire`` for data storage.

.. toctree::
   :maxdepth: 2
   :hidden:

   self
   user_accounts
   conda
   jupyterkernel
   utilization
   solutions
   rubin
   specs
   other_compute
   data
