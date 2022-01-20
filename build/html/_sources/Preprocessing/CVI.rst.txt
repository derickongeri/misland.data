=============================================
Coastal Vulnerability Index
=============================================

The index integrates six physical variables in a quantifiable way to reflect the coast's relative vulnerability to physical changes caused by sea-level rise. This method produces numerical data that cannot be immediately correlated to specific physical effects. However, it does emphasize the areas where the various effects of sea-level rise may be the most severe.

.. figure:: ../cvi_images/ranking.png
    :width: 800
    :align: center
    :height: 400
    :alt: Ranking of coastal vulnerability index variables
    :figclass: align-center

    Ranking of the coastal vulnerability index variables

Once each section of coastline is assigned a risk value for each specific data variable, the coastal vulnerability index is calculated as the square root of the geometric mean of these values divided by the total number of variables.

Data Download
_____________

The data was downloaded from different platforms which included the Google Earth Engine platform, Global lithological dataset and the Ecological coastal units site based on the variable in question.

Data Processing Steps
---------------------

Geomorphology
--------------
The Geomophological dataset was downloaded from the global lithological portal given below;
`Global lithological dataset. <https://data.mendeley.com/datasets/y8g64m2v52/1>`_

.. _DataPreparationOverview:  

It was then subset to the generated study area map of the North Africa region.
On the layer styling panel, symbolize the data into 5 classes using the discrete interpolation and then use the interpolation output to classify the data into five classes to give them the degree of erosivity using the qgis reclassify by table tool as shown the the figure below;

.. figure:: ../cvi_images/geomStyling.png
    :align: center
    :alt: Symbology Layer
    :figclass: align-center

    Layer Styling


.. figure:: ../_static/Images/GEOM.png
    :width: 800
    :align: center
    :height: 400
    :alt: Geomophology reclassify by table
    :figclass: align-center

    Geomophology reclassify by table

The result of the re-classification should be 5 classes with a risk value of 5 classes whereby value 1 is very low and value 5 is very high.

.. figure:: ../cvi_images/classes.png
   :align: center
   :scale: 75%
   :alt: Erosivity classes
   :figclass: align-center

   Geomophology Erosivity Classes

Upload to MISLAND Service
_______________________________

.. figure:: ../cvi_images/geomophologyUpload.png
    :width: 642
    :align: center
    :height: 597
    :alt: saving the layer
    :figclass: align-center

    Uploading the data to MISLAND service


Coastal Slope
--------------
Download the elevation raster file from `Google Earth Engine <https://code.earthengine.google.com/>`_
Subset to the North Africa coastal region using the region's shapefile.
To compute slope, **Open Qgis > Raster > Analysis > Slope**. The slope computation window opens as shown below:

.. figure :: ../cvi_images/slopeCalc.png
   :align: center
   :alt: Slope computation
   :figclass: align-center

   Slope Computation

After a successful slope computation, symbolize the it using the discrete interpolation method in Qgis software and then reclassify it into five classes using the Qgis reclassify by table tool.

.. figure:: ../cvi_images/slopeRank.png
   :alt: Slope ranked classes
   :align: center
   
   Slope ranked classes

.. admonition:: Note

   The class ranges should be obtained from the layer styling value label whereby the lowest is assigned value 1 whereas the highest is assigned value 5.

.. figure:: ../cvi_images/slopeUpload.png
    :width: 642
    :align: center
    :height: 597
    :alt: saving the layer
    :figclass: align-center

    Uploading the data to MISLAND service

.. _Overview:

Tidal Range 
------------

Download the data from the `Coastal Ecological Units (ECU) <https://www.esri.com/arcgis-blog/products/arcgis-living-atlas/mapping/ecus-available/>`_
The data comes as a shapefile with different data attributes of 10 variables.
First convert the data into a raster using the **Rasterize GDAL tool in Qgis**. Remember to change the **burn-in field value** to **TIDAL RANGE**.
Leave the other options as default and click run.

.. figure:: ../cvi_images/RasterizeTidal.png
   :alt: Tidal Range Raster Conversion
   :align: center

   Tidal Range Raster Conversion

Next is to reclassify the data and assign the class ranges as it was done in the :ref:`Geomophology data preparation. <DataPreparationOverview>`

.. figure:: ../cvi_images/tidalUpload.png
    :width: 642
    :align: center
    :height: 597
    :alt: saving the layer
    :figclass: align-center

    Uploading the data to MISLAND service

Wave Height 
-----------

Download the data from `global wave statistics, <http://www.globalwavestatisticsonline.com/Help/height_data.htm>`_ and subset it to the North Africa coast region.
Follow the same procedure as the one used in the :ref:`Geomophology data preparation. <DataPreparationOverview>` to classify the data and rank into into 5 categorical classes.

.. figure:: ../cvi_images/waveHeightUpload.png
    :width: 642
    :align: center
    :height: 597
    :alt: saving the layer
    :figclass: align-center

    Uploading the data to MISLAND service

Shoreline Erosion
------------------

Download the data from the `Coastal Ecological Units (ECU) <https://www.esri.com/arcgis-blog/products/arcgis-living-atlas/mapping/ecus-available/>`_ and then follow the procedure as the one given in :ref:`Tidal Range data preparation <Overview>`.

.. figure:: ../cvi_images/accreationUpload.png
    :width: 642
    :align: center
    :height: 597
    :alt: saving the layer
    :figclass: align-center

    Uploading the data to MISLAND service


Sea Level Rise
---------------

.. figure:: ../cvi_images/sealevelchangeUpload.png
    :width: 642
    :align: center
    :height: 597
    :alt: saving the layer
    :figclass: align-center

    Uploading the data to MISLAND service

