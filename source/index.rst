.. MISLAND DATA PREPARATION MANUAL documentation master file, created by
   sphinx-quickstart on Fri Mar 26 13:09:24 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

MISLAND DATA PREPARATION DOCUMENTATION
=======================================

	.. image:: ../source/_static/Images/LDMS.png
	   :height: 277
	   :width: 550
	   :alt: LocateIT

MISLAND-North Africa is an operational instrument relying on the international standards for reporting SDG 15.3.1 and technical approaches allowing the delivery of regular information on vegetation cover gain/loss to decision makers and environmental agencies at the first place.

The core-service provides land degradation indicators for six North African Countries at two levels:

	- At the regional level(North Africa action zone) where low and medium resolution EO are used.

	- At the pilot site level, where(customized indicators) can be developed, using medium resoultion data(landsat time series imagery and derived vegetation indices, combined with different satellite-derived climate data)

.. note::

   You can download the `PDF Version of this doucument`_ here.

   .. _PDF Version of this doucument: https://misland.readthedocs.io/_/downloads/en/master/pdf/

.. toctree::
   :maxdepth: 3
   :caption: Data and Data Sources
   
   /Introduction/data

.. toctree::
   :maxdepth: 3
   :caption: Data Preprocessing in Qgis
   
   /Preprocessing/Landcover
   /Preprocessing/NDVI
   /Preprocessing/MSAVI
   /Preprocessing/soc
   /Preprocessing/Forestloss
   /Preprocessing/Ecologicalunits
   /Preprocessing/cqi
   /Preprocessing/vqi
   /Preprocessing/sqi
   /Preprocessing/mqi


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`