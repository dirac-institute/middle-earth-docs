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

---------------------------------------
Symlinking datasets into your workspace
---------------------------------------
Rather than typing out long paths like ``/epyc/data3/hats/catalogs/gaia_dr3`` every time, you can create a symbolic link (symlink)
that points from a short path in your home or project directory to the dataset on the shared store. The symlink behaves like the
original directory but takes up no additional space.

Create a symlink with ``ln -s <target> <link_name>``, where ``<target>`` is the existing path you want to point to and ``<link_name>``
is the new shortcut you are creating:

.. code-block:: bash

    $ cd ~
    $ ln -s /epyc/data3/hats/catalogs/gaia_dr3 gaia_dr3

You can now access the catalog through the shorter path:

.. code-block:: python

    lsdb.open_catalog('/astro/users/<username>/gaia_dr3')

A few notes:

* Always use an **absolute path** for the target (the first argument). Relative targets break if you move the link.
* To inspect a symlink, run ``ls -l`` — the output shows ``link_name -> target``.
* To remove a symlink, use ``rm <link_name>``. This deletes the link only, not the target data. **Do not use** ``rm -r`` on a symlink to a directory, as some tools may follow the link and delete the underlying data.
* If the target's permissions deny you access, the symlink will not work. See the "My collaborator cannot access a file or directory" section in :doc:`solutions` for how to check permissions along the full path.