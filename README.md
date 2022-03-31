
-----------------------------------------------------------------
	Jan's SDRuno Plugin collection
-----------------------------------------------------------------

Last - and a little this - year I made a few plugins for SDRuno.
Being an enthousiastic user of SDR RSP's since 2014, I had quite
some experience in writing a variety of SDR applications.
Most of my software is developed under Linux, runs under Linux
and is cross compiled for Windows. 

One of my programs is a "shortwave" receiver, a program with about 10
decoders for various formats, such as CW, weatherfax, etc etc.

The plugins are developed as (almost) windows "mirrors"  of these
decoders. It is "almost" since the framework I am using
in my Linux software is Qt, and the plugins are developed for a
framework in "nana".

---------------------------------------------------------------------
Note on installation and use
----------------------------------------------------------------------

The "folder" (while we normally would say "directory" in programming
enviropnments I'm used to, I'll accept some Windows terminology)
contains, the plugins, each named "SDRunoPlugin_XXX", where the XXX is replaced by a recognizable function name. These plugins should be installed in
the "folder" for the community plugins.

Some plugins need some help, i.e. other dll's where they depend on.
These dll's  libfdk-aac-2.dll, libgcc_s_dw2-1.dll and libwinpthread-1.dll
are included in this "folder". They should be placed in a folder such that the Windows loader can find them. I use "C:\Program Files (x86)\SDRplay\SDRuno",
of course "C:\Windows\SysWOW64" also will do.

Note that the plugins depend on quite some more dll's, most of them
are normally installed on a Windows box, but sometimes I got signals
that a plugin would not load, the cause being some dll missing.

For Windows dll's required for loading and running these plugins, see
the end of this "README".

-------------------------------------------------------------------------
Setting samplerates in SDRuno for these plugins
-------------------------------------------------------------------------

The current version of these plugins use the so-called SP1 entry.
This entry outputs an incoming signal, decimated to 192000 Samples per second
(note that unfortunately, the I and Q component are interchanged);

So, while the previous version of these plugins required  the
user to set the input rate in SDRuno to 2 MHz, and the decimation factor to
32 (resulting in a samplerate of app 63 Khz), that is not needed
anymore, the plugins will open the required SP entry and do their own
furter decimation to - usually - 12 or 2 KHz.

An issue is of course that a signal with a width of say 31 Hz (just a PSK 31
signal) is hardly (better: not) detectable on a spectrum with a width of 
2 or more MHz. USE THE ZOOM FACILITY ON THE MAIN SPECTRUM WIDGET TO
MAKE THE SIGNAL YOU WANT TO TUNE TO AND SEE, VISIBLE.
Furthermore, the filter options provided by the SDRuno for this setting
is not optimal, it is far too large. The plugins themself will do
heavy filtering to obtain a reasonable clean signal with the required
bandwidth.

--------------------------------------------------------------------
The plugins
--------------------------------------------------------------------

-------------------------------------------------------------------
Note on drm
-------------------------------------------------------------------

It took a while but it seems xHE-AAC encoded frames in drm can now
be decoded as well
------------------------------------------------------------------

The plugins in the list are:

 * a plugin for DRM (Digital Radio Mondiale, not Digital Rights management).
DRM is transmitted on shortwave (a variant, DRM+ is transmitted in the good
old FM broadcast bands), and is - as the name suggests - a form of
digital radio.
The common DRM signals have a spectrum width of 10 KHz,  and a transmission
can carry ip to 4 streams, although I have never seen a transmission with 
more than 2 streams.
The current version supports AAC and - slightly experimental - xHE-AAC. It is
experimental since testing xHE-AAC decoding is with only two input files.

![1](/drm-widget.png?raw=true)

 * a plugin for CW. The CW decoder is pretty basic, but the current
version has as addition that - within a user specified range - the software
itself will shift to the strongest signal. Shifting goes reasonably fast
and if no signal is detected nothing will happen.
The software will try - within a reasonable range - to detect the transmission
speed. An indicator for the speed can be set.

![2](/cw-widget.png?raw=true)

 * a plugin for PSK. PSK is a difficult signal, it's bandwidth is small
and there is a great variety in "modes" and settings. Here as well, the
software tries within a reasonable range to shift to the strongest signal,
important since a frequency offset of half a dozen Hz will make decoding
difficult or even impossible. The plugin has a variety of selectors
for different settings

![3](/psk-widget.png?raw=true)

 * a plugin for RTTY. Amateur RTTY has a width of 170 Hz, and a baudrate
of 45. Some weather forecasts use a baudrate of 100 and a width of 800 Hz.
Of  course, the plugin contains a number of selectors for setting baudrate
and signal width.

![4](/rtty-widget.png?raw=true)

 * a plugin for NavTex. On 518 KHz coastguards transmit data.
The signal has a baudrate of 100, and a frequency shift of 170 Hz.

![5](/navtex-widget.png?raw=true)

* a plugin for weatherfax. Weatherfaxes are still transmitted on
shortwave (here a.o 3855 KHz, 4610 KHz). The weatherfax plugin
is able to synchronize on an incoming transmission (although there is
a "cheat"  button to skip the synchronization phase) and
will show a fax signaal. The plugin can save the picture - actually
is the original format, while on the display the format is reduced).

![6](/fax-widget.png?raw=true)

---------------------------------------------------------------------
Dependencies
--------------------------------------------------------------------
It turns out that not all required DLL's are automatically installed on your system
Since I compile this stuff with MSVC, the required dll's were installed.
If you do not have MSVC installed follow the rules:
	
    Install the software via Windows Update.
    Download Visual C++ Redistributable for Visual Studio 2015 from Microsoft directly.
    Install or Repair the Visual C++ Redistributable for Visual Studio 2015 on your computer.


Note that the AAC decoder in the drm plugin further needs some more plugins.
there are included in the repository

	libfdk-aac-2.dll, which needs
	libgcc_a_dw2-1.dll, which on its turn needs
	libwinpthread-1.dll




--------------------------------------------------------------------------
Copyright and license
--------------------------------------------------------------------------

	All these plugins are created by me, Copyright will be
	with me. Of course the copyrights of the owners of these rights
	of the additional dll's is gratefully acknowledged.

	The software - either is source or as dll - is made available
	under a GNU GPLV2, meaning that anyone is allowed to look at
	the software and modify or extend the software, under the
	restriction that all these modications and/or additions are
	made available under the same conditions as this software
	is available

