*******************
LSST Software Stack
*******************

On Middle Earth you can install the `LSST pipelines software <https://pipelines.lsst.io/index.html>`__ without using EUPS.


Middle earth hosts a conda channel that contains an `lsst_distrib` megapackage supporting current released versions of the 
`LSST pipelines software <https://pipelines.lsst.io/index.html>`__ . This conda channel is a collection of packages like 
`conda forge <https://conda-forge.org/packages/>`__, but it does not have a fancy website.

You can enumerate the packages and versions available in the conda channel by running the following on `arnor` or `gondor`

.. code-block:: bash

    # Show all packages
    $ conda search -c file:///astro/store/shiren/dirac-conda --override-channel

    # Show packages according to a search string
    $ conda search -c file:///astro/store/shiren/dirac-conda --override-channel 'lsst*'


You can install packages via three main methods; however, any method of adding a 
`conda channel <https://docs.conda.io/projects/conda/en/stable/user-guide/concepts/channels.html>`__ to your environment will work.

Install a package directly specifying the channel on the command line:

.. code-block:: bash

    (my-conda-env) $ conda install -c file:///astro/store/shiren/dirac-conda lsst-distrib
    # If you need a particular version
    (my-conda-env) $ conda install -c file:///astro/store/shiren/dirac-conda lsst-distrib==30.0.7


Add the channel to your environment so you do not have to specify it at install time

.. code-block:: bash

    # Add the channel to your environment
    (my-conda-env) $ conda config --env --add channels file:///astro/store/shiren/dirac-conda
    # Install the lsst_distrib package
    (my-conda-env) $ conda install lsst-distrib


Create a new environment with the channel (and package) preinstalled

.. code-block:: bash

    # lsst_distrib needs python, so the correct version of python will be installed as a dependency
    $ conda create -n my-conda-env -c file:///astro/store/shiren/dirac-conda -c conda-forge lsst-distrib=30.0.7
    $ conda activate my-conda-env
    (my-conda-env) $


If you need to alter pieces of the full LSST distribution, develop on the LSST stack, or need a more customized install please 
refer to the `LSST Pipeline install instructions <https://pipelines.lsst.io/install/index.html>`__ . 
