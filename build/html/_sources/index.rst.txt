.. MISLAND DATA PREPARATION MANUAL documentation master file, created by
   sphinx-quickstart on Fri Mar 26 13:09:24 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

==================================================================
MISLAND SYSTEM ADMINISTRATION AND DATA PREPARATION DOCUMENTATION
==================================================================

.. figure:: _static/Images/intro1.png
    :width: 800
    :align: center
    :height: 400
    :alt: MISLAND homepage
    :figclass: align-center

    Misland Homepage

MISLAND-North Africa is an operational instrument relying on the international standards for reporting SDG 15.3.1 and technical approaches allowing the delivery of regular information on vegetation cover gain/loss to decision makers and environmental agencies at the first place.

The core-service provides land degradation indicators for six North African Countries at two levels:

	- At the regional level(North Africa action zone) where low and medium resolution EO are used.

	- At the pilot site level, where(customized indicators) can be developed, using medium resoultion data(landsat time series imagery and derived vegetation indices, combined with different satellite-derived climate data)

.. note::

   You can download the `PDF Version of this doucument`_ here.

   .. _PDF Version of this doucument: https://mislanddata.readthedocs.io/_/downloads/en/latest/pdf/

.. toctree::
   :maxdepth: 3
   :caption: MISLAND System Admin
   
   /Introduction/admin

.. toctree::
   :maxdepth: 3
   :caption: Data Preparation
   
   /Introduction/data
   /Introduction/models
   /Introduction/Introduction

.. toctree::
   :maxdepth: 3
   :caption: Data Preprocessing in Qgis
   
   /Preprocessing/NDVI
   /Preprocessing/Landcover
   /Preprocessing/Forestloss
   /Preprocessing/Ecologicalunits
   /Preprocessing/cqi
   /Preprocessing/vqi
   /Preprocessing/sqi
   /Preprocessing/mqi
   /Preprocessing/soc
   /Preprocessing/CVI


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
