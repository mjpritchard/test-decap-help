---
aliases: /article/4917-software-migration-2020
categories:
- Software on JASMIN
collection: jasmin-documentation
date: 2020-08-06 15:57:47
description: 'JASMIN software changes: migration to CentOS7 (2020)'
slug: software-migration-2020
title: 'JASMIN software changes: migration to CentOS7 (2020)'
---

This article explains the changes in the provision of common software on
JASMIN ("sci" servers and LOTUS) when upgrading to main operating system from
RedHat Enterprise Linux 6 (RHEL6) to CentOS7. It answers for the following
questions:

  * What is changing?
  * Which systems are affected?
  * Why is it changing?
  * Comparison of packages in old JASMIN Analysis Platform and new Jaspy/"jasmin-sci" environments
  * How do I get started (quickly)?

## What is changing?

The upgrade from RHEL6 to introduces a new way of working with software
environments on JASMIN.

The previous system involved installations via RPM using a collection of
packages known as the "JASMIN Analysis Platform" (JAP).

The current system uses two approaches to providing software environments and
packages:

  1. Jaspy environments – a collection of software environments that you can "activate" for use.
  2. "jasmin-sci" environment – a single set of software packages installed separately because they were difficult to include in Jaspy.

## Which systems are affected?

This change applies to all generally available JASMIN servers and the LOTUS
cluster. These include:

  * jasmin-sci*
  * cems-sci*
  * jasmin-cylc
  * cron
  * All LOTUS nodes (accessed via LSF)

## Why is it changing?

The reason for moving away from the JAP was to provide a system that could
support multiple versions of software packages, and environments, on a single
platform. From the perspective of reproducible science, the [Jaspy]({{< ref
"jaspy-envs" >}}) approach is more useful because it:

  * keeps previous environments on the system when a new version of an environment is launched
  * includes a listing of all packages (and their versions) that are provided in each date-stamped software environment

From a management point-of-view, Jaspy builds on the packaging tool
"[conda](https://docs.conda.io/en/latest/)" and the community repositories
known as "[conda-forge](https://conda-forge.org/)". These tools are widely
used in the scientific community and provide many components that are re-used
in Jaspy.

## Comparison of packages in old JASMIN Analysis Platform and new
Jaspy/"jasmin-sci" environments

Most packages that were previously provided as part of the JASMIN Analysis
Platform (JAP) are now included in Jaspy environments or the "jasmin-sci"
environment. Some packages have however been dropped. The treatment of certain
packages is documented on the "[extra-sci-
packages](https://github.com/cedadev/extra-sci-packages)" GitHub repository. A
full table of packages that were in JAP and their mappings to Jaspy/"jasmin-
sci" is provided below.

## How do I get started (quickly)?

If you want to access most of the packages you can find them in the most
recent Jaspy environment. This can be activated using:

    
    
     module load jaspy
    

If you need packages that are provided in the "jasmin-sci" environment then
you can activate it using:

    
    
     module load jasmin-sci
    

## Full table of packages from JAP

Here is a full table of packages that were provided via JAP, and how they are
provided for use on CentOS7 machines (as of initial release).

In the summary column:

  * **C** \- package is provided via Conda environment (i.e. Jaspy)
  * **R** \- package is provided via an RPM (as part of the base OS or via jasmin-sci)
  * **CR** \- package is provided both via Jaspy and via an RPM. The version in Jaspy is recommended for use with user code; the RPM version is also installed in order to satisfy an RPM dependency only, and may be subject to change.
  * **N** \- not provided (mostly these have been deprecated by the third-party sources)

**NAME (in JAP)** | **Version in Jaspy 3.7 (conda)** | **Version in Jaspy 2.7 (conda)** | **Version in RPMs (base or jasmin-sci SCL)** | **Summary:** **(C)onda/** **(R)PM /** **(N)one** | **Comments**  
---|---|---|---|---|---  
arpack  |  3.6.3  |  3.6.3  |  |  C  |  
atlas  |  |  3.8.4  |  3.10.1  |  R  |  
atlas-devel  |  |  3.8.4  |  3.10.1  |  R  |  
bbcp  |  |  |  |  N  |  deprecated  
bbcp-config  |  |  |  |  N  |  deprecated  
blas  |  1.1  |  1.0  |  |  C  |  
boost-devel  |  |  1.70.0  |  |  C  |  
cdo  |  1.9.5  |  |  |  C  |  
cmip6-cmor-tables  |  |  |  |  N  |  groups advised to maintain own CMOR  
cmor-libs  |  |  |  |  N  |  groups advised to maintain own CMOR  
coda  |  |  0.19_1  |  |  C  |  
ddd  |  |  |  3.3.12  |  R  |  
diffuse  |  |  |  0.4.8  |  R  |  
dvipng  |  |  |  1.14  |  R  |  package texlive-dvipng-svn26689  
eccodes  |  2.9.2  |  |  |  C  |  
eccodes-devel  |  2.9.2  |  |  |  C  |  
eccodes-fortran  |  2.9.2  |  |  |  C  |  
eccodes-python27  |  2.9.2  |  |  |  C  |  
emacs  |  |  26.1  |  24.3  |  R  |  _emacs is broken in jaspy 2.7_ \-
/usr/bin/emacs may be required to override  
emacs-common-ess  |  |  |  |  N  |  might provide later  
emacs-ess  |  |  |  |  N  |  might provide later  
emacs-ess-el  |  |  |  |  N  |  might provide later  
emacs-gnuplot  |  |  |  4.6.2  |  R  |  
emos  |  |  |  |  N  |  deprecated  
esmf  |  7.1.0r  |  7.1.0r  |  |  C  |  
esmf-doc  |  |  |  |  N  | See [here](http://www.earthsystemmodeling.org/esmf_releases/public/last/ESMF_usrdoc/) and ESMF_refdoc  
esmf-python27  |  7.1.0r  |  7.1.0r  |  |  C  |  
ferret  |  |  |  7.5.0  |  R  |  
fftw  |  3.3.8  |  3.3.8  |  |  C  |  
fftw-devel  |  3.3.8  |  3.3.8  |  |  C  |  
firefox  |  |  |  |  N  |  
flex-devel  |  |  2.6.4  |  |  C  |  
gcc-gfortran  |  |  |  4.8.5  |  R  |  
gdal  |  2.2.4  |  2.0.0  |  |  C  |  
gdal-devel  |  |  |  |  N  |  gdal provided as "gdal"  
gdal-doc  |  |  |  |  N  |  gdal provided as "gdal"  
gdal-java  |  |  |  |  N  |  
gdal-javadoc  |  |  |  |  N  |  
gdal-libs  |  |  |  |  N  |  
gdal-perl  |  |  |  |  N  |  
gdal-python27  |  2.2.4  |  2.0.0  |  |  C  |  
geany  |  |  |  1.31  |  R  |  
geos  |  3.6.2  |  3.7.1  |  |  C  |  
geos-devel  |  3.6.2  |  3.7.1  |  3.4.2  |  R  |  
git  |  2.20.1  |  2.20.1  |  |  C  |  
gitk  |  |  |  1.8.3.1  |  R  |  
glibc-static  |  |  |  2.17  |  R  |  
gnuplot  |  |  |  4.6.2  |  R  |  
grads  |  |  |  2.0.2  |  R  |  
GraphicsMagick-c++  |  |  |  1.3.32  |  R  |  
graphviz  |  2.38.0  |  2.38.0  |  |  C  |  
graphviz-gd  |  |  |  |  N  |  
graphviz-python27  |  2.38.0  |  2.38.0  |  |  C  |  
grass  |  |  |  6.4.4  |  R  |  
grass-devel  |  |  |  6.4.4  |  R  |  
grass-libs  |  |  |  6.4.4  |  R  |  
grib_api  |  |  |  |  N  |  deprecated - use eccodes  
grib_api-devel  |  |  |  |  N  |  deprecated - use eccodes  
grib_api-fortran  |  |  |  |  N  |  deprecated - use eccodes  
grib_api-python27  |  |  |  |  N  |  deprecated - use eccodes  
gsl  |  2.2.1  |  2.5  |  |  C  |  
gsl-devel  |  2.2.1  |  2.5  |  |  C  |  
gsl-static  |  2.2.1  |  2.5  |  |  C  |  
gtk2  |  2.24.31  |  |  |  C  |  
gtk2-devel  |  2.24.31  |  |  |  C  |  
gv  |  |  |  3.7.4  |  R  |  
hdf  |  4.2.13  |  4.2.13  |  |  C  |  
hdf-devel  |  4.2.13  |  4.2.13  |  |  C  |  
hdf5  |  1.10.3  |  1.10.1  |  |  C  |  
hdf5-devel  |  1.10.3  |  1.10.1  |  |  C  |  
hdfeos2  |  2.2  |  2.20  |  20.1.00  |  CR  |  
hdfeos5  |  5.1.16  |  5.1.16  |  |  C  |  
ImageMagick  |  7.0.8_16  |  7.0.8_10  |  |  C  |  
JAGS  |  |  |  |  N  |  available as "rjags"  
jasper-devel  |  1.900.1  |  2.0.14  |  |  C  |  
ksh  |  |  |  20120801  |  R  |  
lapack  |  3.6.1  |  3.6.1  |  |  C  |  
lapack-devel  |  3.6.1  |  3.6.1  |  |  C  |  
leafpad  |  |  |  0.8.18  |  R  |  
libcdms  |  3.1.0  |  3.0.1  |  |  C  |  
libcrayutil  |  |  |  20121128  |  R  |  
libcurl-devel  |  |  |  7.29.0  |  R  |  
libdrs  |  3.1.0  |  3.1.0  |  3.1.2  |  CR  |  
libuuid-devel  |  2.32.1  |  2.32.1  |  2.23.2  |  CR  |  
llvm-devel  |  |  3.3  |  |  C  |  
lxterminal  |  |  |  0.3.2  |  R  |  
mercurial  |  |  4.9.1  |  2.6.2  |  R  |  
mo_unpack  |  |  |  2.0.1  |  R  |  
mtk  |  |  |  1.4.5  |  R  |  
mtk-devel  |  |  |  1.4.5  |  R  |  
mtk-python27  |  |  |  |  N  |  see build instructions for user  
ncBrowse  |  |  |  |  N  |  deprecated  
nccmp  |  |  |  1.8.3.1  |  R  |  
ncl  |  6.5.0  |  |  |  C  |  
nco  |  4.7.8  |  |  |  C  |  
nco-devel  |  4.7.8  |  |  |  C  |  
ncview  |  |  |  2.1.2  |  R  |  
nedit  |  |  |  5.7  |  R  |  
netcdf  |  4.6.1  |  4.6.1  |  4.3.3.1  |  CR  |  called libnetcdf in conda  
netcdf-c++  |  4.2.1  |  4.3.0  |  |  C  |  called netcdf-cxx4 in conda  
netcdf-c++-devel  |  4.2.1  |  4.3.0  |  |  C  |  called netcdf-cxx4 in conda  
netcdf-devel  |  4.6.1  |  4.6.1  |  4.3.3.1  |  CR  |  called libnetcdf in
conda  
netcdf-fortran  |  4.4.4  |  4.4.4  |  4.2  |  CR  |  
netcdf-fortran-devel  |  4.4.4  |  4.4.4  |  4.2  |  CR  |  
octave  |  |  |  3.8.2  |  R  |  
octave-devel  |  |  |  3.8.2  |  R  |  
octave-doc  |  |  |  |  N  |  docs are on <https://octave.org/doc/>  
octave-netcdf  |  |  |  1.0.6  |  R  |  
octave-octcdf  |  |  |  |  N  |  deprecated  
p7zip  |  |  |  16.02  |  R  |  
parallel  |  |  20190522  |  |  C  |  
pdftk  |  |  |  |  N  |  discontinued  
perl-core  |  |  |  5.16.3  |  R  |  
perl-devel  |  |  |  5.16.3  |  R  |  
perl-Image-ExifTool  |  |  |  11.7  |  R  |  
perl-XML-Parser  |  |  2.44_01  |  |  C  |  
postgresql-devel  |  |  |  9.2.24  |  R  |  
proj  |  4.9.3  |  5.2.0  |  4.8.0  |  CR  |  called proj4 in conda  
proj-devel  |  4.9.3  |  5.2.0  |  4.8.0  |  CR  |  called proj4 in conda  
proj-epsg  |  4.9.3  |  5.2.0  |  4.8.0  |  CR  |  called proj4 in conda  
proj-nad  |  4.9.3  |  5.2.0  |  4.8.0  |  CR  |  called proj4 in conda  
proj-static  |  4.9.3  |  5.2.0  |  4.8.0  |  CR  |  called proj4 in conda  
python27  |  3.7.1  |  2.7.15  |  |  C  |  
python27-alabaster  |  0.7.12  |  0.7.12  |  |  C  |  
python27-astral  |  |  1.9.2  |  |  C  |  
python27-Babel  |  2.6.0  |  2.7.0  |  |  C  |  
python27-backports-common  |  |  1.0  |  |  C  |  
python27-backports-functools_lru_cache  |  |  1.5  |  |  C  |  
python27-backports-ssl_match_hostname  |  |  1.0  |  |  C  |  
python27-basemap  |  1.2.0  |  1.2.0  |  |  C  |  
python27-biggus  |  |  0.15.0  |  |  C  |  
python27-boto3  |  1.9.67  |  1.9.188  |  |  C  |  
python27-botocore  |  1.12.68  |  1.12.188  |  |  C  |  
python27-cartopy  |  0.17.0  |  0.16.0  |  |  C  |  
python27-ccplot  |  |  |  |  P  |  
python27-cdat_lite  |  |  |  |  N  |  deprecated  
python27-cerbere  |  |  |  |  N  |  
python27-certifi  |  2018.11.29  |  |  |  C  |  
python27-cf  |  |  2.3.6  |  |  C  |  called cf-python in conda  
python27-cf-checker  |  |  3.1.1  |  |  C  |  
python27-cf-plot  |  |  2.4.10  |  |  C  |  
python27-cf-units  |  2.0.2  |  2.1.1  |  |  C  |  
python27-cf-view  |  |  |  |  N  |  no longer supported  
python27-cftime  |  1.0.3.4  |  1.0.1  |  |  C  |  
python27-chardet  |  3.0.4  |  3.0.4  |  |  C  |  
python27-cis  |  |  1.6.0  |  |  C  |  
python27-cloudpickle  |  0.6.1  |  1.2.1  |  |  C  |  
python27-cmor  |  |  |  |  N  |  groups advised to maintain own CMOR  
python27-cycler  |  0.10.0  |  0.10.0  |  |  C  |  
python27-Cython  |  0.29.2  |  0.29.12  |  |  C  |  
python27-dask  |  1.0.0  |  1.2.2  |  |  C  |  
python27-dateutil  |  |  |  |  C  |  As "dateutil"  
python27-descartes  |  1.1.0  |  1.1.0  |  |  C  |  
python27-docutils  |  0.14  |  0.14  |  |  C  |  
python27-ecmwf-api-client  |  |  |  |  N  |  To be added soon.  
python27-emcee  |  2.2.1  |  2.2.1  |  |  C  |  
python27-enum34  |  |  1.1.6  |  |  C  |  
python27-eofs  |  1.3.1  |  1.4.0  |  |  C  |  
python27-esgf-pyclient  |  |  0.1.8  |  |  C  |  
python27-filelock  |  3.0.10  |  3.0.10  |  |  C  |  
python27-Fiona  |  1.7.13  |  |  |  C  |  
python27-geopandas  |  0.4.0  |  |  |  C  |  
python27-h5py  |  2.8.0  |  2.8.0  |  |  C  |  
python27-httplib2  |  |  0.13.0  |  |  C  |  
python27-idna  |  2.8  |  2.8  |  |  C  |  
python27-ilamb  |  |  2.3.1  |  |  C  |  
python27-ImageHash  |  4.0  |  4.0  |  |  C  |  
python27-imagesize  |  1.1.0  |  1.1.0  |  |  C  |  
python27-ipython  |  7.2.0  |  5.8.0  |  |  C  |  
python27-iris_sample_data  |  2.1.0  |  2.1.0  |  |  C  |  
python27-iris-grib  |  |  0.12.0  |  |  C  |  
python27-jinja2  |  2.1  |  2.10.1  |  |  C  |  
python27-jmespath  |  0.9.3  |  0.9.4  |  |  C  |  
python27-joblib  |  0.13.0  |  0.13.2  |  |  C  |  
python27-Jug  |  1.6.7  |  1.6.8  |  |  C  |  
python27-kiwisolver  |  1.0.1  |  1.1.0  |  |  C  |  
python27-latexcodec  |  1.0.5  |  1.0.7  |  |  C  |  
python27-locket  |  0.2.0  |  0.2.0  |  |  C  |  
python27-MarkupSafe  |  1.1.0  |  1.1.1  |  |  C  |  
python27-matplotlib  |  3.0.2  |  2.2.2  |  |  C  |  
python27-mo_pack  |  0.2.0  |  0.2.0  |  |  C  |  
python27-mock  |  2.0.0  |  3.0.5  |  |  C  |  
python27-mpi4py-mpich  |  |  3.0.1  |  |  C  |  
python27-mpmath  |  1.1.0  |  1.1.0  |  |  C  |  
python27-nappy  |  1.1.4  |  1.2.1  |  |  C  |  
python27-nc-time-axis  |  1.1.0  |  1.1.0  |  |  C  |  
python27-netCDF4  |  1.4.2  |  1.3.1  |  |  C  |  
python27-nose  |  1.3.7  |  1.3.7  |  |  C  |  
python27-numpy  |  1.15.4  |  1.15.4  |  |  C  |  
python27-packaging  |  18.0  |  19.0  |  |  C  |  
python27-pandas  |  0.23.4  |  0.24.2  |  |  C  |  
python27-partd  |  0.3.9  |  1.0.0  |  |  C  |  
python27-patsy  |  0.5.1  |  0.5.1  |  |  C  |  
python27-pep8  |  1.7.1  |  1.7.1  |  |  C  |  
python27-Pillow  |  5.3.0  |  5.2.0  |  |  C  |  
python27-psutil  |  5.4.8  |  5.6.3  |  |  C  |  
python27-psycopg2  |  2.7.6.1  |  2.7.7  |  |  C  |  
python27-pybtex  |  0.22.0  |  0.22.2  |  |  C  |  
python27-pycairo  |  1.18.0  |  1.16.3  |  |  C  |  
python27-pycodestyle  |  2.4.0  |  2.5.0  |  |  C  |  
python27-Pydap  |  3.2.2  |  3.2.2  |  |  C  |  
python27-pygeode  |  |  1.2.2  |  |  C  |  
python27-Pygments  |  2.3.1  |  2.4.2  |  |  C  |  
python27-pygobject2  |  |  3.28.3  |  |  C  |  pygobject in conda  
python27-pygrib  |  2.0.3  |  2.0.2  |  |  C  |  
python27-pygtk2  |  |  |  |  C  |  
python27-pygtk2-libglade  |  |  |  |  N  |  
python27-pyhdf  |  0.9.10  |  0.10.1  |  |  C  |  
python27-pyke  |  1.1.1  |  1.1.1  |  |  C  |  
python27-pyparsing  |  2.3.0  |  2.4.0  |  |  C  |  
python27-pyproj  |  1.9.5.1  |  1.9.6  |  |  C  |  
python27-pyshp  |  2.0.0  |  2.1.0  |  |  C  |  
python27-pyside  |  |  5.6.0a1  |  |  C  |  
python27-pyspharm  |  1.0.9  |  1.0.9  |  |  C  |  
python27-pystan  |  2.17.1.0  |  2.17.1.0  |  |  C  |  
python27-pytz  |  2018.7  |  2019.1  |  |  C  |  
python27-pyugrid  |  0.3.1  |  0.3.1  |  |  C  |  
python27-PyYAML  |  3.13  |  5.1.1  |  |  C  |  
python27-pyzmq  |  17.1.2  |  18.0.2  |  |  C  |  
python27-requests  |  2.21.0  |  2.22.0  |  |  C  |  
python27-rpy2  |  2.9.4  |  2.8.5  |  |  C  |  
python27-s3transfer  |  0.1.13  |  0.2.1  |  |  C  |  
python27-ScientificPython  |  |  |  |  N  |  only available in Python2.7  
python27-scikit-image  |  |  0.14.2  |  |  C  |  
python27-scikit-learn  |  0.20.1  |  0.20.3  |  |  C  |  
python27-scipy  |  1.1.0  |  1.1.0  |  |  C  |  
python27-scitools-iris  |  2.2.0  |  1.13.0  |  |  C  |  
python27-seaborn  |  |  0.9.0  |  |  C  |  
python27-setuptools  |  40.6.3  |  41.0.1  |  |  C  |  
python27-Shapely  |  1.6.4  |  1.6.4  |  |  C  |  
python27-singledispatch  |  |  3.4.0.3  |  |  C  |  
python27-six  |  1.12.0  |  1.12.0  |  |  C  |  
python27-snowballstemmer  |  1.2.1  |  1.9.0  |  |  C  |  
python27-Sphinx  |  1.8.2  |  1.8.5  |  |  C  |  
python27-sphinxcontrib-websupport  |  1.1.0  |  1.1.2  |  |  C  |  
python27-statsmodels  |  0.9.0  |  0.10.0  |  |  C  |  
python27-sympy  |  1.3  |  1.4  |  |  C  |  
python27-Theano  |  1.0.3  |  1.0.4  |  |  C  |  
python27-toolz  |  0.9.0  |  0.10.0  |  |  C  |  
python27-tornado  |  5.1.1  |  5.1.1  |  |  C  |  
python27-tqdm  |  4.28.1  |  4.32.2  |  |  C  |  
python27-typing  |  |  3.7.4  |  |  C  |  
python27-urllib3  |  1.24.1  |  1.25.3  |  |  C  |  
python27-virtualenv  |  16.0.0  |  16.0.0  |  |  C  |  
python27-WebOb  |  1.8.4  |  1.8.5  |  |  C  |  
python27-windspharm  |  1.7.0  |  1.7.0  |  |  C  |  
python27-wxPython  |  4.0.3  |  4.0.3  |  |  C  |  
python27-xarray  |  0.11.0  |  0.11.3  |  |  C  |  
qt-devel  |  |  |  4.8.7  |  R  |  
R  |  3.5.1  |  3.4.1  |  |  C  |  
R-devel  |  3.5.1  |  3.4.1  |  |  C  |  
R-ncdf4  |  1.16  |  1.16  |  |  C  |  
redhat-lsb  |  |  |  4.1  |  R  |  
rjags  |  |  4_6  |  |  C  |  
sqlite-devel  |  |  |  3.7.17  |  R  |  
subversion  |  |  |  1.8.17  |  R  |  
subversion-devel  |  |  |  1.8.17  |  R  |  
subversion-tools  |  |  |  1.8.17  |  R  |  
tcl-devel  |  |  |  8.5  |  R  |  
tcl-devel  |  |  |  8.5.13  |  R  |  
tcsh  |  |  |  6.18.01  |  R  |  
thea  |  |  |  |  N  |  discontinued  
tk  |  8.6.9  |  8.6.9  |  8.5.13  |  CR  |  
tk-devel  |  8.6.9  |  8.6.9  |  8.5.13  |  CR  |  
tkdiff  |  |  |  4.3.5  |  R  |  
tmux  |  2.7  |  2.7  |  |  C  |  
tree  |  |  |  1.6.0  |  R  |  
udunits-devel  |  2.2.27.6  |  2.2.27.6  |  2.2.20  |  R  |  called
udunits2-devel  
umutil  |  |  |  20130102  |  R  |  
umutil-lib  |  |  |  20130102  |  R  |  
uuid  |  |  |  1.6.2  |  R  |  
uuid-devel  |  |  |  1.6.2  |  R  |  
valgrind  |  |  3.15.0  |  |  C  |  
vim-enhanced  |  |  |  7.4.629  |  R  |  
wxGTK-devel  |  |  |  2.8.12  |  R  |  
xconv  |  |  |  1.94  |  R  |  
xemacs  |  |  |  21.5.34  |  R  |  
xorg-x11-util-macros  |  |  |  1.19.0  |  R  |  
xpdf  |  |  |  3.04  |  R  |
{.table .table-striped}