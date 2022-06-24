# North-America-Extratropical-Cyclone-NAEC-Catalogue-temporary-

This README_NAECv1.txt file was produced on 2022-06-20 by Ting-Chen Chen
  
--------------------
GENERAL INFORMATION
--------------------

-Dataset title: North America Extratropical Cyclone (NAEC) Catalogue, Version 1

-Authors: Ting-Chen Chen, Alejandro Di Luca, and Katja Winger

-Affiliation: Département des sciences de la Terre et de l’atmosphère. Université du Québec à Montréal (UQAM), Montréal, Canada

-Brief description:

The NAEC catalogue v1 comprises information of extratropical cyclone (ETC) tracks at hourly temporal resolution in North America (20–80 N and 0–180W) obtained from the ECMWF ERA5 reanalysis from January 1979 to December 2020. In addition, it includes ETC-associated variables such as the near-surface wind speed and precipitation calculated for different radii and in absolute and relative (to the local climatology) terms. This catalogue provides useful information for the assessment of ETC-induced impacts over North America.

-Date of data collection: 42 years from 1979-01-02 to 2020-12-31

-Data production date: 2022-06-20

-Data release date: 2022-06-23

-Geographic location of data collection: North America (20-80N and 0-180W)

-Information regarding granting agencies or sponsors of this data collection:

This research has been made as part of the project “Simulation et analyse du climat à haute resolution” funded by the Ministry of the Environment and the Fight Against Climate Change.

--------------------------------------------------
ACCESS INFORMATION/DATA SHARING
--------------------------------------------------

-Data Licenses/Restrictions or Use Limitations:

This dataset (produced by the research team of Alejandro Di Luca) is licensed under a CC BY 4.0 licence.

The source data we used to produce this dataset is the European Centre for Medium-Range Weather Forecasts (ECMWF) ERA5 hourly reanalysis at a spatial resolution of 0.25×0.25 (Hersbach et al., 2018, 2020). The ECMWF ERA5 reanalysis data is published under a CC BY 4.0 licence, and is available through the Climate Data Store infrastructure: https://cds.climate.copernicus.eu.

-Bibliographic references and hyperlinks to publications related to this dataset:

This dataset is presented in a peer-review article submitted to the Geophysical Research Letter (currently under review):
Chen, T.-C., Di Luca, A., Winger, K., Laprise, R., Thériault, J. M. (2022): Seasonality of continental extratropical-cyclone wind speeds over northeastern North America [under review]. Geophysical Research Letter.

-----------------------------
OVERVIEW OF DATA & FILES
-----------------------------

-List of files:

        Documentation:
                README_NAECv1.txt
                NAEC_Catalogue_v1_Documentation.pdf
        Data:
                NAEC_1979_2020_v1.csv

--------------------------
METHODOLOGICAL INFORMATION
--------------------------

Extratropical cyclone (ETCs) are identified using the storm tracking algorithm developed by Katja Winger at UQAM (the Fortran code is available upon request from winger.katja@uqam.ca). The algorithm is flexible in dealing with different source datasets, and searching domain and period. Users can also choose different fields for the cyclone identification (using, for example, the smoothed field or not, mean sea-level pressure or 850-hPa relative vorticity), change the thresholds for cyclone identification and tracking (e.g., cut-off intensity, distance for tracking), and specify the duration filtering. Here we only detail the setups used for the present catalogue, which is the same as in Chen et al. (2022). The searching domain is within 20–80 N and 0–180W, covering North America and part of the Pacific and Atlantic Oceans (Fig. 1 of NAEC_Catalogue_v1_Documentation.pdf).

The main steps are described below:

i) Data pre-processing:

First, the relative vorticity field at the 850-hPa level is calculated using the zonal and meridional 850-hPa wind fields. Then, the 850-hPa relative vorticity (VORS) and the mean sea-level pressure (MSLP) fields are spatially smoothed using a Cressman filter with a radius of 400 km.

ii) Cyclone center identification:

Cyclone centers are identified based on two conditions: (1) the center must be a local minimum in the MSLP (MSLPmin) but no pressure threshold is enforced, and (2) the maximum VORS (VORSmax) within a 200-km radius must be larger than 10-5 s-1. This vorticity threshold has been used in other studies (e.g., Priestley et al., 2020), and VORSmax is often used to characterize the ETC intensity. If two or more low-pressure centers are found in this circular region, only the lowest pressure center is retained.

iii) Cyclones tracking:

For every existing cyclone center at the current time (t0; noted as At0), the algorithm first predicts its next location (noted as Apt1) by assuming that the storm shifts with the same direction and distance as between its two previous locations (when available). Then, in the following time frame (t1), the closest storm center (noted as Xt1) is matched to the existing storm if its distance to the predicted location (i.e., the distance between Xt1 and Apt1) is smaller than the shifting distance (i.e., distance between At0 and Apt1) or a specified threshold, whichever is greater. We choose 100 km for the threshold with the hourly ERA5, considering that the translation speed of ETC is about 50 km/h on average (Bernhardt & DeGaetano, 2012). The threshold is extended to 150 km if the pressure of the center to be matched deviates less than ± 3 hPa from the existing storm’s value at t0. If no matching is found, the program restarts the matching by assuming that storm remains at the current location (Apt1=At0). If it still finds no match, the tracking of the existing storm ends. The centers that cannot be matched will be viewed as new tracks.

iv) Duration filtering:

Cyclone tracks lasting less than 24 h or traveling a distance smaller than 1000 km are discarded. This is commonly done to filter out thermal lows and small systems (e.g., Neu et al. 2013).


There are in total 24,604 cyclones tracked during this 42-yr period. The tracking results are qualitatively consistent with past studies, with high cyclone center density over the maritime storm tracks and on the lee-side of the Rockies, Great Lakes, and the Hudson Bay over North America (Neu et al., 2013; Fig. 2 of NAEC_Catalogue_v1_Documentation.pdf). While the magnitude of cyclone center density varies significantly across different algorithms, our results lie within the reported range but in the lower part of 15 commonly-used cyclone tracking algorithms presented in Neu et al. (2013).

------------------------------------------------------------
DATA FILE CONTENT INFORMATION
------------------------------------------------------------

-Number of Variables: 96 for each cyclone at one time step

-Number of records: 24,604 cyclone tracks (each track has the entire lifetime information at 1h resolution)

-List of variables, definitions and abbreviations, units of measurement, codes or symbols used:

Each tracked cyclone is given a unique number, and the associated characteristics are listed in chronological order of its lifetime ("lifetime", where 1 indicates the time when the cyclone is first identified). Basic information of the ETC is first provided, including

    "storm"     : storm number
    "lifetime"  : the hour of the lifetime for a given ETC
    "datetime"  : real date and time, formatted as YYYYMMDDHH, UTC time)
    "latitude"  : the latitude of the ETC center
    "longitude" : the longitude of the ETC center
    "MSLPmin"   : the minimum mean sea-level pressure (hPa)
    "VORSmax"   : the maximum 850-hPa relative vorticity (s^-1) within a radius of 200 km.

Spatially-averaged variables associated with ETCs are calculated over a circular area surrounding each cyclone center (Fig. 3 in NAEC_Catalogue_v1_Documentation.pdf). Results using different radii of 400, 600, 800 and 1000 km are provided, indicated by the number following “av” (to be multiplied by 100 km, e.g., av04, av06, av08, av10, respectively):

    "VORS_avR"  : 850-hPa relative vorticity (s^-1), averaged over a radius of Rx100 km from center.
    "10WS_avR"  : wind speed at the 10-m height (m s^-1), averaged over a radius of Rx100 km from center.
    "10WG_avR"  : 10-m wind gust since previous post-processing (the past hour) (m s^-1), averaged over a radius of Rx100 km from center.
    "10W2_avR"  : *square of 10-m wind speed (m^2 s^-2), and then averaged over a radius of Rx100 km from center.
    "85WS_avR"  : 850-hPa wind speed (m s^-1), averaged over a radius of R*100 km from center.
    "PREC_acR"  : hourly accumulated total precipitation (mm). The accumulation period is over the 1 hour ending at the validity date and time, e.g., PREC recorded at 0100 UTC indicates the total precipitation accumulatedfrom 0000 UTC to 0100 UTC. Note that a missing value of “-9.999E+03” is set(because precipitation is a forecast filed in ERA5 and there are no precipitation forecast for the first six hours on 1st January 1979).

    "PRE2_avR"  : *square of hourly accumulated precipitation (mm^2), averaged over a radius of Rx100 km from center.
    "TCWV_avR"  : total column water vapor (kg m^-2).

*The square of 10-m wind speed and precipitation (e.g., 10W2_avR and PRE2_avR) are calculated as these measures are found useful for extreme risk assessment as they highlight the local, small-scale but extreme ETC impacts.


When evaluating the hazards brought by an ETC, relative measures may be more pertinent than the absolute magnitudes. For example, a weaker ETC can cause more severe flooding in a climatologically dry region than a stronger ETC in a region where storm prevails and heavy precipitation often occurs. Therefore, studies on extreme ETC risk assessments often examine whether the cyclone induces wind speeds and precipitation that exceed the threshold values based on the local climatology (e.g., Befort et al., 2018; Owen et al., 2021). Here, two different thresholds are tested: the grid-point-based 98th and 99th percentiles of the ERA5 fields during 1979-2020. Given that the total sample size at each grid point is about 368160 (~24 hours x 365.25 days x 42 years), the occurrence of hourly “extreme” records that exceed the 98th and 99th percentile thresholds is about 7363 and 3681, respectively, in 42 years. Note that the absolute value of such percentile-based threshold differs with location (Fig. 4 in NAEC_Catalogue_v1_Documentation.pdf).

In the catalogue, we also calculate the fractional area and the averaged exceedance of extreme records (i.e., grid points where precipitation and 10-m wind speed values exceed the corresponding climatological thresholds) near each ETC center:

    "WS98_frR"  : the fractional area of extreme 10-m wind speeds exceeding the grid-point-based 98th percentile values within a ETC cover, defined as the circular region within Rx100 km from the center. Similar measures are provided using different radii of 200, 400, 600, 800 and 1000 km (indicated as fr02, fr04, fr06, fr08, fr10, respectively). Note that we recommend using 1000 km for general applications (Utsumi et al., 2016).
    "WS99_frR"  : same as WS98_frR, but extremes are defined as those exceed the grid-point-based 99th percentile values.
    "PR98_frR"  : same as WS98_frR, but for the hourly precipitation field.
    "PR99_frR"  : same as WS99_frR, but for the hourly precipitation field.

While the above gives the spatial extent of local extremes given the presence of an ETC, the averaged magnitude of such exceedance is also calculated:

    "WS98_exR"  : the local difference (exceedance) between the recorded 10-m wind speed and the 98th percentile threshold, summed and then averaged over all extreme grid points within the cyclone cover (defined by R*100 km).
    "WS99_exR"  : same as WS98_exR, but extremes are defined as those exceed the grid-point-based 99th percentile values.
    "PR98_exR"  : same as WS98_exR, but for the hourly precipitation field.
    "PR99_exR"  : same as WS99_exR, but for the hourly precipitation field.

Missing value: -9.999E+03

-Data format:

The catalogue is written as an ASCII delimited file (NAEC_1979_2020_v1.csv). The file size is 1.8G. Extracting the targeted variables (columns) or cyclones (rows) and conducting further analysis can be done by using the open-source Python library pandas.
