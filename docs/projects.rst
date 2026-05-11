###################
Project directories
###################

Working project data (code outputs, intermediate files, etc.) should live on the shared store rather than in your home directory.
The convention on Middle Earth is to create your project directories under:

.. code-block:: text

    /astro/store/shire/<group_name>/<user_name>

Then symlink that location to ``~/projects`` so it is easy to reach from your home directory:

.. code-block:: bash

    $ mkdir -p /astro/store/shire/<group_name>/<user_name>
    $ ln -s /astro/store/shire/<group_name>/<user_name> ~/projects

You can now create and access individual projects through the short path, for example ``~/projects/my_analysis``, while the data
itself lives on the shared store.

A few notes:

* If ``~/projects`` already exists as a real directory, ``ln -s`` will silently place the link *inside* it (e.g. ``~/projects/<user_name>``) rather than erroring out. Move or remove the existing directory before creating the link.
* Use ``ls -l ~/projects`` to confirm the link points where you expect — the output should show ``projects -> /astro/store/shire/<group>/<user>``.
