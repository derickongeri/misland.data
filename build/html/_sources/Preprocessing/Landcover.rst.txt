===========================
Landcover Data Preparation
===========================

MISLAND North Africa usese the European Space Agency (ESA) Climate Change Initiative (CCI) land cover dataset. This dataset provides global maps describing the land surface into 22 classes, which have been defined using the United Nations Food and Agriculture Organization’s (UN FAO) Land Cover Classification System (LCCS). In addition to the land cover (LC) maps, four quality flags are produced to document the reliability of the classification and change detection.
In order to ensure continuity, these land cover maps are consistent with the series of global annual LC maps from the 1990s to 2015 produced by the European Space Agency (ESA) Climate Change Initiative (CCI), which are also available on the ESA CCI LC viewer.

The dataset can be downloaded here from the `ESA C3S archives`_

.. _ESA C3S archives: https://developers.google.com/earth-engine/datasets/catalog/landsat

Data Preprocessing Steps
------------------------
1. Unzip the C3S-LC-L4-LCCS-Map-300m-P1Y-yyyy-v2.1.1 data from the compressed format that it comes in after downloading. Closely examine the contents of this folder as it has various files.

.. image:: ../_static/Images/LC1.png
     :height: 400
     :width: 610
     :alt: LocateIT

2. Load the unzipped NetCDF4 raster onto qgis and select the lccs_class on the “Select Raster Layers to Add” dialog.

.. image:: ../_static/Images/LC2.png
     :height: 277
     :width: 550
     :alt: LocateIT

3.  Once the raster layer is loaded add the vector layer of the OSS region and navigate to Raster > Extraction > Clip Raster by Mask Layer

.. image:: ../_static/Images/LC3.png
     :height: 277
     :width: 550
     :alt: LocateIT

4.  Once the raster layer has been clipped to the area of interest, open the processing toolbox and search for r.reclass and select the GRASS>Raster>r.reclass  tool.

.. image:: ../_static/Images/LC4.png
     :height: 277
     :width: 550
     :alt: LocateIT

5.  On the ”r.reclass” dialog that pops up, select the clipped land cover data as the input layer and paste the following reclassification rules into the “Reclass rules text box” and save the output in a desired location.

.. image:: ../_static/Images/LC5.png
     :height: 277
     :width: 550
     :alt: LocateIT

6.  Once the data is reclassified you can upload the QML style layer to visualize and validate the reclassified land cover data.

.. image:: ../_static/Images/LC6.png
     :height: 277
     :width: 550
     :alt: LocateIT

Data Upload to MISLAND service
-------------------------------
To upload the Land cover dataset to the admin panel. Follow these simple steps

1. Select the **Rasters** option from the list of options on the admin panel 

.. figure:: ../_static/Images/LC7.png
    :width: 598
    :align: center
    :height: 652
    :alt: admin panel
    :figclass: align-center

    Rasters option on admin panel

2  From the *FILTER* options, *By raster type* select **LULC: Land use/land Cover** option to view the list of Land cover datasets that are already availabel on the database

.. figure:: ../_static/Images/LC8.png
    :width: 435
    :align: center
    :height: 550
    :alt: Fitering to view availabel datasets
    :figclass: align-center

    Selecting Land cover option from the list of filters

3.  Once you have confirmed that the raster you wish to add is not in the database. Select the **ADD RASTER** option from the top-right conner of the admin panel.

.. figure:: ../_static/Images/LC9.png
    :width: 425
    :align: center
    :height: 301
    :alt: add raster
    :figclass: align-center

    Selecting 'ADD RASTER' option

4.  On the add raster form that opens up, fill in the *Name* of the Land cover raster you with to add, then select the *Raster Year* and the *Raster Type* as shown below:

.. figure:: ../_static/Images/LC10.png
    :width: 738
    :align: center
    :height: 588
    :alt: add raster form
    :figclass: align-center

    Filling the ADD RASTER form for land cover data upload

.. note::

   It is recomended that you include the Year of the raster in the *Name* field as shown and that you associate the Land cover raster with the **LULC: Land use/land cover** *Raster Type* for the system to work properly and point to the right raster dataset. 