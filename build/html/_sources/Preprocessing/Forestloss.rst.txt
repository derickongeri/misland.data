============
Forest Loss 
============
The High-resolution global forset change results from time-series analysis of Landsat images in characterizing global forest extent and change.

The 'first' and 'last' bands are reference multispectral imagery from the first and last available years for Landsat spectral bands 3, 4, 5, and 7. Reference composite imagery represents median observations from a set of quality-assessed growing-season observations for each of these bands.

MISLAND North Africal uses the Hansen Global Forest Change v1.8 to asses forest loss in the North Africa action zone. For more details of the Hansen Global Forest Change see the `user notes`_

.. _user notes: https://storage.googleapis.com/earthenginepartners-hansen/GFC-2020-v1.8/download.html

Data Preprocessing and Download on GEE
________________________________________

1. Open the _`Google Earth Engine Code` and paste the following code to import the **Hansen Global forest change v1.8**, **OSS North Africa Action zone**(study area) and **Geometry** for forest areas in North Africa.

.. code-block:: javascript
   :linenos:

   var image = ee.Image("UMD/hansen/global_forest_change_2020_v1_8"),
    table = ee.FeatureCollection("users/derickongeri/NorthAfrica"),
    geometry = 
    /* color: #d63000 */
    /* shown: false */
    /* displayProperties: [
      {
        "type": "rectangle"
      }
    ] */
    ee.Geometry.Polygon(
        [[[-10.330249200933336, 37.60222178276082],
          [-10.330249200933336, 31.415726509598066],
          [24.562328924066662, 31.415726509598066],
          [24.562328924066662, 37.60222178276082]]], null, false);

2. To select the forestLoss by year band and export the product paste the following code.

.. code-block:: javascript
   :linenos:

   var dataset = image.clip(table);

   var forestLoss = dataset.select('lossyear');

   Map.addLayer(forestLoss);

   Export.image.toDrive({
     image: forestLoss,
     description: 'ForestLoss',
     scale: 30,
     region: geometry,
     maxPixels:  1e13,
     fileFormat: 'GeoTIFF',
     folder:'GEE_classification',
     formatOptions: {
       cloudOptimized: true
     },
       skipEmptyTiles: true
     });

3. Save the code and run it to export the forestloss by year data.

Data Preprocessing in Qgis
____________________________

1. Download the data form Google drive to your desired location on your local machine and load it to Qgis to view the outputs.

.. figure:: ../_static/Images/fr1.png
    :width: 735
    :align: center
    :height: 415
    :alt: Opening the Forestloss data on Qgis
    :figclass: align-center

    Opening the Forestloss year data on Qgis

2. On the Qgis menu-bar navigate to *Raster*>*Miscellaneous*>*Merge* to merge the downloaded tiles

.. figure:: ../_static/Images/fr2.png
    :width: 735
    :align: center
    :height: 415
    :alt: Merging
    :figclass: align-center

    Merging the Forestloss year data

3. On the Merge dialog, **Input layers** option choose the |selectAll|:sup:`Select All` option and click on :guilabel:`OK`.

.. figure:: ../_static/Images/fr3.png
    :width: 742
    :align: center
    :height: 642
    :alt: Select All layers
    :figclass: align-center

    Selecting All layers to merge
save the output to a temporary layer so as to export it with desired properties in the next step.

4. Right click on the layer and navigate to *Export*>*Save as* option and save the layer to your desired location with the appropriate name.

.. note::
   The forest loss by year raster has values ranging from 1-20. The values represent the loss year form 2001 to 2020 hence to set the "nodata" value to 0 on the *Save Raster Layer as* dialog, check the **No data values** and input the values as shown in the figure below:

	.. figure:: ../_static/Images/fr4.png
	    :width: 691
	    :align: center
	    :height: 608
	    :alt: saving the layer
	    :figclass: align-center

	    Saving the Forest Loss year data

Upload to MISLAND Service
_______________________________

.. figure:: ../_static/Images/fr5.png
    :width: 642
    :align: center
    :height: 597
    :alt: saving the layer
    :figclass: align-center

    Uploading the data to MISLAND service



.. |addToProject| image:: ../_static/common/mAddToProject.png
   :width: 1.5em
.. |checkbox| image:: ../_static/common/checkbox.png
   :width: 1.3em
.. |deleteSelected| image:: ../_static/common/mActionDeleteSelected.png
   :width: 1.5em
.. |editCopy| image:: ../_static/common/mActionEditCopy.png
   :width: 1.5em
.. |editCut| image:: ../_static/common/mActionEditCut.png
   :width: 1.5em
.. |editPaste| image:: ../_static/common/mActionEditPaste.png
   :width: 1.5em
.. |expression| image:: ../_static/common/mIconExpression.png
   :width: 1.5em
.. |fileOpen| image:: ../_static/common/mActionFileOpen.png
   :width: 1.5em
.. |fileSave| image:: ../_static/common/mActionFileSave.png
   :width: 1.5em
.. |integer| image:: ../_static/common/mIconFieldInteger.png
   :width: 1.5em
.. |processing| image:: ../_static/common/processingAlgorithm.png
   :width: 1.5em
.. |processingHelp| image:: ../_static/common/mActionEditHelpContent.png
   :width: 1.5em
.. |processingModel| image:: ../_static/common/processingModel.png
   :width: 1.5em
.. |processingOutput| image:: ../_static/common/mIconModelOutput.png
   :width: 1.5em
.. |qgsProjectFile| image:: ../_static/common/mIconQgsProjectFile.png
   :width: 1.5em
.. |redo| image:: ../_static/common/mActionRedo.png
   :width: 1.5em
.. |saveAsPDF| image:: ../_static/common/mActionSaveAsPDF.png
   :width: 1.5em
.. |saveAsPython| image:: ../_static/common/mActionSaveAsPython.png
   :width: 1.5em
.. |saveAsSVG| image:: ../_static/common/mActionSaveAsSVG.png
   :width: 1.5em
.. |saveMapAsImage| image:: ../_static/common/mActionSaveMapAsImage.png
   :width: 1.5em
.. |selectAll| image:: ../_static/common/mActionSelectAll.png
   :width: 1.5em
.. |start| image:: ../_static/common/mActionStart.png
   :width: 1.5em
.. |unchecked| image:: ../_static/common/checkbox_unchecked.png
   :width: 1.3em
.. |undo| image:: ../_static/common/mActionUndo.png
   :width: 1.5em
.. |zoomActual| image:: ../_static/common/mActionZoomActual.png
   :width: 1.5em
.. |zoomFullExtent| image:: ../_static/common/mActionZoomFullExtent.png
   :width: 1.5em
.. |zoomIn| image:: ../_static/common/mActionZoomIn.png
   :width: 1.5em
.. |zoomOut| image:: ../_static/common/mActionZoomOut.png
   :width: 1.5em
.. |zoomOut| image:: ../_static/common/processingModel.png
   :width: 1.5em

