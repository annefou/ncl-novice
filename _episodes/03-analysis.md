---
title: "Data analysis with NCL"
teaching: 0
exercises: 0
questions:
- "What are the NCL data processing tools?"
- "How to interpolate CESM CAM (Community Atmosphere Model) hybrid coordinates to pressure coordinates?"
objectives:
- "Learn about NCL tools"
- "Learn how to use verth2p_ecmwf"
keypoints:
- "NCL data processing environment"
---

# NCL Tools

The following shell commands are included in the NCL software distribution:

### ncl_filedump

It generates an ASCII representation of supported files
(netCDF, HDF, GRIB1, GRIB2, shapefile) on the standard
output. It is similar to the netCDF program called `ncdump –h`.

~~~
ncl_filedump f2000.T31T31.control.cam.h0.0008-12-22-00000.nc
~~~
{: .language-bash}

~~~
 Copyright (C) 1995-2015 - All Rights Reserved
 University Corporation for Atmospheric Research
 NCAR Command Language Version 6.3.0
 The use of this software is governed by a License Agreement.
 See http://www.ncl.ucar.edu/ for more details.

Variable: f
Type: file
filename:	f2000.T31T31.control.cam.h0.0008-12-22-00000
path:	f2000.T31T31.control.cam.h0.0008-12-22-00000.nc
   file global attributes:
      Conventions : CF-1.0
      source : CAM
      case : f2000.T31T31.control
      title : UNSET
      logname : hanbre
      host : hexagon-5
      Version : $Name$
      revision_Id : $Id$
      initial_file : /work/hanbre/inputdata/atm/cam/inic/gaus/cami_0000-01-01_48x96_L30_c100426.nc
      topography_file : /work/hanbre/inputdata/atm/cam/topo/USGS-gtopo30_48x96_c050520.nc
   dimensions:
      ncl_scalar = 1
      lat = 48
      lon = 96
      time = 11  // unlimited
      nbnd = 2
      chars = 8
      lev = 30
      ilev = 31
   variables:
      double lev ( lev )
         long_name :	hybrid level at midpoints (1000*(A+B))
         units :	level
         positive :	down
         standard_name :	atmosphere_hybrid_sigma_pressure_coordinate
         formula_terms :	a: hyam b: hybm p0: P0 ps: PS

      double hyam ( lev )
         long_name :	hybrid A coefficient at layer midpoints

      double hybm ( lev )
         long_name :	hybrid B coefficient at layer midpoints

      double ilev ( ilev )
         long_name :	hybrid level at interfaces (1000*(A+B))
         units :	level
         positive :	down
         standard_name :	atmosphere_hybrid_sigma_pressure_coordinate
         formula_terms :	a: hyai b: hybi p0: P0 ps: PS

      double hyai ( ilev )
         long_name :	hybrid A coefficient at layer interfaces

      double hybi ( ilev )
         long_name :	hybrid B coefficient at layer interfaces

      double P0 ( ncl_scalar )
         long_name :	reference pressure
         units :	Pa

      double time ( time )
         long_name :	time
         units :	days since 0001-01-01 00:00:00
         calendar :	noleap
         bounds :	time_bnds

      integer date ( time )
         long_name :	current date (YYYYMMDD)

      integer datesec ( time )
         long_name :	current seconds of current date

      double lat ( lat )
         long_name :	latitude
         units :	degrees_north

      double lon ( lon )
         long_name :	longitude
         units :	degrees_east

      double time_bnds ( time, nbnd )
         long_name :	time interval endpoints

      character date_written ( time, chars )

      character time_written ( time, chars )

      integer ntrm ( ncl_scalar )
         long_name :	spectral truncation parameter M

      integer ntrn ( ncl_scalar )
         long_name :	spectral truncation parameter N

      integer ntrk ( ncl_scalar )
         long_name :	spectral truncation parameter K

      integer ndbase ( ncl_scalar )
         long_name :	base day

      integer nsbase ( ncl_scalar )
         long_name :	seconds of base day

      integer nbdate ( ncl_scalar )
         long_name :	base date (YYYYMMDD)

      integer nbsec ( ncl_scalar )
         long_name :	seconds of base date

      integer mdt ( ncl_scalar )
         long_name :	timestep
         units :	s

      integer nlon ( lat )
         long_name :	number of longitudes

      integer wnummax ( lat )
         long_name :	cutoff Fourier wavenumber

      double gw ( lat )
         long_name :	gauss weights

      integer ndcur ( time )
         long_name :	current day (from base day)

      integer nscur ( time )
         long_name :	current seconds of current day

      double co2vmr ( time )
         long_name :	co2 volume mixing ratio

      double ch4vmr ( time )
         long_name :	ch4 volume mixing ratio

      double n2ovmr ( time )
         long_name :	n2o volume mixing ratio

      double f11vmr ( time )
         long_name :	f11 volume mixing ratio

      double f12vmr ( time )
         long_name :	f12 volume mixing ratio

      double sol_tsi ( time )
         long_name :	total solar irradiance
         units :	W/m2

      integer nsteph ( time )
         long_name :	current timestep

      float AEROD_v ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	1
         long_name :	Total Aerosol Optical Depth in visible band
         cell_methods :	time: mean

      float ANRAIN ( time, lev, lat, lon )
         mdims :	1
         units :	m-3
         long_name :	Average rain number conc
         cell_methods :	time: mean

      float ANSNOW ( time, lev, lat, lon )
         mdims :	1
         units :	m-3
         long_name :	Average snow number conc
         cell_methods :	time: mean

      float AODDUST1 ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	
         long_name :	Aerosol optical depth 550 nm model 1 from dust
         cell_methods :	time: mean

      float AODDUST3 ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	
         long_name :	Aerosol optical depth 550 nm model 3 from dust
         cell_methods :	time: mean

      float AODVIS ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	
         long_name :	Aerosol optical depth 550 nm
         cell_methods :	time: mean

      float AQRAIN ( time, lev, lat, lon )
         mdims :	1
         units :	kg/kg
         long_name :	Average rain mixing ratio
         cell_methods :	time: mean

      float AQSNOW ( time, lev, lat, lon )
         mdims :	1
         units :	kg/kg
         long_name :	Average snow mixing ratio
         cell_methods :	time: mean

      float AREI ( time, lev, lat, lon )
         mdims :	1
         units :	Micron
         long_name :	Average ice effective radius
         cell_methods :	time: mean

      float AREL ( time, lev, lat, lon )
         mdims :	1
         units :	Micron
         long_name :	Average droplet effective radius
         cell_methods :	time: mean

      float AWNC ( time, lev, lat, lon )
         mdims :	1
         units :	m-3
         long_name :	Average cloud water number conc
         cell_methods :	time: mean

      float AWNI ( time, lev, lat, lon )
         mdims :	1
         units :	m-3
         long_name :	Average cloud ice number conc
         cell_methods :	time: mean

      float BURDEN1 ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	kg/m2
         long_name :	Aerosol burden mode 1
         cell_methods :	time: mean

      float BURDEN2 ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	kg/m2
         long_name :	Aerosol burden mode 2
         cell_methods :	time: mean

      float BURDEN3 ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	kg/m2
         long_name :	Aerosol burden mode 3
         cell_methods :	time: mean

      float BURDENBC ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	kg/m2
         long_name :	Black carbon aerosol burden
         cell_methods :	time: mean

      float BURDENDUST ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	kg/m2
         long_name :	Dust aerosol burden
         cell_methods :	time: mean

      float BURDENPOM ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	kg/m2
         long_name :	POM aerosol burden
         cell_methods :	time: mean

      float BURDENSEASALT ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	kg/m2
         long_name :	Seasalt aerosol burden
         cell_methods :	time: mean

      float BURDENSO4 ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	kg/m2
         long_name :	Sulfate aerosol burden
         cell_methods :	time: mean

      float BURDENSOA ( time, lat, lon )
         _FillValue :	1e+36
         missing_value :	1e+36
         units :	kg/m2
         long_name :	SOA aerosol burden
         cell_methods :	time: mean

      float CCN3 ( time, lev, lat, lon )
         mdims :	1
         units :	#/cm3
         long_name :	CCN concentration at S=0.1%
         cell_methods :	time: mean

      float CDNUMC ( time, lat, lon )
         units :	1/m2
         long_name :	Vertically-integrated droplet concentration
         cell_methods :	time: mean

      float CLDHGH ( time, lat, lon )
         units :	fraction
         long_name :	Vertically-integrated high cloud
         cell_methods :	time: mean

      float CLDICE ( time, lev, lat, lon )
         mdims :	1
         units :	kg/kg
         long_name :	Grid box averaged cloud ice amount
         cell_methods :	time: mean

      float CLDLIQ ( time, lev, lat, lon )
         mdims :	1
         units :	kg/kg
         long_name :	Grid box averaged cloud liquid amount
         cell_methods :	time: mean

      float CLDLOW ( time, lat, lon )
         units :	fraction
         long_name :	Vertically-integrated low cloud
         cell_methods :	time: mean

      float CLDMED ( time, lat, lon )
         units :	fraction
         long_name :	Vertically-integrated mid-level cloud
         cell_methods :	time: mean

      float CLDTOT ( time, lat, lon )
         units :	fraction
         long_name :	Vertically-integrated total cloud
         cell_methods :	time: mean

      float CLOUD ( time, lev, lat, lon )
         mdims :	1
         units :	fraction
         long_name :	Cloud fraction
         cell_methods :	time: mean

      float DCQ ( time, lev, lat, lon )
         mdims :	1
         units :	kg/kg/s
         long_name :	Q tendency due to moist processes
         cell_methods :	time: mean

      float DMS_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	DMS in bottom layer
         cell_methods :	time: mean

      float DTCOND ( time, lev, lat, lon )
         mdims :	1
         units :	K/s
         long_name :	T tendency - moist processes
         cell_methods :	time: mean

      float DTH ( time, lev, lat, lon )
         mdims :	1
         units :	K/s
         long_name :	T horizontal diffusive heating
         cell_methods :	time: mean

      float DTV ( time, lev, lat, lon )
         mdims :	1
         units :	K/s
         long_name :	T vertical diffusion
         cell_methods :	time: mean

      float EMISCLD ( time, lev, lat, lon )
         mdims :	1
         units :	1
         long_name :	cloud emissivity
         cell_methods :	time: mean

      float FICE ( time, lev, lat, lon )
         mdims :	1
         units :	fraction
         long_name :	Fractional ice content within cloud
         cell_methods :	time: mean

      float FLDS ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Downwelling longwave flux at surface
         cell_methods :	time: mean

      float FLNS ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Net longwave flux at surface
         cell_methods :	time: mean

      float FLNSC ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Clearsky net longwave flux at surface
         cell_methods :	time: mean

      float FLNT ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Net longwave flux at top of model
         cell_methods :	time: mean

      float FLNTC ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Clearsky net longwave flux at top of model
         cell_methods :	time: mean

      float FLUT ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Upwelling longwave flux at top of model
         cell_methods :	time: mean

      float FLUTC ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Clearsky upwelling longwave flux at top of model
         cell_methods :	time: mean

      float FREQI ( time, lev, lat, lon )
         mdims :	1
         units :	fraction
         long_name :	Fractional occurrence of ice
         cell_methods :	time: mean

      float FREQL ( time, lev, lat, lon )
         mdims :	1
         units :	fraction
         long_name :	Fractional occurrence of liquid
         cell_methods :	time: mean

      float FREQR ( time, lev, lat, lon )
         mdims :	1
         units :	fraction
         long_name :	Fractional occurrence of rain
         cell_methods :	time: mean

      float FREQS ( time, lev, lat, lon )
         mdims :	1
         units :	fraction
         long_name :	Fractional occurrence of snow
         cell_methods :	time: mean

      float FSDS ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Downwelling solar flux at surface
         cell_methods :	time: mean

      float FSDSC ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Clearsky downwelling solar flux at surface
         cell_methods :	time: mean

      float FSNS ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Net solar flux at surface
         cell_methods :	time: mean

      float FSNSC ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Clearsky net solar flux at surface
         cell_methods :	time: mean

      float FSNT ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Net solar flux at top of model
         cell_methods :	time: mean

      float FSNTC ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Clearsky net solar flux at top of model
         cell_methods :	time: mean

      float FSNTOA ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Net solar flux at top of atmosphere
         cell_methods :	time: mean

      float FSNTOAC ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Clearsky net solar flux at top of atmosphere
         cell_methods :	time: mean

      float FSUTOA ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Upwelling solar flux at top of atmosphere
         cell_methods :	time: mean

      float H2O2_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	H2O2 in bottom layer
         cell_methods :	time: mean

      float H2SO4_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	H2SO4 in bottom layer
         cell_methods :	time: mean

      float ICEFRAC ( time, lat, lon )
         units :	fraction
         long_name :	Fraction of sfc area covered by sea-ice
         cell_methods :	time: mean

      float ICIMR ( time, lev, lat, lon )
         mdims :	1
         units :	kg/kg
         long_name :	Prognostic in-cloud ice mixing ratio
         cell_methods :	time: mean

      float ICWMR ( time, lev, lat, lon )
         mdims :	1
         units :	kg/kg
         long_name :	Prognostic in-cloud water mixing ratio
         cell_methods :	time: mean

      float IWC ( time, lev, lat, lon )
         mdims :	1
         units :	kg/m3
         long_name :	Grid box average ice water content
         cell_methods :	time: mean

      float LANDFRAC ( time, lat, lon )
         units :	fraction
         long_name :	Fraction of sfc area covered by land
         cell_methods :	time: mean

      float LHFLX ( time, lat, lon )
         units :	W/m2
         long_name :	Surface latent heat flux
         cell_methods :	time: mean

      float LWCF ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Longwave cloud forcing
         cell_methods :	time: mean

      float NUMICE ( time, lev, lat, lon )
         mdims :	1
         units :	1/kg
         long_name :	Grid box averaged cloud ice number
         cell_methods :	time: mean

      float NUMLIQ ( time, lev, lat, lon )
         mdims :	1
         units :	1/kg
         long_name :	Grid box averaged cloud liquid number
         cell_methods :	time: mean

      float OCNFRAC ( time, lat, lon )
         units :	fraction
         long_name :	Fraction of sfc area covered by ocean
         cell_methods :	time: mean

      float OMEGA ( time, lev, lat, lon )
         mdims :	1
         units :	Pa/s
         long_name :	Vertical velocity (pressure)
         cell_methods :	time: mean

      float OMEGAT ( time, lev, lat, lon )
         mdims :	1
         units :	K Pa/s
         long_name :	Vertical heat flux
         cell_methods :	time: mean

      float ORO ( time, lat, lon )
         units :	frac
         long_name :	ORO
         cell_methods :	time: mean

      float PBLH ( time, lat, lon )
         units :	m
         long_name :	PBL height
         cell_methods :	time: mean

      float PHIS ( time, lat, lon )
         units :	m2/s2
         long_name :	Surface geopotential

      float PRECC ( time, lat, lon )
         units :	m/s
         long_name :	Convective precipitation rate (liq + ice)
         cell_methods :	time: mean

      float PRECL ( time, lat, lon )
         units :	m/s
         long_name :	Large-scale (stable) precipitation rate (liq + ice)
         cell_methods :	time: mean

      float PRECSC ( time, lat, lon )
         units :	m/s
         long_name :	Convective snow rate (water equivalent)
         cell_methods :	time: mean

      float PRECSL ( time, lat, lon )
         units :	m/s
         long_name :	Large-scale (stable) snow rate (water equivalent)
         cell_methods :	time: mean

      float PS ( time, lat, lon )
         units :	Pa
         long_name :	Surface pressure
         cell_methods :	time: mean

      float PSL ( time, lat, lon )
         units :	Pa
         long_name :	Sea level pressure
         cell_methods :	time: mean

      float Q ( time, lev, lat, lon )
         mdims :	1
         units :	kg/kg
         long_name :	Specific humidity
         cell_methods :	time: mean

      float QFLX ( time, lat, lon )
         units :	kg/m2/s
         long_name :	Surface water flux
         cell_methods :	time: mean

      float QREFHT ( time, lat, lon )
         units :	kg/kg
         long_name :	Reference height humidity
         cell_methods :	time: mean

      float QRL ( time, lev, lat, lon )
         mdims :	1
         Sampling_Sequence :	rad_lwsw
         units :	K/s
         long_name :	Longwave heating rate
         cell_methods :	time: mean

      float QRS ( time, lev, lat, lon )
         mdims :	1
         Sampling_Sequence :	rad_lwsw
         units :	K/s
         long_name :	Solar heating rate
         cell_methods :	time: mean

      float RELHUM ( time, lev, lat, lon )
         mdims :	1
         units :	percent
         long_name :	Relative humidity
         cell_methods :	time: mean

      float SHFLX ( time, lat, lon )
         units :	W/m2
         long_name :	Surface sensible heat flux
         cell_methods :	time: mean

      float SNOWHICE ( time, lat, lon )
         units :	m
         long_name :	Snow depth over ice
         cell_methods :	time: mean

      float SNOWHLND ( time, lat, lon )
         units :	m
         long_name :	Water equivalent snow depth
         cell_methods :	time: mean

      float SO2_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	SO2 in bottom layer
         cell_methods :	time: mean

      float SOAG_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	SOAG in bottom layer
         cell_methods :	time: mean

      float SOLIN ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Solar insolation
         cell_methods :	time: mean

      float SWCF ( time, lat, lon )
         Sampling_Sequence :	rad_lwsw
         units :	W/m2
         long_name :	Shortwave cloud forcing
         cell_methods :	time: mean

      float T ( time, lev, lat, lon )
         mdims :	1
         units :	K
         long_name :	Temperature
         cell_methods :	time: mean

      float TAUX ( time, lat, lon )
         units :	N/m2
         long_name :	Zonal surface stress
         cell_methods :	time: mean

      float TAUY ( time, lat, lon )
         units :	N/m2
         long_name :	Meridional surface stress
         cell_methods :	time: mean

      float TGCLDCWP ( time, lat, lon )
         units :	kg/m2
         long_name :	Total grid-box cloud water path (liquid and ice)
         cell_methods :	time: mean

      float TGCLDIWP ( time, lat, lon )
         units :	kg/m2
         long_name :	Total grid-box cloud ice water path
         cell_methods :	time: mean

      float TGCLDLWP ( time, lat, lon )
         units :	kg/m2
         long_name :	Total grid-box cloud liquid water path
         cell_methods :	time: mean

      float TMQ ( time, lat, lon )
         units :	kg/m2
         long_name :	Total (vertically integrated) precipitable water
         cell_methods :	time: mean

      float TREFHT ( time, lat, lon )
         units :	K
         long_name :	Reference height temperature
         cell_methods :	time: mean

      float TS ( time, lat, lon )
         units :	K
         long_name :	Surface temperature (radiative)
         cell_methods :	time: mean

      float TSMN ( time, lat, lon )
         units :	K
         long_name :	Minimum surface temperature over output period
         cell_methods :	time: minimum

      float TSMX ( time, lat, lon )
         units :	K
         long_name :	Maximum surface temperature over output period
         cell_methods :	time: maximum

      float U ( time, lev, lat, lon )
         mdims :	1
         units :	m/s
         long_name :	Zonal wind
         cell_methods :	time: mean

      float U10 ( time, lat, lon )
         units :	m/s
         long_name :	10m wind speed
         cell_methods :	time: mean

      float UU ( time, lev, lat, lon )
         mdims :	1
         units :	m2/s2
         long_name :	Zonal velocity squared
         cell_methods :	time: mean

      float V ( time, lev, lat, lon )
         mdims :	1
         units :	m/s
         long_name :	Meridional wind
         cell_methods :	time: mean

      float VD01 ( time, lev, lat, lon )
         mdims :	1
         units :	kg/kg/s
         long_name :	Vertical diffusion of Q
         cell_methods :	time: mean

      float VQ ( time, lev, lat, lon )
         mdims :	1
         units :	m/skg/kg
         long_name :	Meridional water transport
         cell_methods :	time: mean

      float VT ( time, lev, lat, lon )
         mdims :	1
         units :	K m/s
         long_name :	Meridional heat transport
         cell_methods :	time: mean

      float VU ( time, lev, lat, lon )
         mdims :	1
         units :	m2/s2
         long_name :	Meridional flux of zonal momentum
         cell_methods :	time: mean

      float VV ( time, lev, lat, lon )
         mdims :	1
         units :	m2/s2
         long_name :	Meridional velocity squared
         cell_methods :	time: mean

      float WGUSTD ( time, lat, lon )
         units :	m/s
         long_name :	wind gusts from turbulence
         cell_methods :	time: mean

      float WSUB ( time, lev, lat, lon )
         mdims :	1
         units :	m/s
         long_name :	Diagnostic sub-grid vertical velocity
         cell_methods :	time: mean

      float Z3 ( time, lev, lat, lon )
         mdims :	1
         units :	m
         long_name :	Geopotential Height (above sea level)
         cell_methods :	time: mean

      float bc_a1_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	bc_a1 in bottom layer
         cell_methods :	time: mean

      float dst_a1SF ( time, lat, lon )
         units :	kg/m2/s
         long_name :	dst_a1 dust surface emission
         cell_methods :	time: mean

      float dst_a1_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	dst_a1 in bottom layer
         cell_methods :	time: mean

      float dst_a3SF ( time, lat, lon )
         units :	kg/m2/s
         long_name :	dst_a3 dust surface emission
         cell_methods :	time: mean

      float dst_a3_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	dst_a3 in bottom layer
         cell_methods :	time: mean

      float ncl_a1_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	ncl_a1 in bottom layer
         cell_methods :	time: mean

      float ncl_a2_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	ncl_a2 in bottom layer
         cell_methods :	time: mean

      float ncl_a3_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	ncl_a3 in bottom layer
         cell_methods :	time: mean

      float num_a1_SRF ( time, lat, lon )
         units :	 1/kg
         long_name :	num_a1 in bottom layer
         cell_methods :	time: mean

      float num_a2_SRF ( time, lat, lon )
         units :	 1/kg
         long_name :	num_a2 in bottom layer
         cell_methods :	time: mean

      float num_a3_SRF ( time, lat, lon )
         units :	 1/kg
         long_name :	num_a3 in bottom layer
         cell_methods :	time: mean

      float pom_a1_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	pom_a1 in bottom layer
         cell_methods :	time: mean

      float so4_a1_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	so4_a1 in bottom layer
         cell_methods :	time: mean

      float so4_a2_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	so4_a2 in bottom layer
         cell_methods :	time: mean

      float so4_a3_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	so4_a3 in bottom layer
         cell_methods :	time: mean

      float soa_a1_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	soa_a1 in bottom layer
         cell_methods :	time: mean

      float soa_a2_SRF ( time, lat, lon )
         units :	kg/kg
         long_name :	soa_a2 in bottom layer
         cell_methods :	time: mean
~~~
{: .output}


### ncl_convert2nc 

It converts GRIB1, GRIB2, shapefile, HDF, or HDF-EOS files to NetCDF files

### ng4ex

`ng4ex`is a script for generating hundreds of available C, Fortran,
and NCL object-oriented examples.

### WRAPIT 

It wraps Fortran 77 or 90 code so you can call it directly from NCL

# Data processing with NCL

Prior to visualization, it is quite often necessary to apply additional processing steps to the original data. 

For processing NetCDF data, we recommend you to use separate tools such as [CDO](https://code.mpimet.mpg.de/projects/cdo/) or [NCO](http://nco.sourceforge.net/). These tools are designed to efficiently perform specific tasks and are usually be more efficient than NCL. 

However, for specific tasks such as vertical interpolation and regridding, we recommend to use NCL.

### Interpolation from CAM hybrid coordinates to pressure coordinates

It is very often handy to interpolate from CAM hybrid coordinates to pressure coordinates, especially when you need to compare with other models or observations.

NCL provides a built-in function called `vinth2p_ecmwf`. 

~~~
f = addfile("f2000.T31T31.control.cam.h0.0008-12-22-00000.nc","r")
T = f->T                                    ; get temperature
P0mb = 0.01*f->P0                           ; get reference pressure
hyam = f->hyam                              ; get a coefficiants
hybm = f->hybm                              ; get b coefficiants
PS   = f->PS                                ; get pressure
PHIS = f->PHIS                              ; get surface geopotential

; vector containing the new pressure levels 
pnew = (/ 850.0,700.0,500.0,300.0,200.0 /)

nlev = dimsizes(hyam)
tbot = T(nlev-1,:,:) 
T_p =vinth2p_ecmwf(T,hyam,hybm,pnew, \
	           PS,1,P0mb,1,      \
                   True,1,tbot,PHIS)

~~~
{: .language-bash}

* The first `1` in the call to `vinth2p_ecmwf` corresponds to the type of interpolation:
   * 1 LINEAR, 
   * 2 LOG, 
   * 3 LOG LOG

* The second 1 is a parameter that is not used yet (for future improvement of this function) and should always be set to 1).

* The parameter set to True means we allow extrapolation. If set to False = no extrapolation when the pressure level is outside of the range of psfc.

* The last `1` in the call is used to specify which variable you are willing to interpolate. This is due to the fact that `vint2p_ecmwf` applies different algorithm for temperature (=1), geopotential height (=-1) or other variables (=0).

* tbot is an array with the same sizes as psfc equal to temperature at the lowest (i.e, closest to the surface) level. While this is used only if varflg=-1 (ie, geopotential height), it must still be provided for all cases.

For more information see [here](https://www.ncl.ucar.edu/Document/Functions/Built-in/vinth2p_ecmwf.shtml)

### NCL regridding

NCL regridding tools required to install ESMF regridding tools but since NCL 6.4.0, they are now fully integrated to NCL, simplifying their usage and installation.
