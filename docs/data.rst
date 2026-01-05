##########################################
Data Access
##########################################
There are a number of datasets stored locally on the Middle Earth / epyc. 
Even if these datasets are web accessible, it is much more efficient to access them directly from the local storage.

----------------
Catalogs in LSDB
----------------
Many astronomical survey datasets are stored in `Hats <https://hats.readthedocs.io/en/stable/>`_ style catalogs accessible through the `LSDB <https://docs.lsdb.io/en/latest/index.html>`_ package.

To see a list of available catalogs, and their documentation refer to `https://data.lsdb.io/ <https://data.lsdb.io/>`_.

For example instructions to load the `Gaia DR3 <https://data.lsdb.io/#Gaia/Gaia_DR3_(US-West,_HTTP)>`_ catalog in lsdb are the following:

.. code-block:: python

    lsdb.open_catalog('https://data.lsdb.io/hats/gaia_dr3')

This web accessible URL can be replaced with a local path if you are running on Middle Earth / epyc using the prefix ``/epyc/data3/hats/catalogs/`` . 

And the same line of code becomes:

.. code-block:: python

    lsdb.open_catalog('/epyc/data3/hats/catalogs/gaia_dr3')

Making this change will greatly increase the speed of data access, especially for large datasets.