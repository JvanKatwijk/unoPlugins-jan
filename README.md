
-----------------------------------------------------------------
	Jan's SDRuno Plugin collection
-----------------------------------------------------------------

Last - and a little this - year I made a few plugins for SDRuno.
Being an enthousiastic user of SDR RSP's since 2014, I had quite
some experience in writing a variety of SDR applications.
Most of my software is developed under Linux, runs under Linux
and is cross compiled for Windows. 

One of my programs is a "shortwave" receiver, a program with about 10
decoders for various formats, such as CW, weatherfax, dr, psk, etc etc.

The plugins are developed as (almost) windows "mirrors"  of these
decoders. It is "almost" since the framework I am using
in my Linux software is Qt and the gcc compiler collection,
and the plugins are developed for a framework in "nana", using the MSVC
"development"  environment.

---------------------------------------------------------------------
IMPORTANT Note on installation and use
----------------------------------------------------------------------

The Plugins are the ones starting with "SDRunoPlugin_", for each a
brief description is given below.

While these plugins run fine on my W10 Box (W10 home edition), there
are sometimes questions from people who notice that the plugin fails
to load. This is especially the case with the plugins for the weatherfax
and the navTex. They share the possibility of saving output to a file.

Now since I am completely ignorant about windows (and hope to stay that
for a very long time), I only can tell that it seems that some dll's
are missing. 

YOU CAN CHECK WHETHER OR NOT DLL'S ARE MISSING BY APPLYING THE DEPENDENCY
CHECKER ON THE PLUGINS ON YOUR SYSTEM. A ZIPPED VERSION OF THE 
DEPENDENCY CHECKER IS IN THIS FOLDER. JUST DOWNLOAD IT TO E.G. "Downloads",
UNZIP IT WHICH WILL GIVE A FOLDER "Dependencies_x64_Release",
GO INTO THE UNPACKED FOLDER AND START "DependenciesGui".

Use the File button on the opened widget and, from the folder where
the community plugins are stored, in my case
"c:\Documents and Settings\xxx\Source\Repos\plugin\", select the plugin
you want to investigate

![1](/dependency-checker.png?raw=true)

The result will be shown, as in the picture. If dll's are missing or cannot
be loaded properly it will clearly be indicated.

The dependency analyser states that the plugins need the following
dll's to be available in C:\Windows\SysWOW64

	Kernel32.dll
	user32.dll
	gdi32.dll
	COMDLG32.dll
	SHELL32.dll
	MSVCP140.dll
	VCRUNTIME140.dll

	ucrtbase.dll

The AAC decoder in the drm plugin further needs
	libfdk-aac-2.dll, which needs
	libgcc_a_dw2-1.dll, which on its turn needs
	libwinpthread-1.dll


How do I fix the api-ms-win-crt-runtime-l1-1-0. dll  or other missing
dll error?

Install the software via Windows Update.
Download Visual C++ Redistributable for Visual Studio 2015 from Microsoft directly.
Install or Repair the Visual C++ Redistributable for Visual Studio 2015 on your computer.


-------------------------------------------------------------------------
Setting samplerates in SDRuno for these plugins
-------------------------------------------------------------------------

The current version of these plugins use the so-called IQout entry.
This entry outputs an incoming signal, decimated to 192000 Samples per second
(note that unfortunately, the I and Q component are interchanged,
a better name would be the QIout entry);

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
will show a fax signaal.
A Wefax576 signal  has a width of about 1800 pixels and a length of 1200
lines, it is shown as a 900 x 600 picture. However, if the picture
is saved, the format of the saved picture is the original 1800 x 1200
size.

![6](/fax-widget.png?raw=true)

The current version, version 2, now saves all settings between invocations/

![6](/ft8-plugin.png?raw=true)

An experimental ft8 decoder. The Windows version contains an error such
that the software may crash. The Linux version from which it is derived
does not, so identifying the error in the plugin is beyond my capabilities.
Use the plugin at your own risk.


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

