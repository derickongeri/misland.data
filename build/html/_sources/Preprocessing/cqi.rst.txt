======================
Climate Quality Index
======================
Climate quality is assessed on the basis of how it influences water availability to the plants. Consideration has been given to the amount of rainfall, air temperature and aridity. Climate layers and relative scores are reported in Table 3. In particular the selected layers are: Annual precipitation (a crucial parameter in plant growth); Bagnouls-Gaussen aridity index (a synthesis of precipitation, evapotranspiration and run-off information); Slope aspect (affects microclimatic conditions and erosion).

Data Preprocessing in Qgis
____________________________
1. Open the downloaded Potential Evapotranspiration and Precipitation Datasets on Qgis.

.. note::
   The two datasets are in **NetCDF** (Network Common Data Form) - a file format for storing multidimensional scientific data (variables) such as temperature, humidity, pressure, wind speed, and direction. Each of these variables can be displayed through a dimension (such as time) by making a layer or table view from the netCDF file.
   When loading the precipitation data select the **ppt** option on the *Select Raster Layers to Add* dialog that pops up.

   .. figure:: ../_static/Images/cqi2a.png
    :width: 588
    :align: center
    :height: 453
    :alt: Loading the rainfall and PET data
    :figclass: align-center

    Selecting the Precipitation data to add to Qgis


The loaded layers, alongside the OSS North Africa action zone shapefile should appear on the layers panel on Qgis as shown below

.. figure:: ../_static/Images/cqi2.png
    :width: 700
    :align: center
    :height: 450
    :alt: Loading the rainfall and PET data
    :figclass: align-center

    Loading the PPT and PET NetCDF files to Qgis


2. Clip the layers to the desires study area by navigating to *Raster*>*Extraction*>*Clip Raster by Mask Layer* option on the Qgis Menu bar.

.. figure:: ../_static/Images/cqi1a.png
    :width: 526
    :align: center
    :height: 338
    :alt: Clipping by Mask Layer
    :figclass: align-center

    Clipping by Mask Layer

On the dialoge that pops up select the inputs as shown and specify the **Source CRS** and **target CRS** options as shown below. Save the outputs to your desired location before running the tool.

.. figure:: ../_static/Images/cqi1.png
    :width: 782
    :align: center
    :height: 650
    :alt: Clipping by Mask Layer
    :figclass: align-center

    Clipping by Mask Layer

3. Once the layers are successfully cliped and saved, open the Processing toolbox and type "Climate Quality Index" and select the *Climate Quality Index* moded under **Models**

.. figure:: ../_static/Images/cqi3.png
    :width: 409
    :align: center
    :height: 281
    :alt: Climate Quality Index model
    :figclass: align-center

    Climate Quality Index model

Select the proper inputs for the *Potential Evapotranspiration* and the *Precipitation*

.. figure:: ../_static/Images/cqi4.png
    :width: 742
    :align: center
    :height: 644
    :alt: Climate Quality Index model
    :figclass: align-center

    Defining Inputs for the CQI model

.. note::
   The CQI Model yeilds the Precipitation Index by computing the total annual precipitation and reclassifying the values. The Aridity Index is computed as the ration of the Mean annual precipitation and the potential evapotranspiration using the simple Penman-Monteith formulae. The process is as summarized in the graphical representation of the model shown below. 

	.. figure:: ../_static/Images/cqi5.png
	    :width: 800
	    :align: center
	    :height: 300
	    :alt: Climate Quality Index model
	    :figclass: align-center

	    CQI Model graphical model

	The classes for the precipitation and aridity index are obtained from: Ferrara, A*., Kosmas, C., Salvati, L., Padula, A., Mancino, G., & Nolè, A. (2020). Updating the MEDALUS‐ESA Framework for Worldwide Land Degradation and Desertification Assessment. *Land Degradation & Development*, 31(12), 1593-1607.

	.. figure:: ../_static/Images/cqi9.png
	    :width: 544
	    :align: center
	    :height: 208
	    :alt: Climate Quality Index model
	    :figclass: align-center

	    Aridity Index and Precipitaiton index scores

4. Once the model has been executed successfully, The ouputs will be loaded onto Qgis. Right click on the temporary layer and navigate to the *Save as* option to to export the layers with the desired Name, CRS and dimensions as shown below;

.. figure:: ../_static/Images/cqi6.png
    :width: 800
    :align: center
    :height: 681
    :alt: Climate Quality Index model outputs
    :figclass: align-center

    CQI Model graphical model outputs

.. figure:: ../_static/Images/cqi7.png
    :width: 777
    :align: center
    :height: 375
    :alt: Climate Quality Index model
    :figclass: align-center

    Saving the outputs

.. note::
   On the horizontal and vertical resolution setings in the *Save as* dialog paset the value 0.0027778 for each of the outpus to give the layers a resolution 0f 300m to match other variables for computing the desertification indicators

   .. figure:: ../_static/Images/cqi10.png
    :width: 695
    :align: center
    :height: 609
    :alt: Setting the resolution of the layers
    :figclass: align-center

    Setting the resolution of the output layers layers

Uploading the Arididy Index to MISLAND Service
________________________________________________
.. note::
   It is important that you give the Aridity Index layer a descriptive name and assocciate it with the correct year and raster category as shown below. 

.. figure:: ../_static/Images/cqi8.png
    :width: 663
    :align: center
    :height: 544
    :alt: Uploading the Aridity Index
    :figclass: align-center

    Aridity index data upload

Uploading the Rainfall Data to MISLAND Service
__________________________________________________
