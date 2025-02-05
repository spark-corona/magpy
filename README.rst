MagPy
=====

**MagPy (or GeomagPy) is a Python package for analysing and displaying
geomagnetic data.**

Version Info: (please note: this package is still in a development state
with frequent modifcations) please check the release notes.

MagPy provides tools for geomagnetic data analysis with special focus on
typical data processing routines in observatories. MagPy provides
methods for data format conversion, plotting and mathematical procedures
with specifically geomagnetic analysis routines such as basevalue and
baseline calculation and database handling. Among the supported data
formats are *ImagCDF, IAGA-02, WDC, IMF, IAF, BLV*, and many more. Full
installation also provides a graphical user interface, *xmagpy*.

Typical usage for reading and visualising data looks like this:

::

        #!/usr/bin/env python

        from magpy.stream import read
        import magpy.mpplot as mp
        stream = read(path_or_url='filename')
        mp.plot(stream)

Below you will find a quick guide to usage of the MagPy package. The
quickest approach can be accomplished when skipping everything except
the tutorials.

1. INSTALLATION
---------------

1.1 Windows installation - WinPython Package
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1.1.1 Install NASA `CDF <https://cdf.gsfc.nasa.gov/>`__ support
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  enables CDF support for formats like ImagCDF
-  package details and files at http://cdf.gsfc.nasa.gov/
-  download and install a recent version of CDF e.g.
   cdf36\_2\_1-setup-32.exe
-  Note: please use 32 bit installer.

1.1.2 Install MagPy for Windows
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  find the MagPy Windows installer here (under Downloads):
   http://www.conrad-observatory.at
-  download and execute magpy-0.x.x.exe
-  all required packages are included in the installer

1.1.3 Post-installation information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  MagPy should have a sub-folder in the Start menu. Here you will find
   two items:

   ::

       * python -> opens a python shell ready for MagPy
       * xmagpy -> opens the MagPy graphical user interface

1.2 Linux/MacOs installation - Anaconda
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1.2.1 Install `Anaconda <https://www.continuum.io/downloads>`__ on your operating system
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  download files from https://www.continuum.io/Downloads (tested with
   Anaconda2 for Python 2.7)
-  see https://docs.continuum.io/anaconda/install for more details

1.2.2 Install NASA CDF support
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  http://cdf.gsfc.nasa.gov/
-  download and install the latest cdf version for your operating system

1.2.3 Install MagPy and SpacePy (required for CDF support)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  open a Terminal
-  ... known issues: eventually change to the anaconda2/bin directory
   before running python (if not set as default)
-  ... check by starting python in the terminal
-  run './pip install spacepy'
-  ... known issues: installation of spacepy eventually requires a
   fortran compiler
-  ... e.g. Linux: install gcc
-  ... e.g. MacOs: install gcc and gfortran
-  run './pip install geomagpy'
-  ... known issues: e.g. Linux: MySQL-python problem -> install
   libmysqlclient-dev on linux (e.g. debian/ubuntu: sudo apt-get install
   libmysqlclient-dev)

1.2.4 Post-installation information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

-  please note that anaconda provides a full python environment with
   many packages not used by MagPy
-  for a "slim" installation follow the "from scratch" instructions
   below (for experienced users)
-  for upgrades: run './pip install geomagpy version==new-version'.
   Installation provides both shell based magpy and the graphical user
   interface xmagpy

-  running magpy: \* type "python" in a terminal -> opens a python shell
   ready for MagPy \* type "xmagpy" in a terminal -> open the graphical
   user interface of MagPy \* !! MacOS: !! type "xmagpyw" in a terminal
   -> open the graphical user interface of MagPy (since v0.3.95)

-  adding a shortcut for xmagpy: coming soon

1.3 MacOs installation - MacPorts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1.3.1 Install `MacPorts <https://www.macports.org/>`__
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1.3.2 coming soon
^^^^^^^^^^^^^^^^^

1.4 Platform independent installations - Docker
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1.4.1 Install `Docker <https://www.docker.com/>`__ (toolbox) on your operating system
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

     - https://docs.docker.com/engine/installation/

1.4.2 Get the MagPy Image
^^^^^^^^^^^^^^^^^^^^^^^^^

::

     - open a docker shell

            >>> docker pull geomagpy/magpy:latest
            >>> docker run -d --name magpy -p 8000:8000 geomagpy/magpy:latest

1.4.3 Open a browser
^^^^^^^^^^^^^^^^^^^^

::

     - open address http://localhost:8000 (or http://"IP of your VM":8000)
     - NEW: first time access might require a token or passwd

            >>> docker logs magpy

          will show the token 
     - run python shell (not conda) 
     - in python shell


            >>> %matplotlib inline
            >>> from magpy.stream import read
            >>> ...

1.5 Install from source (experts only)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Requirements: - Python 2.7,3.x (*xmagpy* will only work with python 2.7)

Recommended: - Python packages: \* NasaCDF \* SpacePy \* pexpect (for
SSH support)

-  Other useful Software:

   -  MySQL (database features)
   -  NetCDF4 (support is currently in preparation)
   -  Webserver (e.g. Apache2, PHP)

1.5.1 Linux
^^^^^^^^^^^

A) Get python packages and other extensions (for other distros than
   debian/ubuntu install similar packages):

   ::

       sudo apt-get install python-numpy python-scipy python-matplotlib python-nose python-wxgtk2.8 python-wxtools python-dev build-essential python-networkx python-h5py python-f2py gfortran ncurses-dev libhdf5-serial-dev hdf5-tools libnetcdf-dev python-netcdf python-serial python-twisted owfs python-ow python-setuptools git-core mysql-server python-mysqldb libmysqlclient-dev
       sudo pip install ffnet
       sudo pip install pexpect
       sudo pip install pyproj

B) Get CDF and Omni database support:

   a) CDF (NASA): http://cdf.gsfc.nasa.gov/html/sw\_and\_docs.html
      (tested with 3.6.1.0, please check validity of commands below to
      make command for any future versions)

      tar -zxvf cdf36\_1-dist-all.tar.gz cd cdf36\* make OS=linux
      ENV=gnu CURSES=yes FORTRAN=no UCOPTIONS=-O2 SHARED=yes all sudo
      make INSTALLDIR=/usr/local/cdf install

   b) SpacePy (Los Alamos):
      https://sourceforge.net/projects/spacepy/files/spacepy/ (tested
      with 0.1.6)

      sudo pip install spacepy

C) Install MagPy

   a) Using pip

      sudo pip install GeomagPy

      -  specific version: sudo pip install GeomagPy==v0.3.9

   b) Using github (latest development versions)

      git clone git://github.com/GeomagPy/MagPy.git cd MagPy\* sudo
      python setup.py install

1.5.2 Windows
^^^^^^^^^^^^^

| Tested on XP, Win7, Win10 a) Get a current version of Python(x,y) and
  install it optionally select packages ffnet and netcdf during install
  - for cdf support b) Download nasaCDF packages and install (see links
  above) c) get python-spacepy package d) download and unpack
  GeomagPy-x.x.x.tar.gz e) open a command window f) go to the unpacked
  directory e.g. cd
  c::raw-latex:`\user`:raw-latex:`\Downloads`:raw-latex:`\GeomagPy`
| g) execute "setup.py install"

2. A quick guide to MagPy
-------------------------

written by R. Leonhardt, R. Bailey (April 2017)

2.1 Getting started
~~~~~~~~~~~~~~~~~~~

Start python. Import all stream methods and classes using:

::

    from magpy.stream import *

Please note that this import will shadow any already existing ``read``
method.

2.2 Reading and writing data
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

MagPy supports the following data formats and thus conversions between
them: - WDC: World Data Centre format - JSON: JavaScript Object Notation
- IMF: Intermagnet Format - IAF: Intermagnet Archive Format - NEIC: WGET
data from USGS - NEIC - IAGA: IAGA 2002 text format - IMAGCDF:
Intermagnet CDF Format - GFZKP: GeoForschungsZentrum KP-Index format -
GSM19/GSM90: Output formats from GSM magnetometers - POS1: POS-1 binary
output - BLV: Baseline format Intermagnet - IYFV: Yearly mean format
Intermagnet

... and many others. To get a full list, use:

::

        from magpy.stream import *
        print(PYMAG_SUPPORTED_FORMATS)

You will find several example files provided with MagPy. The ``cdf``
file is stored along with meta information in NASA's common data format
(cdf). Reading this file requires a working installation of Spacepy cdf.

If you do not have any geomagnetic data file you can access example data
by using the following command (after ``import *``):

::

        data = read(example1)
        

The data from ``example1`` has been read into a MagPy *DataStream* (or
*stream*) object. Most data processing routines in MagPy are applied to
data streams.

Several example data sets are provided within the MagPy package:

-  ``example1``: `INTERMAGNET <http://www.intermagnet.org>`__ CDF
   (ImagCDF) file with 1 second xyzf data
-  ``example2``: `INTERMAGNET <http://www.intermagnet.org>`__ Archive
   format (IAF) file for one month with 1 min, 1 hour, K and mean data
-  ``example3``: MagPy readable DI data file with data from 1 single DI
   measurement
-  ``example4``: MagPy Basevalue file (PYSTR) with analysis results of
   several DI data

2.2.1 Reading
^^^^^^^^^^^^^

For a file in the same directory:

::

        data = read(r'myfile.min') 

... or for specific paths in Linux:

::

        data = read(r'/path/to/file/myfile.min') 

... or for specific paths in Windows:

::

        data = read(r'c:\path\to\file\myfile.min')

Pathnames are related to your operating system. In this guide we will
assume a Linux system. Files that are read in are uploaded to the memory
and each data column (or piece of header information) is assigned to an
internal variable (key). To get a quick overview of the assigned keys in
any given stream (``data``) you can use the following method:

::

        print(data._get_key_headers() )

2.2.2 Writing
^^^^^^^^^^^^^

After loading data from a file, we can save the data in the standard
IAGA02 and IMAGCDF formats with the following commands.

To create an IAGA-02 format file, use:

::

        data.write(r'/path/to/diretory/',format_type='IAGA')

To create an `INTERMAGNET <http://www.intermagnet.org>`__ CDF (ImagCDF)
file:

::

        data.write(r'/path/to/diretory/',format_type='IMAGCDF')

The filename will be created automatically according to the defined
format. By default, daily files are created and the date is added to the
filename in-between the optional parameters ``filenamebegins`` and
``filenameends``. If ``filenameends`` is missing, ``.txt`` is used as
default.

2.2.3 Other possibilities for reading files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To read all local files ending with .min within a directory (creates a
single stream of all data):

::

        data = read(r'/path/to/file/*.min')

Getting magnetic data directly from an online source such as the WDC:

::

        data = read(r'ftp://thewellknownaddress/single_year/2011/fur2011.wdc')

Getting *kp* data from the GFZ Potsdam:

::

        data = read(r'http://www-app3.gfz-potsdam.de/kp_index/qlyymm.tab')

(Please note: data access and usage is subjected to the terms and
conditions of the individual data provider. Please make sure to read
them before accessing any of these products.)

No format specifications are required for reading. If MagPy can handle
the format, it will be automatically recognized.

Getting data for a specific time window for local files:

::

        data = read(r'/path/to/files/*.min',starttime="2014-01-01", endtime="2014-05-01")

... and remote files:

::

        data = read(r'ftp://address/fur2013.wdc',starttime="2013-01-01", endtime="2013-02-01")

Reading data from the INTERMAGNET Webservice (starting soon):

::

        data = read('http://www.intermagnet.org/test/ws/?id=WIC')

2.2.4 Selecting timerange
^^^^^^^^^^^^^^^^^^^^^^^^^

The stream can be trimmed to a specific time interval after reading by
applying the trim method, e.g. for a specific month:

::

        data = data.trim(starttime="2013-01-01", endtime="2013-02-01")

.. raw:: html

   <!--#### 2.2.5 Tutorial

   For the ongoing quick example please use the following steps. This will create daily IAGA02 files within the directory. Please make sure that the directory is empty before writing data to it.

   A) Load example data

   Within the MagPy package, several example data sets are provided:

      example1: [INTERMAGNET] CDF (ImagCDF) file with 1 second data
      example2: [INTERMAGNET] Archive format (IAF) file with 1 min, 1 hour, K and mean data
      example3: MagPy readable DI data file with data from 1 single DI measurement
      example4: MagPy Basevalue file (PYSTR) with analysis results of several DI data

           # Replace example1 with a full path, if you have your own data 
           data = read(example1)

   B) Store it locally in your favorite directory

           data.write('/tmp/',filenamebegins='MyExample_', format_type='IAGA')

   Please note that storing data in a different formt might require additional meta information. Checkout section (i) on how to deal with these aspects.-->

2.3 Getting help on options and usage
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2.3.1 Python's help function
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Information on individual methods and options can be obtained as
follows:

For basic functions:

::

        help(read)

For specific methods related to e.g. a stream object "data":

::

        help(data.fit)

Note that this requires the existence of a "data" object, which is
obtained e.g. by data = read(...). The help text can also be shown by
directly calling the *DataStream* object method using:

::

        help(DataStream.fit)

.. raw:: html

   <!--#### 2.3.2 Tutorial

           help(data.fit)-->

2.3.2 MagPy's logging system
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

MagPy automatically logs many function options and runtime information,
which can be useful for debugging purposes. This log is saved by default
in the temporary file directory of your operating system, e.g. for Linux
this would be ``/tmp/magpy.log``. The log is formatted as follows with
the date, module and function in use and the message leve
(INFO/WARNING/ERROR):

::

        2017-04-22 09:50:11,308 INFO - magpy.stream - Initiating MagPy...

Messages on the WARNING and ERROR level will automatically be printed to
shell. Messages for more detailed debugging are written at the DEBUG
level and will not be printed to the log unless an additional handler
for printing DEBUG is added.

Custom loggers can be defined by creating a logger object after
importing MagPy and adding handlers (with formatting):

::

        from magpy.stream import *
        import logging
        
        logger = logging.getLogger()
        hdlr = logging.FileHandler('testlog.log')
        formatter = logging.Formatter('%(asctime)s - %(name)s - %(levelname)s - %(message)s')
        hdlr.setFormatter(formatter)
        logger.addHandler(hdlr)
        

The logger can also be configured to print to shell (stdout, without
formatting):

::

        import sys
        logger = logging.getLogger()
        stdoutlog = logging.StreamHandler(sys.stdout)
        logger.addHandler(stdoutlog)

2.4 Plotting
~~~~~~~~~~~~

You will find some example plots at the `Conrad
Observatory <http://www.conrad-observatory.at>`__.

2.4.1 Quick (and not dirty)
^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

        import magpy.mpplot as mp
        mp.plot(data)

2.4.2 Some options
^^^^^^^^^^^^^^^^^^

Select specific keys to plot:

::

        mp.plot(data,variables=['x','y','z'])
        

Defining a plot title and specific colors (see ``help(mp.plot)`` for
list and all options):

::

        mp.plot(data,variables=['x','y'],plottitle="Test plot",
                colorlist=['g', 'c'])

2.4.3 Data from multiple streams
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Various datasets from multiple data streams will be plotted above one
another. Provide a list of streams and an array of keys:

::

        mp.plotStreams([data1,data2],[['x','y','z'],['f']])

.. raw:: html

   <!--#### 2.4.4 Tutorial

   Read a second stream

           otherdata = read(WDC)

   Plot xyz data from both streams

           mp.plotStreams([data,otherdata]) -->

2.5 Flagging data
~~~~~~~~~~~~~~~~~

The flagging procedure allows the observer to mark specific data points
or ranges. Falgs are useful for labelling data spikes, storm onsets,
pulsations, disturbances, lightning strikes, etc. Each flag is asociated
with a comment and a type number. The flagtype number ranges between 0
and 4:

-  0: normal data with comment (e.g. "Hello World")
-  1: data marked by automated analysis (e.g. spike)
-  2: data marked by observer as valid geomagnetic signature (e.g. storm
   onset, pulsation). Such data cannot be marked invalid by automated
   procedures
-  3: data marked by observer as invalid (e.g. lightning, magnetic
   disturbance)
-  4: merged data (e.g. data inserted from another source/instrument as
   defined in the comment)

Flags can be stored along with the data set (requires CDF format output)
or separately in a binary archive. These flags can then be applied to
the raw data again, ascertaining perfect reproducibility.

2.5.1 Mark data spikes
^^^^^^^^^^^^^^^^^^^^^^

Load a data record with data spikes:

::

        datawithspikes = read(example1)

Mark all spikes using the automated function ``flag_outlier`` with
default options:

::

        flaggeddata = datawithspikes.flag_outlier(timerange=timedelta(minutes=1),threshold=3)

Show flagged data in a plot:

::

        mp.plot(flaggeddata,['f'],annotate=True)

2.5.2 Flag time range
^^^^^^^^^^^^^^^^^^^^^

Flag a certain time range:

::

        flaglist = flaggeddata.flag_range(keys=['f'], starttime='2012-08-02T04:33:40', 
                                          endtime='2012-08-02T04:44:10', 
                                          flagnum=3, text="iron metal near sensor")

Apply these flags to the data:

::

        flaggeddata = flaggeddata.flag(flaglist)

Show flagged data in a plot:

::

        mp.plot(flaggeddata,['f'],annotate=True)

2.5.3 Save flagged data
^^^^^^^^^^^^^^^^^^^^^^^

To save the data together with the list of flags to a CDF file:

::

        flaggeddata.write('/tmp/',filenamebegins='MyFlaggedExample_', format_type='PYCDF')

To check for correct save procedure, read and plot the new file:

::

        newdata = read("/tmp/MyFlaggedExample_*")
        mp.plot(newdata,annotate=True, plottitle='Reloaded flagged CDF data')

2.5.4 Save flags separately
^^^^^^^^^^^^^^^^^^^^^^^^^^^

To save the list of flags seperately from the data in a pickled binary
file:

::

        fullflaglist = flaggeddata.extractflags()
        saveflags(fullflaglist,"/tmp/MyFlagList.pkl"))

These flags can be loaded in and then reapplied to the data set:

::

        data = read(example1)
        flaglist = loadflags("/tmp/MyFlagList.pkl")
        data = data.flag(flaglist)
        mp.plot(data,annotate=True, plottitle='Raw data with flags from file')

2.5.5 Drop flagged data
^^^^^^^^^^^^^^^^^^^^^^^

For some analyses it is necessary to use "clean" data, which can be
produced by dropping data flagged as invalid (e.g. spikes). By default,
the following method removes all data marked with flagtype numbers 1 and
3.

::

        cleandata = flaggeddata.remove_flagged()
        mp.plot(cleandata, ['f'], plottitle='Flagged data dropped')

2.6 Basic methods
~~~~~~~~~~~~~~~~~

2.6.1 Filtering
^^^^^^^^^^^^^^^

MagPy's ``filter`` uses the settings recommended by
`IAGA <http://www.iaga-aiga.org/>`__/`INTERMAGNET <http://www.intermagnet.org>`__.
Ckeck ``help(data.filter)`` for further options and definitions of
filter types and pass bands.

First, get the sampling rate before filtering in seconds:

::

        print("Sampling rate before [sec]:", cleandata.samplingrate())

Filter the data set with default parameters (``filter`` automatically
chooses the correct settings depending on the provided sanmpling rate):

::

        filtereddata = cleandata.filter()

Get sampling rate and filtered data after filtering (please note that
all filter information is added to the data's meta information
dictionary (data.header):

::

        print("Sampling rate after [sec]:", filtereddata.samplingrate())
        print("Filter and pass band:", filtereddata.header.get('DataSamplingFilter',''))

2.6.2 Coordinate transformation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Assuming vector data in columns [x,y,z] you can freely convert between
xyz, hdz, and idf coordinates:

::

        cleandata = cleandata.xyz2hdz()

2.6.3 Calculate delta F
^^^^^^^^^^^^^^^^^^^^^^^

If the data file contains xyz (hdz, idf) data and an independently
measured f value, you can calculate delta F between the two instruments
using the following:

::

        cleandata = cleandata.delta_f()
        mp.plot(cleandata,plottitle='delta F')

2.6.4 Calculate Means
^^^^^^^^^^^^^^^^^^^^^

Mean values for certain data columns can be obtained using the ``mean``
method. The mean will only be calculated for data with the percentage of
valid data (in contrast to missing data) points not falling below the
value given by the percentage option (default 95). If too much data is
missing, then no mean is calulated and the function returns NaN.

::

        print(cleandata.mean('df', percentage=80))
        

The median can be calculated by defining the ``meanfunction`` option:

::

        print(cleandata.mean('df', meanfunction='median'))

2.6.5 Applying offsets
^^^^^^^^^^^^^^^^^^^^^^

Constant offsets can be added to individual columns using the ``offset``
method with a dictionary defining the MagPy stream column keys and the
offset to be applied (datetime.timedelta object for time column, float
for all others):

::

        offsetdata = cleandata.offset({'time':timedelta(seconds=0.19),'f':1.24})

2.6.6 Scaling data
^^^^^^^^^^^^^^^^^^

Individual columns can also be multiplied by values provided in a
dictionary:

::

        multdata = cleandata.multiply({'x':-1})

2.6.7 Fit functions
^^^^^^^^^^^^^^^^^^^

MagPy offers the possibility to fit functions to data using either
polynomial functions or cubic splines (default):

::

        func = cleandata.fit(keys=['x','y','z'],knotstep=0.1)
        mp.plot(cleandata,variables=['x','y','z'],function=func)

2.6.8 Derivatives
^^^^^^^^^^^^^^^^^

Time derivatives, which are useful to identify outliers and sharp
changes, are calculated as follows:

::

        diffdata = cleandata.differentiate(keys=['x','y','z'],put2keys = ['dx','dy','dz'])
        mp.plot(diffdata,variables=['dx','dy','dz'])

2.6.9 All methods at a glance
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For a summary of all supported methods, see the section **List of all
MagPy methods** below.

2.7 Geomagnetic analysis
~~~~~~~~~~~~~~~~~~~~~~~~

2.7.1 Determination of K indices
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

MagPy supports the FMI method for determination of K indices. Please
consult the MagPy publication for details on this method and
application.

A month of one minute data is provided in ``example2``, which
corresponds to an `INTERMAGNET <http://www.intermagnet.org>`__ IAF
archive file. Reading a file in this format will load one minute data by
default. Accessing hourly data and other information is described below.

::

        data2 = read(example2)
        kvals = data2.k_fmi()

The determination of K values will take some time as the filtering
window is dynamically adjusted. In order to plot the original data (H
component) and K values together, we now use the multiple stream
plotting method ``plotStreams``. Here you need to provide a list of
streams and an array containing variables for each stream. The
additional options determine the appearance of the plot (limits, bar
chart):

::

        mp.plotStreams([data2,kvals],[['x'],['var1']],
                       specialdict = [{},{'var1':[0,9]}],
                       symbollist=['-','z'],
                       bartrange=0.06)
        

``'z'`` in ``symbollist`` refers to the second subplot (K), which should
be plotted as bars rather than the standard line (``'-'``).

2.7.2 Automated geomagnetic storm detection
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Geomagnetic storm detection is supported by MagPy using two procedures
based on wavelets and the Akaike Information Criterion (AIC) as outlined
in detail in Bailey and Leonhardt (2016). A basic example of usage to
find an SSC using a Discrete Wavelet Transform (DWT) is shown below:

::

        from magpy.stream import read
        from magpy.opt.stormdet import seekStorm
        stormdata = read("LEMI025_2015-03-17.cdf")      # 1s variometer data
        stormdata = stormdata.xyz2hdz()
        stormdata = stormdata.smooth('x', window_len=25)
        detection, ssc_list = seekStorm(stormdata, method="MODWT")
        print("Possible SSCs detected:", ssc_list)
        

The method ``seekStorm`` will return two variables: ``detection`` is
True if any detection was made, while ``ssc_list`` is a list of
dictionaries containing data on each detection. Note that this method
alone can return a long list of possible SSCs (most incorrectly
detected), particularly during active storm times. It is most useful
when additional restrictions based on satellite solar wind data apply
(currently only optimised for ACE data, e.g. from the NOAA website):

::

        satdata_ace_1m = read('20150317_ace_swepam_1m.txt')
        satdata_ace_5m = read('20150317_ace_epam_5m.txt')
        detection, ssc_list, sat_cme_list = seekStorm(stormdata,
                    satdata_1m=satdata_ace_1m, satdata_5m=satdata_ace_5m,
                    method='MODWT', returnsat=True)
        print("Possible CMEs detected:", sat_cme_list)
        print("Possible SSCs detected:", ssc_list)

2.7.3 Sq analysis
^^^^^^^^^^^^^^^^^

Methods are currently in preparation.

2.7.4 Validity check of data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A common and important application used in the geomagnetism community is
a general validity check of geomagnetic data to be submitted to the
official data repositories `IAGA <http://www.iaga-aiga.org/>`__, WDC, or
`INTERMAGNET <http://www.intermagnet.org>`__. Please note: this is
currently under development and will be extended in the near future. A
'one-click' test method will be included in xmagpy in the future,
checking:

A) Validity of data formats, e.g.:

   ::

       data = read('myiaffile.bin', debug=True) 

B) Completeness of meta-information

C) Conformity of applied techniques to respective rules

D) Internal consistency of data

E) Optional: regional consistency

2.7.5 Spectral Analysis and Noise
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For analysis of the spectral content of data, MagPy provides two basic
plotting methods. ``plotPS`` will calculate and display a power spectrum
of the selected component. ``plotSpectrogram`` will plot a spectrogram
of the time series. As usual, there are many options for plot window and
processing parameters that can be accessed using the help method.

::

        data = read(example1)
        mp.plotPS(data,key='f')
        mp.plotSpectrogram(data,['f'])

2.8 Handling multiple streams
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2.8.1 Merging streams
^^^^^^^^^^^^^^^^^^^^^

Merging data comprises combining two streams into one new stream. This
includes adding a new column from another stream, filling gaps with data
from another stream or replacing data from one column with data from
another stream. The following example sketches the typical usage:

::

        print("Data columns in data2:", data2._get_key_headers())
        newstream = mergeStreams(data2,kvals,keys=['var1'])
        print("Data columns after merging:", data2._get_key_headers())
        mp.plot(newstream, ['x','y','z','var1'],symbollist=['-','-','-','z'])

If column ``var1`` does not existing in data2 (as above), then this
column is added. If column ``var1`` had already existed, then missing
data would be inserted from stream ``kvals``. In order to replace any
existing data, use option ``mode='replace'``.

2.8.2 Differences between streams
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Sometimes it is necessary to examine the differences between two data
streams e.g. differences between the F values of two instruments running
in parallel at an observatory. The method ``subtractStreams`` is
provided for this analysis:

::

        diff = subtractStreams(data1,data2,keys=['f'])

2.9 The art of meta-information
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Each data set is accompanied by a dictionary containing meta-information
for this data. This dictionary is completely dynamic and can be filled
freely, but there are a number of predefined fields that help the user
provide essential meta-information as requested by
`IAGA <http://www.iaga-aiga.org/>`__,
`INTERMAGNET <http://www.intermagnet.org>`__ and other data providers.
All meta information is saved only to MagPy-specific archive formats
PYCDF and PYSTR. All other export formats save only specific information
as required by the projected format.

The current content of this dictionary can be accessed by:

::

        data = read(example1)
        print(data.header)

Information is added/changed by using:

::

        data.header['SensorName'] = 'FGE'

Individual information is obtained from the dictionary using standard
key input:

::

        print(data.header.get('SensorName'))

If you want to have a more readable list of the header information, do:

::

        for key in data.header:
            print ("Key: {} \t Content: {}".format(key,data.header.get(key)))

2.9.1 Conversion to ImagCDF - Adding meta-information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To convert data from `IAGA <http://www.iaga-aiga.org/>`__ or IAF formats
to the new `INTERMAGNET <http://www.intermagnet.org>`__ CDF format, you
will usually need to add additional meta-information required for the
new format. MagPy can assist you here, firstly by extracting and
correctly adding already existing meta-information into newly defined
fields, and secondly by informing you of which information needs to be
added for producing the correct output format.

Example of IAGA02 to ImagCDF:

::

        mydata = read('IAGA02-file.min')
        mydata.write('/tmp',format_type='IMAGCDF')

The console output of the write command (see below) will tell you which
information needs to be added (and how) in order to obtain correct
ImagCDF files. Please note, MagPy will store the data in any case and
will be able to read it again even if information is missing. Before
submitting to a GIN, you need to make sure that the appropriate
information is contained. Attributes that relate to publication of the
data will not be checked at this point, and might be included later.

::

        >>>Writing IMAGCDF Format /tmp/wic_20150828_0000_PT1M_4.cdf
        >>>writeIMAGCDF: StandardLevel not defined - please specify by yourdata.header['DataStandardLevel'] = ['None','Partial','Full']
        >>>writeIMAGCDF: Found F column
        >>>writeIMAGCDF: given components are XYZF. Checking F column...
        >>>writeIMAGCDF: analyzed F column - values are apparently independend from vector components - using column name 'S'

Now add the missing information. Selecting 'Partial' will require
additional information. You will get a 'reminder' if you forget this.
Please check IMAGCDF instructions on specific codes:

::

        mydata.header['DataStandardLevel'] = 'Partial'
        mydata.header['DataPartialStandDesc'] = 'IMOS-01,IMOS-02,IMOS-03,IMOS-04,IMOS-05,IMOS-06,IMOS-11,IMOS-12,IMOS-13,IMOS-14,IMOS-15,IMOS-21,IMOS-22,IMOS-31,IMOS-41'

Similar reminders to fill out complete header information will be shown
for other conversions like:

::

        mydata.write('/tmp',format_type='IAGA')
        mydata.write('/tmp',format_type='IMF')
        mydata.write('/tmp',format_type='IAF',coverage='month')
        mydata.write('/tmp',format_type='WDC')

2.9.2 Providing location data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Providing location data usually requires information on the reference
system (ellipsoid,...). By default MagPy assumes that these values are
provided in WGS84/WGS84 reference system. In order to facilitate most
easy referencing and conversions, MagPy supports
`EPSG <https://www.epsg-registry.org/>`__ codes for coordinates. If you
provide the geodetic references as follows, and provided that the
`proj4 <https://github.com/OSGeo/proj.4>`__ Python package is available,
MagPy will automatically convert location data to the requested output
format (currently WGS84).

::

        mydata.header['DataAcquisitionLongitude'] = -34949.9
        mydata.header['DataAcquisitionLatitude'] = 310087.0
        mydata.header['DataLocationReference'] = 'GK M34, EPSG: 31253'

        >>>...
        >>>writeIMAGCDF: converting coordinates to epsg 4326
        >>>...

2.9.3 Special meta-information fields
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The meta-information fields can hold much more information than required
by most output formats. This includes basevalue and baseline parameters,
flagging details, detailed sensor information, serial numbers and much
more. MagPy makes use of these possibilities. In order to save this
meta-information along with your data set you can use MagPy internal
archiving format, ``PYCDF``, which can later be converted to any of the
aforementioned output formats. You can even reconstruct a full data
base. Any upcoming meta-information or output request can be easily
added/modified without disrupting already existing data sets and the
ability to read and analyse old data. This data format is also based on
Nasa CDF. ASCII outputs are also supported by MagPy, of which the
``PYSTR`` format also contains all meta information and ``PYASCII`` is
the most compact. Please consider that ASCII formats require a lot of
memory, especially for one second and higher resolution data.

::

        mydata.write('/tmp',format_type='PYCDF',coverage='year')

2.10 Data transfer
~~~~~~~~~~~~~~~~~~

MagPy contains a number of methods to simplify data transfer for
observatory applications. Methods within the basic Python functionality
can also be very useful. Using the implemented methods requires:

::

        from magpy import transfer as mt

2.10.1 Downloads
^^^^^^^^^^^^^^^^

Use the ``read`` method as outlined above. No additional imports are
required.

2.10.2 FTP upload
^^^^^^^^^^^^^^^^^

Files can also be uploaded to an FTP server:

::

        mt.ftpdatatransfer(localfile='/path/to/data.cdf',ftppath='/remote/directory/',myproxy='ftpaddress or address of proxy',port=21,login='user',passwd='passwd',logfile='/path/mylog.log')
        

The upload methods using FTP, SCP and GIN support logging. If the data
file failed to upload correctly, the path is added to a log file and,
when called again, upload of the file is retried. This option is useful
for remote locations with unstable network connections.

2.10.3 Secure communication protocol (SCP)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To transfer via SCP:

::

        mt.scptransfer('user@address:/remote/directory/','/path/to/data.cdf',passwd,timeout=60)

2.10.4 Upload data to GIN
^^^^^^^^^^^^^^^^^^^^^^^^^

Use the following command:

::

        mt.ginupload('/path/to/data.cdf', ginuser, ginpasswd, ginaddress, faillog=True, stdout=True)

2.10.5 Avoiding real-text passwords in scripts
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In order to avoid using real-text password in scripts, MagPy comes along
with a simple encryption routine.

::

        from magpy.opt import cred as mpcred

Credentials will be saved to a hidden file with encrypted passwords. To
add information for data transfer to a machine called 'MyRemoteFTP' with
an IP of 192.168.0.99:

::

        mpcred.cc('transfer', 'MyRemoteFTP', user='user', passwd='secure', address='192.168.0.99', port=21)

Extracting passwd information within your data transfer scripts:

::

        user = mpcred.lc('MyRemoteFTP', 'user')
        password = mpcred.lc('MyRemoteFTP','passwd')

2.11 DI measurements, basevalues and baselines
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

These procedures require an additional import:

::

        from magpy import absolutes as di

2.11.1 Data structure of DI measurements
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please check ``example3``, which is an example DI file. You can create
these DI files by using the input sheet from xmagpy or the online input
sheet provided by the Conrad Observatory. If you want to use this
service, please contact the Observatory staff. Also supported are
DI-files from the AUTODIF.

2.11.2 Reading DI data
^^^^^^^^^^^^^^^^^^^^^^

Reading and analyzing DI data requires valid DI file(s). For correct
analysis, variometer data and scalar field information needs to be
provided as well. Checkout ``help(di.absoluteAnalysis)`` for all
options. The analytical procedures are outlined in detail in the MagPy
article (citation). A typical analysis looks like:

::

        diresult = di.absoluteAnalysis('/path/to/DI/','path/to/vario/','path/to/scalar/')

Path to DI can either point to a single file, a directory or even use
wildcards to select data from a specific observatory/pillar. Using the
examples provided along with MagPy, the analysis line looks like

::

        diresult = di.absoluteAnalysis(example3,example2,example2)

Calling this method will provide terminal output as follows and a stream
object ``diresult`` which can be used for further analyses.

::

        >>>...
        >>>Analyzing manual measurement from 2015-03-25
        >>>Vector at: 2015-03-25 08:18:00+00:00
        >>>Declination: 3:53:46, Inclination: 64:17:17, H: 21027.2, Z: 43667.9, F: 48466.7
        >>>Collimation and Offset:
        >>>Declination:    S0: -3.081, delta H: -6.492, epsilon Z: -61.730
        >>>Inclination:    S0: -1.531, epsilon Z: -60.307
        >>>Scalevalue: 1.009 deg/unit
        >>>Fext with delta F of 0.0 nT
        >>>Delta D: 0.0, delta I: 0.0

Fext indicates that F values have been used from a separate file and not
provided along with DI data. Delta values for F, D, and I have not been
provided either. ``diresult`` is a stream object containing average D, I
and F values, the collimation angles, scale factors and the base values
for the selected variometer, beside some additional meta information
provided in the data input form.

2.11.3 Reading BLV files
^^^^^^^^^^^^^^^^^^^^^^^^

Basevalues:

::

        blvdata = read('/path/myfile.blv')
        mp.plot(blvdata, symbollist=['o','o','o'])

Adopted baseline:

::

        bldata = read('/path/myfile.blv',mode='adopted')
        mp.plot(bldata)

2.11.4 Basevalues and baselines
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Basevalues as obtained in (2.11.2) or (2.11.3) are stored in a normal
data stream object, therefore all analysis methods outlined above can be
applied to this data. The ``diresult`` object contains D, I, and F
values for each measurement in columns x,y,z. Basevalues for H, D and Z
related to the selected variometer are stored in columns dx,dy,dz. In
``example4``, you will find some more DI analysis results. To plot these
basevalues we can use the following plot command, where we specify the
columns, filled circles as plotsymbols and also define a minimum spread
of each y-axis of +/- 5 nT for H and Z, +/- 0.05 deg for D.

::

        basevalues = read(example4)
        mp.plot(basevalues, variables=['dx','dy','dz'], symbollist=['o','o','o'], padding=[5,0.05,5])

Fitting a baseline can be easily accomplished with the ``fit`` method.
First we test a linear fit to the data by fitting a polynomial function
with degree 1.

::

        func = basevalues.fit(['dx','dy','dz'],fitfunc='poly', fitdegree=1)
        mp.plot(basevalues, variables=['dx','dy','dz'], symbollist=['o','o','o'], padding=[5,0.05,5], function=func)

We then fit a spline function using 3 knotsteps over the timerange (the
knotstep option is always related to the given timerange).

::

        func = basevalues.fit(['dx','dy','dz'],fitfunc='spline', knotstep=0.33)
        mp.plot(basevalues, variables=['dx','dy','dz'], symbollist=['o','o','o'], padding=[5,0.05,5], function=func)

Hint: a good estimate on the necessary fit complexity can be obtained by
looking at delta F values. If delta F is mostly constant, then the
baseline should also not be very complex.

2.11.5 Applying baselines
^^^^^^^^^^^^^^^^^^^^^^^^^

The baseline method provides a number of options to assist the observer
in determining baseline corrections and realted issues. The basic
building block of the baseline method is the fit function as discussed
above. Lets first load raw vectorial geomagnetic data, the absevalues of
which are contained in above example:

::

        rawdata = read(example5)

Now we can apply the basevalue information and the spline function as
tested above:

::

        func = rawdata.baseline(basevalues, extradays=0, fitfunc='spline',
                                knotstep=0.33,startabs='2015-09-01',endabs='2016-01-22')

The ``baseline`` method will determine and return a fit function between
the two given timeranges based on the provided basevalue data
``blvdata``. The option ``extradays`` allows for adding days before and
after start/endtime for which the baseline function will be
extrapolated. This option is useful for providing quasi-definitive data.
When applying this method, a number of new meta-information attributes
will be added, containing basevalues and all functional parameters to
describe the baseline. Thus, the stream object still contains
uncorrected raw data, but all baseline correction information is now
contained within its meta data. To apply baseline correction you can use
the ``bc`` method:

::

        corrdata = rawdata.bc()

If baseline jumps/breaks are necessary due to missing data, you can call
the baseline function for each independent segment and combine the
resulting baseline functions to a list:

::

        stream = read(mydata,starttime='2016-01-01',endtime='2016-03-01')
        basevalues = read(mybasevalues)
        adoptedbasefunc = []
        adoptedbasefunc.append(stream.baseline(basevalues, extradays=0, fitfunc='poly', fitdegree=1,startabs='2016-01-01',endabs='2016-02-01')
        adoptedbasefunc.append(stream.baseline(basevalues, extradays=0, fitfunc='spline', knotstep=0.33,startabs='2016-01-02',endabs='2016-01-03')

        corr = stream.bc()

The combined baseline can be plotted accordingly. Extend the function
parameters with each additional segment.

::

        mp.plot(basevalues, variables=['dx','dy','dz'], symbollist=['o','o','o'], padding=[5,0.05,5], function=adoptedbasefunc)

Adding a baseline for scalar data, which is determined from the delta F
values provided within the basevalue data stream:

::

        scalarbasefunc = []
        scalarbasefunc.append(basevalues.baseline(basevalues, keys=['df'], extradays=0, fitfunc='poly', fitdegree=1,startabs='2016-01-01',endabs='2016-03-01'))
        plotfunc = adoptedbasefunc
        plotfunc.extend(scalarbasefunc)
        mp.plot(basevalues, variables=['dx','dy','dz','df'], symbollist=['o','o','o','o'], padding=[5,0.05,5,5], function=plotfunc)

Getting dailymeans and correction for scalar baseline can be acomplished
by:

::

        meanstream = stream.dailymeans()
        meanstream = meanstream.func2stream(scalarbasefunc,mode='sub',keys=['f'],fkeys=['df'])
        meanstream = meanstream.delta_f()

Please note that here the function originally determined from the deltaF
(df) values of the basevalue data needs to be applied to the F column
(f) from the data stream. Before saving we will also extract the
baseline parameters from the meta information, which is automatically
generated by the ``baseline`` method.

::

        absinfo = stream.header.get('DataAbsInfo','')
        fabsinfo = basevalues.header.get('DataAbsInfo','')

2.11.6 Saving basevalue and baseline information
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following will create a BLV file:

::

        basevalues.write('/my/path', coverage='all', format_type='BLV', diff=meanstream, year='2016', absinfo=absinfo, deltaF=fabsinfo)

Information on the adopted baselines will be extracted from option
``absinfo``. If several functions are provided, baseline jumps will be
automatically inserted into the BLV data file. The output of adopted
scalar baselines is configured by option ``deltaF``. If a number is
provided, this value is assumed to represent the adopted scalar
baseline. If either 'mean' or 'median' are given (e.g.
``deltaF='mean'``), then the mean/median value of all delta F values in
the ``basevalues`` stream is used, requiring that such data is
contained. Providing functional parameters as stored in a
``DataAbsInfo`` meta information field, as shown above, will calculate
and use the scalar baseline function. The ``meanstream`` stream contains
daily averages of delta F values between variometer and F measurements
and the baseline adoption data in the meta-information. You can,
however, provide all this information manually as well. The typical way
to obtain such a ``meanstream`` is sketched above.

2.12 Database support
~~~~~~~~~~~~~~~~~~~~~

MagPy supports database access and many methods for optimizing data
treatment in connection with databases. Among many other benefits, using
a database simplifies many typical procedures related to
meta-information. Currently, MagPy supports
`MySQL <https://www.mysql.com/>`__ databases. To use these features, you
need to have MySQL installed on your system. In the following we provide
a brief outline of how to set up and use this optional addition. Please
note that a proper usage of the database requires sensor-specific
information. In geomagnetism, it is common to combine data from
different sensors into one file structure. In this case, such data needs
to remain separate for database usage and is only combined when
producing
`IAGA <http://www.iaga-aiga.org/>`__/`INTERMAGNET <http://www.intermagnet.org>`__
definitive data. Furthermore, unique sensor information such as type and
serial number is required.

::

        import magpy import database as mdb

2.12.1 Setting up a MagPy database (using MySQL)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Open mysql (e.g. Linux: ``mysql -u root -p mysql``) and create a new
database. Replace ``#DB-NAME`` with your database name (e.g. ``MyDB``).
After creation, you will need to grant priviledges to this database to a
user of your choice. Please refer to official MySQL documentations for
details and further commands.

::

         mysql> CREATE DATABASE #DB-NAME; 
         mysql> GRANT ALL PRIVILEGES ON #DB-NAME.* TO '#USERNAME'@'%' IDENTIFIED BY '#PASSWORD';

2.12.2 Initializing a MagPy database
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Connecting to a database using MagPy is done using following command:

::

        db = mdb.mysql.connect(host="localhost",user="#USERNAME",passwd="#PASSWORD",db="#DB-NAME")
        mdb.dbinit(db)

2.12.3 Adding data to the database
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Examples of useful meta-information:

::

        iagacode = 'WIC'
        data = read(example1)
        gsm = data.selectkeys(['f'])
        fge = data.selectkeys(['x','y','z'])
        gsm.header['SensorID'] = 'GSM90_12345_0002'
        gsm.header['StationID'] = iagacode
        fge.header['SensorID'] = 'FGE_22222_0001'
        fge.header['StationID'] = iagacode
        mdb.writeDB(db,gsm)
        mdb.writeDB(db,fge)

All available meta-information will be added automatically to the
relevant database tables. The SensorID scheme consists of three parts:
instrument (GSM90), serial number (12345), and a revision number (0002)
which might change in dependency of maintenance, calibration, etc. As
you can see in the example above, we separate data from different
instruments, which we recommend particularly for high resolution data,
as frequency and noise characteristics of sensor types will differ.

2.12.4 Reading data
^^^^^^^^^^^^^^^^^^^

To read data from an established database:

::

        data = mdb.readDB(db,'GSM90_12345_0002') 

Options e.g. starttime='' and endtime='' are similar as for normal
``read``.

2.12.5 Meta data
^^^^^^^^^^^^^^^^

An often used application of database connectivity with MagPy will be to
apply meta-information stored in the database to data files before
submission. The following command demostrates how to extract all missing
meta-information from the database for the selected sensor and add it to
the header dictionary of the data object.

::

        rawdata = read('/path/to/rawdata.bin')
        rawdata.header = mdb.dbfields2dict(db,'FGE_22222_0001')
        rawdata.write(..., format_type='IMAGCDF')

2.13 Monitoring scheduled scripts
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Automated analysis can e easily accomplished by adding a series of MagPy
commands into a script. A typical script could be:

::

        # read some data and get means
        data = read(example1)
        mean_f = data.mean('f')

        # import monitor method
        from magpy.opt import Analysismonitor
        analysisdict = Analysismonitor(logfile='/var/log/anamon.log')
        analysisdict = analysisdict.load()
        # check some arbitray threshold
        analysisdict.check({'data_threshold_f_GSM90': [mean_f,'>',20000]})

If provided criteria are invalid, then the logfile is changed
accordingly. This method can assist you particularly in checking data
actuality, data contents, data validity, upload success, etc. In
combination with an independent monitoring tool like
`Nagios <https://www.nagios.org/>`__, you can easily create mail/SMS
notfications of such changes, in addition to monitoring processes, live
times, disks etc. `MARCOS <https://github.com/geomagpy/MARCOS>`__ comes
along with some instructions on how to use Nagios/MagPy for data
acquisition monitoring.

2.14 Data acquisition support
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

MagPy contains a couple of packages which can be used for data
acquisition, collection and organization. These methods are primarily
contained in two applications:
`MARTAS <https://github.com/geomagpy/MARTAS>`__ and
`MARCOS <https://github.com/geomagpy/MARCOS>`__. MARTAS (Magpy Automated
Realtime Acquisition System) supports communication with many common
instruments (e.g. GSM, LEMI, POS1, FGE, and many non-magnetic
instruments) and transfers serial port signals to
`WAMP <http://wamp-proto.org/>`__ (Web Application Messaging Protocol),
which allows for real-time data access using e.g. WebSocket
communication through the internet. MARCOS (Magpy's Automated Realtime
Collection and Organistaion System) can access such real-time streams
and also data from many other sources and supports the observer by
storing, analyzing, archiving data, as well as monitoring all processes.
Details on these two applications can be found elsewhere.

2.15 Graphical user interface
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Many of the above mentioned methods are also available within the
graphical user interface of MagPy. To use this check the installation
instructions for your operating system. You will find Video Tutorials
online (to be added) describing its usage for specific analyses.

2.16 Current developments
~~~~~~~~~~~~~~~~~~~~~~~~~

2.16.1 Exchange data objects with `ObsPy <https://github.com/obspy/obspy>`__
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

MagPy supports the exchange of data with ObsPy, the seismological
toolbox. Data objects of both python packages are very similar. Note:
ObsPy assumes regular spaced time intervals. Please be careful if this
is not the case with your data. The example below shows a simple import
routine, on how to read a seed file and plot a spectrogram (which you
can identically obtain from ObsPy as well). Conversions to MagPy allow
for vectorial analyses, and geomagnetic applications. Conversions to
ObsPy are useful for effective high frequency analysis, requiring evenly
spaced time intervals, and for exporting to seismological data formats.

::

        from obspy import read as obsread
        seeddata = obsread('/path/to/seedfile')
        magpydata = obspy2magpy(seeddata,keydict={'ObsPyColName': 'x'})
        mp.plotSpectrogram(magpydata,['x'])

2.16.2 Flagging in ImagCDF
^^^^^^^^^^^^^^^^^^^^^^^^^^

::

        datawithspikes = read(example1)
        flaggeddata = datawithspikes.flag_outlier(keys=['f'],timerange=timedelta(minutes=1),threshold=3)
        mp.plot(flaggeddata,['f'],annotate=True)
        flaggeddata.write(tmpdir,format_type='IMAGCDF',addflags=True)

The ``addflags`` option denotes that flagging information will be added
to the ImagCDF format. Please note that this is still under development
and thus content and format specifications may change. So please use it
only for test purposes and not for archiving. To read and view flagged
ImagCDF data, just use the normal read command, and activate annotation
for plotting.

::

        new = read('/tmp/cnb_20120802_000000_PT1S_1.cdf')
        mp.plot(new,['f'],annotate=True)

2.17 List of all MagPy methods
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Please use the help method (section 2.3) for descriptions and return
values.

+--------+---------+------------+
| group  | method  | parameter  |
+========+=========+============+
| -      | **findp | name, path |
|        | ath**   |            |
+--------+---------+------------+
| -      | \*\*\_p | method     |
|        | ickle\_ |            |
|        | method\ |            |
|        | *\*     |            |
+--------+---------+------------+
| -      | \*\*\_u | func\_name |
|        | npickle | ,          |
|        | \_metho | obj, cls   |
|        | d\*\*   |            |
+--------+---------+------------+
| stream | ****ini | self,      |
|        | t****   | container= |
|        |         | None,      |
|        |         | header={}, |
|        |         | ndarray=No |
|        |         | ne         |
+--------+---------+------------+
| stream | **ext** | self,      |
|        |         | columnstru |
|        |         | cture      |
+--------+---------+------------+
| stream | **add** | self,      |
|        |         | datlst     |
+--------+---------+------------+
| stream | **lengt | self       |
|        | h**     |            |
+--------+---------+------------+
| stream | **repla | self,      |
|        | ce**    | datlst     |
+--------+---------+------------+
| stream | **copy* | self       |
|        | *       |            |
+--------+---------+------------+
| stream | ****str | self       |
|        | ****    |            |
+--------+---------+------------+
| stream | ****rep | self       |
|        | r****   |            |
+--------+---------+------------+
| stream | ****get | self,      |
|        | item*** | index      |
|        | *       |            |
+--------+---------+------------+
| stream | ****len | self       |
|        | ****    |            |
+--------+---------+------------+
| stream | **clear | self       |
|        | \_heade |            |
|        | r**     |            |
+--------+---------+------------+
| stream | **exten | self,datls |
|        | d**     | t,header,n |
|        |         | darray     |
+--------+---------+------------+
| stream | **union | self,colum |
|        | **      | n          |
+--------+---------+------------+
| stream | **remov | self       |
|        | eduplic |            |
|        | ates**  |            |
+--------+---------+------------+
| stream | **start | self,      |
|        | **      | dateformt= |
|        |         | None       |
+--------+---------+------------+
| stream | **end** | self,      |
|        |         | dateformt= |
|        |         | None       |
+--------+---------+------------+
| stream | **findt | self,time, |
|        | ime**   | \*\*kwargs |
+--------+---------+------------+
| stream | \*\*\_f | self       |
|        | ind\_t\ |            |
|        | _limits |            |
|        | \*\*    |            |
+--------+---------+------------+
| stream | \*\*\_p | self       |
|        | rint\_k |            |
|        | ey\_hea |            |
|        | ders\*\ |            |
|        | *       |            |
+--------+---------+------------+
| stream | \*\*\_g | self,\*\*k |
|        | et\_key | wargs      |
|        | \_heade |            |
|        | rs\*\*  |            |
+--------+---------+------------+
| stream | \*\*\_g | self       |
|        | et\_key |            |
|        | \_names |            |
|        | \*\*    |            |
+--------+---------+------------+
| stream | **drope | self       |
|        | mpty**  |            |
+--------+---------+------------+
| stream | **fille | self,      |
|        | mpty**  | ndarray,   |
|        |         | keylist    |
+--------+---------+------------+
| stream | **sorti | self       |
|        | ng**    |            |
+--------+---------+------------+
| stream | \*\*\_g | self, key, |
|        | et\_lin | value      |
|        | e\*\*   |            |
+--------+---------+------------+
| stream | \*\*\_t | self, keys |
|        | ake\_co |            |
|        | lumns\* |            |
|        | \*      |            |
+--------+---------+------------+
| stream | \*\*\_r | self, key, |
|        | emove\_ | value      |
|        | lines\* |            |
|        | \*      |            |
+--------+---------+------------+
| stream | \*\*\_g | self, key  |
|        | et\_col |            |
|        | umn\*\* |            |
+--------+---------+------------+
| stream | \*\*\_p | self,      |
|        | ut\_col | column,    |
|        | umn\*\* | key,       |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | \*\*\_m | self, key, |
|        | ove\_co | put2key    |
|        | lumn\*\ |            |
|        | *       |            |
+--------+---------+------------+
| stream | \*\*\_d | self,key   |
|        | rop\_co |            |
|        | lumn\*\ |            |
|        | *       |            |
+--------+---------+------------+
| stream | \*\*\_c | self, key  |
|        | lear\_c |            |
|        | olumn\* |            |
|        | \*      |            |
+--------+---------+------------+
| stream | \*\*\_r | self,      |
|        | educe\_ | pointlimit |
|        | stream\ | =100000    |
|        | *\*     |            |
+--------+---------+------------+
| stream | \*\*\_r | self       |
|        | emove\_ |            |
|        | nancolu |            |
|        | mns\*\* |            |
+--------+---------+------------+
| stream | \*\*\_a | self,      |
|        | ic\*\*  | signal, k, |
|        |         | debugmode= |
|        |         | None       |
+--------+---------+------------+
| stream | **harmf | self,nt,   |
|        | it**    | val,       |
|        |         | fitdegree  |
+--------+---------+------------+
| stream | \*\*\_g | self, key, |
|        | et\_max | returntime |
|        | \*\*    | =False     |
+--------+---------+------------+
| stream | \*\*\_g | self, key, |
|        | et\_min | returntime |
|        | \*\*    | =False     |
+--------+---------+------------+
| stream | **ampli | self,key   |
|        | tude**  |            |
+--------+---------+------------+
| stream | \*\*\_g | self, t,   |
|        | f\*\*   | tau        |
+--------+---------+------------+
| stream | \*\*\_h | self, p, x |
|        | f\*\*   |            |
+--------+---------+------------+
| stream | \*\*\_r | self,      |
|        | esidual | func, y    |
|        | \_func\ |            |
|        | *\*     |            |
+--------+---------+------------+
| stream | \*\*\_t | self,      |
|        | au\*\*  | period,    |
|        |         | fac=0.8325 |
|        |         | 5461       |
+--------+---------+------------+
| stream | \*\*\_c | self,      |
|        | onverts | coordinate |
|        | tream\* | ,          |
|        | \*      | \*\*kwargs |
+--------+---------+------------+
| stream | \*\*\_d | self,index |
|        | elete\* |            |
|        | \*      |            |
+--------+---------+------------+
| stream | \*\*\_a | self,strea |
|        | ppend\* | m          |
|        | \*      |            |
+--------+---------+------------+
| stream | \*\*\_d | self,      |
|        | et\_tra | period     |
|        | nge\*\* |            |
+--------+---------+------------+
| stream | \*\*\_i | self, s    |
|        | s\_numb |            |
|        | er\*\*  |            |
+--------+---------+------------+
| stream | \*\*\_n | self,      |
|        | ormaliz | column     |
|        | e\*\*   |            |
+--------+---------+------------+
| stream | \*\*\_t | self, time |
|        | esttime |            |
|        | \*\*    |            |
+--------+---------+------------+
| stream | \*\*\_d | self, key  |
|        | rop\_na |            |
|        | ns\*\*  |            |
+--------+---------+------------+
| stream | \*\*\_s | self, keys |
|        | elect\_ |            |
|        | keys\*\ |            |
|        | *       |            |
+--------+---------+------------+
| stream | \*\*\_s | self,      |
|        | elect\_ | starttime= |
|        | timeran | None,      |
|        | ge\*\*  | endtime=No |
|        |         | ne,        |
|        |         | maxidx=-1  |
+--------+---------+------------+
| stream | **aic\_ | self, key, |
|        | calc**  | \*\*kwargs |
+--------+---------+------------+
| stream | **basel | self,      |
|        | ine**   | absoluteda |
|        |         | ta,        |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **strea | self,      |
|        | m2dict* | keys=['dx' |
|        | *       | ,'dy','dz' |
|        |         | ],         |
|        |         | dictkey='D |
|        |         | ataBaseVal |
|        |         | ues'       |
+--------+---------+------------+
| stream | **dict2 | self,dictk |
|        | stream* | ey='DataBa |
|        | *       | seValues'  |
+--------+---------+------------+
| stream | **basel | self,      |
|        | ineAdva | absdata,   |
|        | nced**  | baselist,  |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **bc**  | self,      |
|        |         | function=N |
|        |         | one,       |
|        |         | ctype=None |
|        |         | ,          |
|        |         | alpha=0.0, |
|        |         | level='pre |
|        |         | liminary'  |
+--------+---------+------------+
| stream | **binde | self,key,f |
|        | tector* | lagnum=1,k |
|        | *       | eystoflag= |
|        |         | ['x'],sens |
|        |         | orid=None, |
|        |         | text=None, |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **calc\ | self,      |
|        | _f**    | \*\*kwargs |
+--------+---------+------------+
| stream | **daily | self,      |
|        | means** | keys=['x', |
|        |         | 'y','z','f |
|        |         | '],        |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **date\ | self,      |
|        | _offset | offset     |
|        | **      |            |
+--------+---------+------------+
| stream | **delta | self,      |
|        | \_f**   | \*\*kwargs |
+--------+---------+------------+
| stream | **f\_fr | self,      |
|        | om\_df* | \*\*kwargs |
|        | *       |            |
+--------+---------+------------+
| stream | **diffe | self,      |
|        | rentiat | \*\*kwargs |
|        | e**     |            |
+--------+---------+------------+
| stream | **DWT\_ | self,key=' |
|        | calc**  | x',wavelet |
|        |         | ='db4',lev |
|        |         | el=3,plot= |
|        |         | False,outf |
|        |         | ile=None,  |
+--------+---------+------------+
| stream | **event | self, key, |
|        | logger* | values,    |
|        | *       | compare=No |
|        |         | ne,        |
|        |         | stringvalu |
|        |         | es=None,   |
|        |         | addcomment |
|        |         | =None,     |
|        |         | debugmode= |
|        |         | None       |
+--------+---------+------------+
| stream | **extra | self, key, |
|        | ct**    | value,     |
|        |         | compare=No |
|        |         | ne,        |
|        |         | debugmode= |
|        |         | None       |
+--------+---------+------------+
| stream | **extra | self,      |
|        | ct2**   | keys,      |
|        |         | get='>',   |
|        |         | func=None, |
|        |         | debugmode= |
|        |         | None       |
+--------+---------+------------+
| stream | **extra | self,      |
|        | polate* | start, end |
|        | *       |            |
+--------+---------+------------+
| stream | **filte | self,\*\*k |
|        | r**     | wargs      |
+--------+---------+------------+
| stream | **fit** | self,      |
|        |         | keys,      |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **extra | self       |
|        | ctflags |            |
|        | **      |            |
+--------+---------+------------+
| stream | **flagf | self,index |
|        | ast**   | array,flag |
|        |         | ,          |
|        |         | comment,ke |
|        |         | ys=None    |
+--------+---------+------------+
| stream | **flag\ | self,      |
|        | _range* | \*\*kwargs |
|        | *       |            |
+--------+---------+------------+
| stream | **flag\ | self,      |
|        | _outlie | \*\*kwargs |
|        | r**     |            |
+--------+---------+------------+
| stream | **flag* | self,      |
|        | *       | flaglist,  |
|        |         | removedupl |
|        |         | icates=Fal |
|        |         | se,        |
|        |         | debug=Fals |
|        |         | e          |
+--------+---------+------------+
| stream | **flagl | self,flagl |
|        | iststat | ist        |
|        | s**     |            |
+--------+---------+------------+
| stream | **flagl | self,flagl |
|        | istclea | ist        |
|        | n**     |            |
+--------+---------+------------+
| stream | **strea | self,      |
|        | m2flagl | userange=T |
|        | ist**   | rue,       |
|        |         | flagnumber |
|        |         | =None,     |
|        |         | keystoflag |
|        |         | =None,     |
|        |         | sensorid=N |
|        |         | one,       |
|        |         | comment=No |
|        |         | ne         |
+--------+---------+------------+
| stream | **flagl | self,      |
|        | istmod* | mode='sele |
|        | *       | ct',       |
|        |         | flaglist=[ |
|        |         | ],         |
|        |         | parameter= |
|        |         | 'key',     |
|        |         | value=None |
|        |         | ,          |
|        |         | newvalue=N |
|        |         | one        |
+--------+---------+------------+
| stream | **flagl | self,      |
|        | istadd* | flaglist,  |
|        | *       | sensorid,  |
|        |         | keys,      |
|        |         | flagnumber |
|        |         | ,          |
|        |         | comment,   |
|        |         | startdate, |
|        |         | enddate=No |
|        |         | ne         |
+--------+---------+------------+
| stream | **flag\ | self, key, |
|        | _stream | flag,      |
|        | **      | comment,   |
|        |         | startdate, |
|        |         | enddate=No |
|        |         | ne,        |
|        |         | samplingra |
|        |         | te=0.,     |
|        |         | debug=Fals |
|        |         | e          |
+--------+---------+------------+
| stream | **simpl | self,basev |
|        | ebaseva | alue,\*\*k |
|        | lue2str | wargs      |
|        | eam**   |            |
+--------+---------+------------+
| stream | **func2 | self,funct |
|        | stream* | ion,\*\*kw |
|        | *       | args       |
+--------+---------+------------+
| stream | **func\ | self,funct |
|        | _add**  | ion,\*\*kw |
|        |         | args       |
+--------+---------+------------+
| stream | **func\ | self,funct |
|        | _subtra | ion,\*\*kw |
|        | ct**    | args       |
+--------+---------+------------+
| stream | **get\_ | self,      |
|        | gaps**  | \*\*kwargs |
+--------+---------+------------+
| stream | **get\_ | self,      |
|        | rotatio | xcompensat |
|        | nangle* | ion=0,keys |
|        | *       | =['x','y', |
|        |         | 'z'],\*\*k |
|        |         | wargs      |
+--------+---------+------------+
| stream | **get\_ | self       |
|        | samplin |            |
|        | g\_peri |            |
|        | od**    |            |
+--------+---------+------------+
| stream | **sampl | self,      |
|        | ingrate | \*\*kwargs |
|        | **      |            |
+--------+---------+------------+
| stream | **integ | self,      |
|        | rate**  | \*\*kwargs |
+--------+---------+------------+
| stream | **inter | self,      |
|        | pol**   | keys,      |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **k\_ex | self,      |
|        | tend**  | \*\*kwargs |
+--------+---------+------------+
| stream | **k\_fm | self,      |
|        | i**     | \*\*kwargs |
+--------+---------+------------+
| stream | **lines | self       |
|        | truct2n |            |
|        | darray* |            |
|        | *       |            |
+--------+---------+------------+
| stream | **mean* | self, key, |
|        | *       | \*\*kwargs |
+--------+---------+------------+
| stream | **missi | self,v,win |
|        | ngvalue | dow\_len,t |
|        | **      | hreshold=0 |
|        |         | .9,fill='m |
|        |         | ean'       |
+--------+---------+------------+
| stream | **MODWT | self,key=' |
|        | \_calc* | x',wavelet |
|        | *       | ='haar',le |
|        |         | vel=1,plot |
|        |         | =False,out |
|        |         | file=None  |
+--------+---------+------------+
| stream | **multi | self,      |
|        | ply**   | factors,   |
|        |         | square=Fal |
|        |         | se         |
+--------+---------+------------+
| stream | **offse | self,      |
|        | t**     | offsets,   |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **plot* | self,      |
|        | *       | keys=None, |
|        |         | debugmode= |
|        |         | None,      |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **power | self, key, |
|        | spectru | debugmode= |
|        | m**     | None,      |
|        |         | outfile=No |
|        |         | ne,        |
|        |         | fmt=None,  |
|        |         | axes=None, |
|        |         | title=None |
|        |         | ,\*\*kwarg |
|        |         | s          |
+--------+---------+------------+
| stream | **rando | self,perce |
|        | mdrop** | ntage=None |
|        |         | ,fixed\_in |
|        |         | dicies=Non |
|        |         | e          |
+--------+---------+------------+
| stream | **remov | self,      |
|        | e**     | starttime= |
|        |         | None,      |
|        |         | endtime=No |
|        |         | ne         |
+--------+---------+------------+
| stream | **remov | self,      |
|        | e\_flag | \*\*kwargs |
|        | ged**   |            |
+--------+---------+------------+
| stream | **remov | self,      |
|        | e\_outl | \*\*kwargs |
|        | ier**   |            |
+--------+---------+------------+
| stream | **resam | self,      |
|        | ple**   | keys,      |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **rotat | self,\*\*k |
|        | ion**   | wargs      |
+--------+---------+------------+
| stream | **scale | self,      |
|        | \_corre | keys,      |
|        | ction** | scales,    |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **selec | self,      |
|        | tkeys** | keys,      |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **smoot | self,      |
|        | h**     | keys=None, |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **spect | self,      |
|        | rogram* | keys,      |
|        | *       | per\_lap=0 |
|        |         | .9,        |
|        |         | wlen=None, |
|        |         | log=False, |
+--------+---------+------------+
| stream | **stead | self, key, |
|        | yrise** | timewindow |
|        |         | ,          |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **stere | self,      |
|        | oplot** | \*\*kwargs |
+--------+---------+------------+
| stream | **trim* | self,      |
|        | *       | starttime= |
|        |         | None,      |
|        |         | endtime=No |
|        |         | ne,        |
|        |         | newway=Fal |
|        |         | se         |
+--------+---------+------------+
| stream | **vario | self,      |
|        | meterco | variopath, |
|        | rrectio | thedate,   |
|        | n**     | \*\*kwargs |
+--------+---------+------------+
| stream | \*\*\_w | self,      |
|        | rite\_f | format\_ty |
|        | ormat\* | pe,        |
|        | \*      | filenamebe |
|        |         | gins,      |
|        |         | filenameen |
|        |         | ds,        |
|        |         | coverage,  |
|        |         | dateformat |
|        |         | ,year      |
+--------+---------+------------+
| stream | **write | self,      |
|        | **      | filepath,  |
|        |         | compressio |
|        |         | n=5,       |
|        |         | \*\*kwargs |
+--------+---------+------------+
| stream | **idf2x | self,\*\*k |
|        | yz**    | wargs      |
+--------+---------+------------+
| stream | **xyz2i | self,\*\*k |
|        | df**    | wargs      |
+--------+---------+------------+
| stream | **xyz2h | self,\*\*k |
|        | dz**    | wargs      |
+--------+---------+------------+
| stream | **hdz2x | self,\*\*k |
|        | yz**    | wargs      |
+--------+---------+------------+
| -      | **coord | u,v,w,kind |
|        | inatetr |            |
|        | ansform |            |
|        | **      |            |
+--------+---------+------------+
| -      | **isNum | s          |
|        | ber**   |            |
+--------+---------+------------+
| -      | **find\ | array,valu |
|        | _neares | e          |
|        | t**     |            |
+--------+---------+------------+
| -      | **ceil\ | dt,seconds |
|        | _dt**   |            |
+--------+---------+------------+
| -      | **read* | path\_or\_ |
|        | *       | url=None,  |
|        |         | dataformat |
|        |         | =None,     |
|        |         | headonly=F |
|        |         | alse,      |
|        |         | \*\*kwargs |
+--------+---------+------------+
| -      | \*\*\_r | filename,  |
|        | ead\*\* | dataformat |
|        |         | =None,     |
|        |         | headonly=F |
|        |         | alse,      |
|        |         | \*\*kwargs |
+--------+---------+------------+
| -      | **savef | mylist=Non |
|        | lags**  | e,path=Non |
|        |         | e          |
+--------+---------+------------+
| -      | **loadf | path=None, |
|        | lags**  | sensorid=N |
|        |         | one,begin= |
|        |         | None,      |
|        |         | end=None   |
+--------+---------+------------+
| -      | **joinS | stream\_a, |
|        | treams* | stream\_b, |
|        | *       | \*\*kwargs |
+--------+---------+------------+
| -      | **appen | streamlist |
|        | dStream |            |
|        | s**     |            |
+--------+---------+------------+
| -      | **merge | stream\_a, |
|        | Streams | stream\_b, |
|        | **      | \*\*kwargs |
+--------+---------+------------+
| -      | **dms2d | dms        |
|        | **      |            |
+--------+---------+------------+
| -      | **find\ | stream1,   |
|        | _offset | stream2,   |
|        | **      | guess\_low |
|        |         | =-60.,     |
|        |         | guess\_hig |
|        |         | h=60.      |
+--------+---------+------------+
| -      | **diffS | stream\_a, |
|        | treams* | stream\_b, |
|        | *       | \*\*kwargs |
+--------+---------+------------+
| -      | **subtr | stream\_a, |
|        | actStre | stream\_b, |
|        | ams**   | \*\*kwargs |
+--------+---------+------------+
| -      | **stack | streamlist |
|        | Streams | ,          |
|        | **      | \*\*kwargs |
+--------+---------+------------+
| -      | **compa | stream\_a, |
|        | reStrea | stream\_b  |
|        | ms**    |            |
+--------+---------+------------+
| -      | **array | listofarra |
|        | 2stream | ys,        |
|        | **      | keystring, |
|        |         | starttime= |
|        |         | None,sr=No |
|        |         | ne         |
+--------+---------+------------+
| -      | **obspy | opstream,  |
|        | 2magpy* | keydict={} |
|        | *       |            |
+--------+---------+------------+
| -      | **extra | datestring |
|        | ctDateF |            |
|        | romStri |            |
|        | ng**    |            |
+--------+---------+------------+
| -      | **testT | time       |
|        | imeStri |            |
|        | ng**    |            |
+--------+---------+------------+
| -      | **denor | column,    |
|        | malize* | startvalue |
|        | *       | ,          |
|        |         | endvalue   |
+--------+---------+------------+
| -      | **find\ | array,     |
|        | _neares | value      |
|        | t**     |            |
+--------+---------+------------+
| -      | **maskN | column     |
|        | AN**    |            |
+--------+---------+------------+
| -      | **nan\_ | y          |
|        | helper* |            |
|        | *       |            |
+--------+---------+------------+
| -      | **neare | x          |
|        | stPow2* |            |
|        | *       |            |
+--------+---------+------------+
| -      | **test\ | time       |
|        | _time** |            |
+--------+---------+------------+
| -      | **conve | lon,lat,pr |
|        | rtGeoCo | o1,pro2    |
|        | ordinat |            |
|        | e**     |            |
+--------+---------+------------+
| mpplot | **plote | stream     |
|        | asy**   |            |
+--------+---------+------------+
| mpplot | **plot\ | stream,var |
|        | _new**  | iables=[], |
|        |         | specialdic |
|        |         | t={},error |
|        |         | bars=False |
|        |         | ,padding=0 |
|        |         | ,noshow=Fa |
|        |         | lse        |
+--------+---------+------------+
| mpplot | **plot* | stream,var |
|        | *       | iables=[], |
|        |         | specialdic |
|        |         | t={},error |
|        |         | bars=False |
|        |         | ,padding=0 |
|        |         | ,noshow=Fa |
|        |         | lse        |
+--------+---------+------------+
| mpplot | **plotS | streamlist |
|        | treams* | ,variables |
|        | *       | ,padding=N |
|        |         | one,specia |
|        |         | ldict={},e |
|        |         | rrorbars=N |
|        |         | one        |
+--------+---------+------------+
| mpplot | **toggl | event      |
|        | e\_sele |            |
|        | ctor**  |            |
+--------+---------+------------+
| mpplot | **addFl | data,      |
|        | ag**    | flagger,   |
|        |         | indeciesto |
|        |         | beflagged, |
|        |         | variables  |
+--------+---------+------------+
| mpplot | **plotF | data,varia |
|        | lag**   | bles=None, |
|        |         | figure=Fal |
|        |         | se         |
+--------+---------+------------+
| mpplot | **plotE | stream,key |
|        | MD**    | ,verbose=F |
|        |         | alse,plott |
|        |         | itle=None  |
+--------+---------+------------+
| mpplot | **plotN | streamlist |
|        | ormStre | ,          |
|        | ams**   | key,       |
|        |         | normalize= |
|        |         | True,      |
|        |         | normalizet |
|        |         | =False     |
+--------+---------+------------+
| mpplot | **plotP | stream,key |
|        | S**     | ,debugmode |
|        |         | =False,out |
|        |         | file=None, |
|        |         | noshow=Fal |
|        |         | se         |
+--------+---------+------------+
| mpplot | **plotS | mag\_strea |
|        | atMag** | m,sat\_str |
|        |         | eam,keys,o |
|        |         | utfile=Non |
|        |         | e,plottype |
|        |         | ='disconti |
|        |         | nuous'     |
+--------+---------+------------+
| mpplot | **plotS | stream,    |
|        | pectrog | keys,      |
|        | ram**   | NFFT=1024, |
|        |         | detrend=ml |
|        |         | ab.detrend |
|        |         | \_none     |
+--------+---------+------------+
| mpplot | **magpy | x,         |
|        | Specgra | NFFT=256,  |
|        | m**     | Fs=2,      |
|        |         | Fc=0,      |
|        |         | detrend=ml |
|        |         | ab.detrend |
|        |         | \_none     |
+--------+---------+------------+
| mpplot | **plotS | stream,foc |
|        | tereopl | us='all',c |
|        | ot**    | olorlist   |
|        |         | =          |
|        |         | ['b','r',' |
|        |         | g','c','m' |
|        |         | ,'y','k']  |
+--------+---------+------------+
| mpplot | \*\*\_p | data,saved |
|        | lot\*\* | pi=80,grid |
|        |         | =True,grid |
|        |         | color=grid |
|        |         | color,nosh |
|        |         | ow=False   |
+--------+---------+------------+
| mpplot | \*\*\_c | ax, tmax,  |
|        | onfinex | tmin,      |
|        | \*\*    | timeunit   |
+--------+---------+------------+
| mpplot | \*\*\_e | stream,    |
|        | xtract\ | key        |
|        | _data\_ |            |
|        | for\_PS |            |
|        | D\*\*   |            |
+--------+---------+------------+
| databa | **dbget | db,pierid, |
| se     | Pier**  | rp, value, |
|        |         | maxdate=No |
|        |         | ne,        |
|        |         | l=False,   |
|        |         | dic='Delta |
|        |         | Dictionary |
|        |         | '          |
+--------+---------+------------+
| databa | **dbget | db,        |
| se     | lines** | tablename, |
|        |         | lines      |
+--------+---------+------------+
| databa | **dbupd | db,tablena |
| se     | ate**   | me,        |
|        |         | keys,      |
|        |         | values,    |
|        |         | condition= |
|        |         | None       |
+--------+---------+------------+
| databa | **dbget | db,tablena |
| se     | float** | me,sensori |
|        |         | d,columnid |
|        |         | ,revision= |
|        |         | None       |
+--------+---------+------------+
| databa | **dbget | db,tablena |
| se     | string* | me,sensori |
|        | *       | d,columnid |
|        |         | ,revision= |
|        |         | None       |
+--------+---------+------------+
| databa | **dbupl | db,        |
| se     | oad**   | path,stati |
|        |         | onid,\*\*k |
|        |         | wargs      |
+--------+---------+------------+
| databa | **dbini | db         |
| se     | t**     |            |
+--------+---------+------------+
| databa | **dbdel | db,datainf |
| se     | ete**   | oid,\*\*kw |
|        |         | args       |
+--------+---------+------------+
| databa | **dbdic | db,header\ |
| se     | t2field | _dict,\*\* |
|        | s**     | kwargs     |
+--------+---------+------------+
| databa | **dbfie | db,datainf |
| se     | lds2dic | oid        |
|        | t**     |            |
+--------+---------+------------+
| databa | **dbalt | db         |
| se     | er**    |            |
+--------+---------+------------+
| databa | **dbsel | db,        |
| se     | ect**   | element,   |
|        |         | table,     |
|        |         | condition= |
|        |         | None,      |
|        |         | expert=Non |
|        |         | e,         |
|        |         | debug=Fals |
|        |         | e          |
+--------+---------+------------+
| databa | **dbcoo | db, pier,  |
| se     | rdinate | epsgcode=' |
|        | s**     | epsg:4326' |
+--------+---------+------------+
| databa | **dbsen | db,sensori |
| se     | sorinfo | d,sensorke |
|        | **      | ydict=None |
|        |         | ,sensorrev |
|        |         | ision      |
|        |         | = '0001'   |
+--------+---------+------------+
| databa | **dbdat | db,sensori |
| se     | ainfo** | d,datakeyd |
|        |         | ict=None,t |
|        |         | ablenum=No |
|        |         | ne,default |
|        |         | station='W |
|        |         | IC',update |
|        |         | db=True    |
+--------+---------+------------+
| databa | **write | db,        |
| se     | DB**    | datastream |
|        |         | ,          |
|        |         | tablename= |
|        |         | None,      |
|        |         | StationID= |
|        |         | None,      |
|        |         | mode='repl |
|        |         | ace',      |
|        |         | revision=N |
|        |         | one,       |
|        |         | debug=Fals |
|        |         | e,         |
|        |         | \*\*kwargs |
+--------+---------+------------+
| databa | **dbset | db,        |
| se     | Timesin | tablename, |
|        | DataInf | colstr,uni |
|        | o**     | tstr       |
+--------+---------+------------+
| databa | **dbupd | db,        |
| se     | ateData | tablename, |
|        | Info**  | header     |
+--------+---------+------------+
| databa | **strea | db,        |
| se     | m2db**  | datastream |
|        |         | ,          |
|        |         | noheader=N |
|        |         | one,       |
|        |         | mode=None, |
|        |         | tablename= |
|        |         | None,      |
|        |         | \*\*kwargs |
+--------+---------+------------+
| databa | **readD | db, table, |
| se     | B**     | starttime= |
|        |         | None,      |
|        |         | endtime=No |
|        |         | ne,        |
|        |         | sql=None   |
+--------+---------+------------+
| databa | **db2st | db,        |
| se     | ream**  | sensorid=N |
|        |         | one,       |
|        |         | begin=None |
|        |         | ,          |
|        |         | end=None,  |
|        |         | tableext=N |
|        |         | one,       |
|        |         | sql=None   |
+--------+---------+------------+
| databa | **dilin | db,        |
| se     | e2db**  | dilinestru |
|        |         | ct,        |
|        |         | mode=None, |
|        |         | \*\*kwargs |
+--------+---------+------------+
| databa | **db2di | db,\*\*kwa |
| se     | line**  | rgs        |
+--------+---------+------------+
| databa | **apply | db, stream |
| se     | Deltas* |            |
|        | *       |            |
+--------+---------+------------+
| databa | **getBa | db,sensori |
| se     | seline* | d,         |
|        | *       | date=None  |
+--------+---------+------------+
| databa | **flagl | db,flaglis |
| se     | ist2db* | t,mode=Non |
|        | *       | e,sensorid |
|        |         | =None,modi |
|        |         | ficationda |
|        |         | te=None    |
+--------+---------+------------+
| databa | **db2fl | db,sensori |
| se     | aglist* | d,         |
|        | *       | begin=None |
|        |         | ,          |
|        |         | end=None,  |
|        |         | comment=No |
|        |         | ne,        |
|        |         | flagnumber |
|        |         | =-1,       |
|        |         | key=None,  |
|        |         | removedupl |
|        |         | icates=Fal |
|        |         | se         |
+--------+---------+------------+
| databa | **strin | string     |
| se     | g2dict* |            |
|        | *       |            |
+--------+---------+------------+
| tranfe | \*\*\_c | logfile    |
| r      | hecklog |            |
|        | file\*\ |            |
|        | *       |            |
+--------+---------+------------+
| tranfe | **ftpda | \*\*kwargs |
| r      | tatrans |            |
|        | fer**   |            |
+--------+---------+------------+
| tranfe | \*\*\_m | myproxy,   |
| r      | issingv | port,      |
|        | als\*\* | login,     |
|        |         | passwd,    |
|        |         | logfile    |
+--------+---------+------------+
| tranfe | **scptr | src,dest,p |
| r      | ansfer* | asswd,\*\* |
|        | *       | kwargs     |
+--------+---------+------------+
| tranfe | **ssh\_ | remotepath |
| r      | remotef | ,          |
|        | ilelist | filepat,   |
|        | **      | user,      |
|        |         | host,      |
|        |         | passwd     |
+--------+---------+------------+
| tranfe | **ginup | filename=N |
| r      | load**  | one,       |
|        |         | user=None, |
|        |         | password=N |
|        |         | one,       |
|        |         | url=None,\ |
|        |         | *\*kwargs  |
+--------+---------+------------+
| tranfe | **ftpdi | \*\*kwargs |
| r      | rlist** |            |
+--------+---------+------------+
| tranfe | **ftpre | \*\*kwargs |
| r      | move**  |            |
+--------+---------+------------+
| tranfe | **ftpge | ftpaddress |
| r      | t**     | ,ftpname,f |
|        |         | tppasswd,r |
|        |         | emotepath, |
|        |         | localpath, |
|        |         | identifier |
|        |         | ,port=None |
|        |         | ,\*\*kwarg |
|        |         | s          |
+--------+---------+------------+

