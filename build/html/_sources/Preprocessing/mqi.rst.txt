=========================
Management Qulity Index
=========================

1. Open the downloaded country population density data on Qgis as shown in the figure so as to merge them 

.. figure:: ../_static/Images/mqi1.png
    :width: 721
    :align: center
    :height: 400
    :alt: Opening Land cover and population data on Qgis
    :figclass: align-center

    Opening Land cover and population data on Qgis

2. On the Qgis Menu-bar, navigate to *Raster>Miscelleneous>Merge* as shown below:

.. figure:: ../_static/Images/mqi2.png
    :width: 594
    :align: center
    :height: 411
    :alt: Merging the population dataset
    :figclass: align-center

    Merging Population Dataset

3. On the dialog that pops-up, click on the *Input Layer* selection option and choose *Select All*

.. figure:: ../_static/Images/mqi3a.png
    :width: 883
    :align: center
    :height: 691
    :alt: Selecting population datasets to merge
    :figclass: align-center

    Merge layers dialog

.. figure:: ../_static/Images/mqi3.png
    :width: 883
    :align: center
    :height: 691
    :alt: Selecting population datasets to merge
    :figclass: align-center

    Selecting population datasets to merge

Save the merged layer to your desired location.

4. With the output from step 3 above loaded onto Qgis, Load the landcover data for the same year as the population data
.. figure:: ../_static/Images/mqi4.png
    :width: 710
    :align: center
    :height: 400
    :alt: Loading the Landcover data on Qgis
    :figclass: align-center

    Load the Landcover data on Qgis

5. Once the layers are loaded on to Qgis, open the processing toolbox and search for 'Management Quality Index' in the search bar. The management quality index model shoul show up under your the **Models** section as shown. Click on the Model to open it.

.. figure:: ../_static/Images/mqi5.png
    :width: 411
    :align: center
    :height: 340
    :alt: Management Quality Index Model
    :figclass: align-center

    Accessing the MQI model from the processing toolbox

6. Select the Landcover and Population dataset as your model inputs on the dialog that pops up as shown below:

.. figure:: ../_static/Images/mqi6.png
    :width: 765
    :align: center
    :height: 621
    :alt: MQI Dialog
    :figclass: align-center

    Selecting Imput parameters for the MQI model

7. 
.. figure:: ../_static/Images/mqi7.png
    :width: 883
    :align: center
    :height: 691
    :alt: Selecting population datasets to merge
    :figclass: align-center

    Management Quality Index Model summary

.. figure:: ../_static/Images/mqi8.png
    :width: 715
    :align: center
    :height: 400
    :alt: MQI model outputs
    :figclass: align-center

    Management Quality Index model outputs

.. figure:: ../_static/Images/mqi9.png
    :width: 838
    :align: center
    :height: 633
    :alt: Saving the Outputs
    :figclass: align-center

    Saving the Outputs of the MQI model




