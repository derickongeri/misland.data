====================
Vegetation Indices 
====================

MODIS NDVI
____________
Data download from Google Earth Engine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
The MOD13Q1 V6 product provides a Vegetation Index (VI) value at a per pixel basis. There are two primary vegetation layers. The first is the Normalized Difference Vegetation Index (NDVI) which is referred to as the continuity index to the existing National Oceanic and Atmospheric Administration-Advanced Very High Resolution Radiometer (NOAA-AVHRR) derived NDVI. The second vegetation layer is the Enhanced Vegetation Index (EVI) that minimizes canopy background variations and maintains sensitivity over dense vegetation conditions. The MODIS NDVI and EVI products are computed from atmospherically corrected bi-directional surface reflectances that have been masked for water, clouds, heavy aerosols, and cloud shadows.

To compute and download the mean anual MODIS NDVI data from google earth engine. Open the `Google Earth Engine Code`_ and paste the lines of code provided below

.. Code-block:: javascript
   :linenos:

	/**** Start of imports. If edited, may not auto-convert in the playground. ****/
	var table = ee.FeatureCollection("users/derickongeri/NorthAfrica");
	/***** End of imports. If edited, may not auto-convert in the playground. *****/
	var dataset = ee.ImageCollection('MODIS/006/MOD13Q1')
	                  .filter(ee.Filter.date('2018-01-01', '2019-01-01'))
	                  .mean()
	                  .clip(table);

	var ndvi = dataset.select('NDVI');
	var ndviVis = {
	  min: 0.0,
	  max: 8000.0,
	  palette: [
	    'FFFFFF', 'CE7E45', 'DF923D', 'F1B555', 'FCD163', '99B718', '74A901',
	    '66A000', '529400', '3E8601', '207401', '056201', '004C00', '023B01',
	    '012E01', '011D01', '011301'
	  ],
	};
	Map.centerObject(table);
	Map.addLayer(ndvi, ndviVis, 'NDVI');

	Export.image.toCloudStorage({
	image:ndvi,
	description: 'NDVI',
	maxPixels:1e13,
	scale:250,
	bucket:'oss_ldms_vi',
	region:table 
	})


Landsat derived NDVI, MSAVI, SAVI
____________________________________

Data download from Google Earth Engine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Several annual NDVI composite techniques have been discussed to overcome current Landsat 5 artifacts.
MISLAND uses annual NDVI products based on different percentiles in order to better qualify and quantify the Vegetation Loss Index.

To compute and download desired percentile composites from google earth engine. Open the `Google Earth Engine Code`_ and paste the lines of code provided below

.. _Google Earth Engine Code: https://code.earthengine.google.com/

.. code-block:: javascript
   :linenos:

    // Required Data Inputs 
	// ===================
	// * USGS/NASA's Landsat 4 surface reflectance tier 1 dataset (August 1982 - December 1993)
	// * USGS/NASA's Landsat 5 surface reflectance tier 1 dataset (January 1, 1984 - May 5, 2012)
	// * USGS/NASA's Landsat 7 surface reflectance tier 1 dataset (January 1, 1999 - December 31, 2019)
	// * USGS/NASA's Landsat 8 surface reflectance tier 1 dataset (April 11, 2013 - December 31, 2019)
	// * Study Area Polygon

	var countries = ee.FeatureCollection("USDOS/LSIB_SIMPLE/2017");

	var Year='2002'


	var country = 'Libya';
	var ALGO = "PERCENTILE65"; // PERCENTILE75  // PERCENTILE65 // PERCENTILE60 // MEDIAN
	var cloudCoveragePercentage = 80;


	var studyArea = countries.filter(ee.Filter.eq('country_na',country ))
	//Map.addLayer(studyArea);

	/*
	borders are quite coarse 
	var northAfrica = ee.FeatureCollection('users/derickongeri/Admin')
	// Replace country name with EGYPT, LIBYA, ALGERIA, MAURITANIA, MOROCCO, TUNISIA
	var country = 'TUNISIA';
	var studyArea = northAfrica.filter(ee.Filter.eq('NAME', country))
	Map.addLayer(studyArea);
	*/




	var start_date = Year+ '-01-01';
	var end_date   = Year+ '-12-31';


	//--------------------------------------------------------------------
	//       Landsat 4, 5, 7 cloudmask
	//--------------------------------------------------------------------

	    // If the cloud bit (5) is set and the cloud confidence (7) is high
	    // or the cloud shadow bit is set (3), then it's a bad pixel.
	var cloudMaskL7 = function(image) {
	  var qa = image.select('pixel_qa');
	  var cloud = qa.bitwiseAnd(1 << 5)
	                  .and(qa.bitwiseAnd(1 << 7))
	                  .or(qa.bitwiseAnd(1 << 3));
	  
	    // Remove edge pixels that don't occur in all bands
	  //var mask2 = image.mask().reduce(ee.Reducer.min())//.focal_min(300,'square','meters').eq(0);
	  //var mask2 = image.select('B4').reduce(ee.Reducer.min()).gt(0)//.focal_min(500,'square','meters');
	  // Remove edge pixels that don't occur in all bands
	  var mask3 =  
	              (image.select('B3').gt(100))
	              .and(image.select('B4').gt(100))
	              

	              .and(image.select('B4').lt(10000))
	              .and(image.select('B3').lt(10000))

	              
	  
	  return image.updateMask(cloud.not()).updateMask(mask3)//.updateMask(mask2)//.clip(image.geometry().buffer(-5000))//.or(mask3));
	};


	var cloudMaskL45 = function(image) {
	  var qa = image.select('pixel_qa');
	  var cloud = qa.bitwiseAnd(1 << 5)
	                  .and(qa.bitwiseAnd(1 << 7))
	                  .or(qa.bitwiseAnd(1 << 3));
	  
	  // Remove edge pixels that don't occur in all bands
	  //var mask2 = image.mask().reduce(ee.Reducer.min());
	    var mask2 =  
	              (image.select('B3').gt(100))
	              .and(image.select('B4').gt(100))
	              

	              .and(image.select('B4').lt(10000))
	              .and(image.select('B3').lt(10000))
	  
	  return (image.updateMask(cloud.not()).updateMask(mask2))//.clip(image.geometry().buffer(-5000))//.updateMask(mask2);
	};


	//--------------------------------------------------------------------
	//         Landsat 8 cloudmask
	//--------------------------------------------------------------------

	    // Bits 3 and 5 are cloud shadow and cloud, respectively.
	function maskL8sr(image) {
	  var cloudShadowBitMask = (1 << 3);
	  var cloudsBitMask = (1 << 5);
	  
	    // Get the pixel QA band.
	  var qa = image.select('pixel_qa');

	    // Both flags should be set to zero, indicating clear conditions.
	  var mask = qa.bitwiseAnd(cloudShadowBitMask).eq(0)
	                 .and(qa.bitwiseAnd(cloudsBitMask).eq(0));
	  var mask2 =  
	              
	              (image.select('B5').gt(100))
	              .and(image.select('B4').gt(100))
	              

	              .and(image.select('B5').lt(10000))
	              .and(image.select('B4').lt(10000))
	              
	   //var mask2 = image.mask().reduce(ee.Reducer.min()).focal_min(500,'square','meters');
	  //return image
	  return image.updateMask(mask).updateMask(mask2)//.clip(image.geometry().buffer(-5000));
	}




	    // Apply Cloudmask to L4.5.7
	var L4 = ee.ImageCollection("LANDSAT/LT04/C01/T1_SR")
	                  .filterDate(start_date, end_date)
	                  .filter(ee.Filter.lessThan('CLOUD_COVER_LAND', cloudCoveragePercentage))
	                  .filterBounds(studyArea)
	                  .map(cloudMaskL45)
	                  .select(['B3', 'B4'], ['RED', 'NIR']);;

	var L5 = ee.ImageCollection('LANDSAT/LT05/C01/T1_SR')
	                  .filterDate(start_date, end_date)
	                  .filter(ee.Filter.lessThan('CLOUD_COVER_LAND', cloudCoveragePercentage))
	                  .filterBounds(studyArea)
	                  .map(cloudMaskL45)
	                  .select(['B3', 'B4'], ['RED', 'NIR']);;

	var L7a = ee.ImageCollection('LANDSAT/LE07/C01/T1_SR')
	                  .filterDate('1999-01-01', '2003-04-01')
	                  .filterDate(start_date, end_date)
	                  .filter(ee.Filter.lessThan('CLOUD_COVER_LAND', 100))
	                  .filterBounds(studyArea)
	                  .map(cloudMaskL7)
	                  .select(['B3', 'B4'], ['RED', 'NIR']);;
	var L7b = ee.ImageCollection('LANDSAT/LE07/C01/T1_SR')
	                  .filterDate('2012-01-01', '2013-12-31')
	                  .filterDate(start_date, end_date)
	                  .filter(ee.Filter.lessThan('CLOUD_COVER_LAND', 100))
	                  .filterBounds(studyArea)
	                  .map(cloudMaskL7)
	                  .select(['B3', 'B4'], ['RED', 'NIR']);;

	var L7 = L7a.merge(L7b);

	var L8 = ee.ImageCollection('LANDSAT/LC08/C01/T1_SR')
	                  .filterDate(start_date, end_date)
	                  .filter(ee.Filter.lessThan('CLOUD_COVER', cloudCoveragePercentage))
	                  .filterBounds(studyArea)
	                  //.filterBounds(AOI)
	                  .map(maskL8sr)
	                  .select(['B4', 'B5'], ['RED', 'NIR']);
	                  
	                  




	    //Define collection

	                  
	//--------------------------------------------------------------------
	// Merge Landsat 4, 5, 8 imagery collections and filter all by date/place
	//--------------------------------------------------------------------

	//Merge Landsat 4, 5 , 7 '

	var L4578 = L4.merge(L5).merge(L7).merge(L8);


	//--------------------------------------------------------------------
	//                     Create NDVI Collection 
	//--------------------------------------------------------------------

	var NDVI = function(image) {
	  return image.normalizedDifference(['NIR', 'RED']).rename('NDVI');
	  //return image.addBands(ndvi);
	};

	if (ALGO=='MEDIAN'){
	    var suffix = 'median'; 
	    var annualNDVI = L4578.map(NDVI).median().clip(studyArea);
	}

	if (ALGO=='PERCENTILE75'){
	    var suffix = '75pc'; 
	    var annualNDVI = L4578.map(NDVI).reduce(ee.Reducer.percentile([75])).clip(studyArea);
	}

	if (ALGO=='PERCENTILE65'){
	    var suffix = '65pc'; 
	    var annualNDVI = L4578.map(NDVI).reduce(ee.Reducer.percentile([65])).clip(studyArea);
	}


	var ndvi_visualization = {
	  min: -0.22789797020331423, 
	  max: 0.6575894075894075,
	  palette: 'FFFFFF, CE7E45, DF923D, F1B555, FCD163, 99B718, 74A901, 66A000, 529400,' +
	    '3E8601, 207401, 056201, 004C00, 023B01, 012E01, 011D01, 011301'
	};
	Map.addLayer(annualNDVI, ndvi_visualization, 'NDVI');

	//--------------------------------------------------------------------
	//       Export as GeoTIFF
	//--------------------------------------------------------------------


	Export.image.toDrive({
	 image: annualNDVI,
	 description: country + '_NDVI_' + suffix + '_' + Year,
	 scale: 30,
	 region: studyArea,
	 maxPixels:  1e13,
	 fileFormat: 'GeoTIFF',
	 folder:'GEE_classification',
	 formatOptions: {
	   cloudOptimized: true
	     },
	  skipEmptyTiles: true
	  });
	  
	  //Map.addLayer(L7.first(), {}, 'L7');






