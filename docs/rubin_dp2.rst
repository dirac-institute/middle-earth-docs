************************************
Rubin Data Preview 2 (DP2) Catalogs
************************************

Rubin Observatory's `Early Data Preview 2 (EDP2) <https://dp2.lsst.io/>`__ was released on July 27, 2026.
EDP2 contains image and catalog products from Science Pipelines v30 processing of observations obtained with the
LSST Camera between April 2025 and January 2026. It includes deep coadd images and the full suite of catalog data
products, including measurements on processed visit and difference images.

The catalogs are available locally on UW compute infrastructure in
`HATS <https://hats.readthedocs.io/en/stable/>`__ format, for use with
`LSDB <https://docs.lsdb.io/en/latest/index.html>`__.

----------------------------
Local file locations
----------------------------

.. list-table::
   :widths: 25 75
   :header-rows: 1

   * - Platform
     - Path
   * - Middle Earth (arnor / gondor)
     - ``/astro/store/shire/hats/catalogs/rubin_dp2``
   * - Hyak Klone
     - ``/gscratch/dirac/hats/catalogs/rubin_dp2``


----------------------------
Loading catalogs with LSDB
----------------------------

The upstream catalogs are also available over the web at `data.lsst.cloud <https://data.lsst.cloud/>`__ and
documented at `data.lsdb.io <https://data.lsdb.io/Rubin/DP2/>`__. However, loading from the local path is
**much faster** and avoids network overhead.

To open a DP2 catalog in Python, point LSDB at the local path instead of the web URL.
For example, to load the **Object** collection:

.. code-block:: python

    import lsdb

    # On Middle Earth (arnor / gondor)
    object_cat = lsdb.open_catalog('/astro/store/shire/hats/catalogs/rubin_dp2/object_collection')

    # On Hyak Klone
    object_cat = lsdb.open_catalog('/gscratch/dirac/hats/catalogs/rubin_dp2/object_collection')

Catalogs are opened lazily — only the schema is read initially, and data are loaded on demand. This makes it
practical to work with the full catalogs interactively: opening the 786-million-row Object catalog above takes
a fraction of a second.

Point LSDB at the **collection** directory (``object_collection``), not at the catalog directory nested inside
it (``object_collection/object_lc``). Opening the collection also attaches the catalog's margin cache, which
LSDB needs in order to return correct results for cross-matches near partition boundaries.

By default only a subset of columns is loaded. Pass ``columns="all"`` for the full schema, and use a search
filter to restrict to a region of sky:

.. code-block:: python

    cone = lsdb.ConeSearch(ra=9.603, dec=-45.192, radius_arcsec=120.0)
    object_cat = lsdb.open_catalog(
        '/astro/store/shire/hats/catalogs/rubin_dp2/object_collection',
        search_filter=cone,
        columns="all",
    )


----------------------------
Available catalogs
----------------------------

The local HATS release contains three catalog collections. Refer to the
`DP2 data products documentation <https://dp2.lsst.io/products/index.html>`__ for full schema and column
descriptions.

.. list-table::
   :widths: 30 15 55
   :header-rows: 1

   * - Collection
     - Rows
     - Contents
   * - ``object_collection``
     - 786,420,720
     - Coadd Object catalog, with nested per-object forced-source lightcurves
   * - ``dia_object_collection``
     - 232,004,216
     - DIA Object catalog, with nested DIA Source and DIA forced-source lightcurves
   * - ``object_photoz``
     - 651,640,921
     - Photometric redshifts for Objects from six estimators

The Object and DIA Object collections include **nested** per-object lightcurves — forced-source photometry in
*ugrizy*, in the ``objectForcedSource`` and ``diaObjectForcedSource`` columns respectively. This enables
time-series analysis without a separate join against a Source table. Note that this is why there are no
standalone Source or Forced Source catalogs in the local release: that photometry lives inside the Object
catalogs. Catalogs in the upstream DP2 release that are *not* mirrored locally (SS Object, SS Source, MPC
Orbits, Visit, Visit Summary) remain available over the web at
`data.lsst.cloud <https://data.lsst.cloud/>`__.

The photometric redshift catalog carries ``objectId``, so it can be joined back to the Object catalog. Its
six per-object estimates are ``bpz_z_best``, ``dnf_z_best``, ``fzboost_z_best``, ``gpz_z_best``,
``knn_z_best``, and ``tpz_z_best``.

To list the catalog directories available locally:

.. code-block:: bash

    $ ls /astro/store/shire/hats/catalogs/rubin_dp2/
    dia_object_collection  object_collection  object_photoz  public-files


----------------------------
Cross-matching
----------------------------

LSDB can cross-match DP2 catalogs against other HATS-format catalogs stored on Middle Earth.
Older catalogs (e.g., Gaia DR3) are under ``/epyc/data3/hats/catalogs/``, while DP2 catalogs use the newer
shire storage at ``/astro/store/shire/hats/catalogs/rubin_dp2/``. See :doc:`data` for the full list of
locally available catalogs.

.. code-block:: python

    import lsdb

    dp2_objects = lsdb.open_catalog('/astro/store/shire/hats/catalogs/rubin_dp2/object_collection')
    gaia = lsdb.open_catalog('/epyc/data3/hats/catalogs/gaia_dr3')

    matched = dp2_objects.crossmatch(gaia, n_neighbors=1, radius_arcsec=1.0)

The cross-match is lazy, like the catalogs themselves. Call ``.compute()`` to materialize the result — restrict
to a region of sky first unless you intend to match the full catalogs:

.. code-block:: python

    cone = lsdb.ConeSearch(ra=9.603, dec=-45.192, radius_arcsec=120.0)

    dp2_objects = lsdb.open_catalog(
        '/astro/store/shire/hats/catalogs/rubin_dp2/object_collection', search_filter=cone)
    gaia = lsdb.open_catalog('/epyc/data3/hats/catalogs/gaia_dr3', search_filter=cone)

    matched = dp2_objects.crossmatch(gaia, n_neighbors=1, radius_arcsec=1.0).compute()


----------------------------
Upstream documentation
----------------------------

* **DP2 documentation:** `dp2.lsst.io <https://dp2.lsst.io/>`__
* **LSDB + DP2 guide:** `lsdb.io/dp2 <https://lsdb.io/dp2>`__
* **HATS catalog browser:** `data.lsdb.io/Rubin/DP2 <https://data.lsdb.io/Rubin/DP2/>`__
* **HATS data via HTTP:** `data.lsst.cloud <https://data.lsst.cloud/>`__
* **DP2 tutorials:** `dp2.lsst.io/tutorials <https://dp2.lsst.io/tutorials/index.html>`__

**Dataset citation:**

    NSF-DOE Vera C. Rubin Observatory (2026); Legacy Survey of Space and Time Data Preview 2.
    https://doi.org/10.71929/rubin/3382528


----------------------------
Data access policy
----------------------------

DP2 access requires Rubin data rights. All scientists and students in the US and Chile, plus named members of
international in-kind teams, have data rights. See the
`Rubin data policy <https://rubinobservatory.org/for-scientists/data-products/data-policy>`__ for details.

The full DP2 release (adding processed visit images, difference images, and templates) is expected October–December 2026.
