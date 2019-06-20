
RMradar_pi - Raymarine Digital Radar Plugin for OpenCPN
========================================================

Should work with digital radars like RD424D and analog radars connected to E-series classic MFDs. Most of the code is taken from BR24Radar_pi project and so is the text below.

Plugin has only been tested on Linux platform. If you want to give it a try, set your LAN IP to your choice of 10.X.X.X/8, connect RDXXXD radar or E-series MFD. Plugin can run in the passive mode and display radar picture while MFD is controlling the radar.

If there is no MFD on the network, radar control will need to be enabled in the plugin settings. If you do it, you are on your own, this software does not come with guarantees of any kind.

Compiling
---------

You can compile just this plugin without having to compile the entire OpenCPN source. If you check out the plugin source into the plugins subdirectory of your OpenCPN source tree, you can build it as part of it (exactly as with the versions prior to 1.0).

You will need the general preconditions for building OpenCPN from http://opencpn.org/ocpn/developers_manual .

The following command line snippets show how to build the entire package separately from the OpenCPN source.
In order to build multiple platforms you can build in separate `build-${platform}` directories.

###Obtain the source code

```
git clone https://github.com/ab2nkovs/RMRadar_pi.git
```

###Build on Microsoft Windows

-- Tested, does compile.

```
mkdir BR24radar_pi/build-win32
cd BR24radar_pi/build-win32
cmake ..
cmake --build .
```
Windows note: You must place opencpn.lib into your build directory to be able to link the plugin DLL. You can get this file from your local OpenCPN build, or alternatively download from http://sourceforge.net/projects/opencpnplugins/files/opencpn_lib/

###Creating a package on Microsoft Windows

Windows

-- not tested, probably will not work

```
cmake --build . --config release --target package
```

###Build on Linux

Example on 64 bit Intel/AMD64 system:

```
mkdir RMRadar_pi/build-linux-x86_64
cd RMRadar_pi/build-linux-x86_64
cmake ..
make
```


###Creating a package on Linux

```
make package
```

###Build on Mac OS X:

-- not tested, probably will not work

XCode can be downloaded from the App Store.

Tools: Can be installed either manually or from Homebrew (http://brew.sh). Homebrew is _highly_ recommended.
```
brew install cmake
brew install gettext
ln -s /usr/local/Cellar/gettext/0.19.2/bin/msgmerge /usr/local/bin/msgmerge
ln -s /usr/local/Cellar/gettext/0.19.2/bin/msgfmt /usr/local/bin/msgfmt
```

To target older OS X versions than the one you are running, you need the respective SDKs installed. Official releases target 10.7. The easiest way to achieve that is using https://github.com/devernay/xcodelegacy

####Building wxWidgets
(do not use wxmac from Homebrew, it is not compatible with OpenCPN)
Get wxWidgets 3.0.x source from http://wxwidgets.org
Configure, build and install
```
cd wxWidgets-3.0.2
./configure --enable-unicode --with-osx-cocoa --with-macosx-sdk=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.7
make
sudo make install
```

####Building the plugin
Before running cmake, you must set the deployment target to OS X 10.7 to be compatible with the libraries used by core OpenCPN
```
export MACOSX_DEPLOYMENT_TARGET=10.7
mkdir build-mac
cd build-mac
cmake ..
make
```

####Packaging on OS X
Get and install the Packages application from http://s.sudre.free.fr/Software/Packages/about.html
```
make create-pkg
```

License
-------
The plugin code is licensed under the terms of the GPL v2.

Acknowledgements
----------------

This would be a pretty useless plugin if OpenCPN did not exist. Hurrah for @bdbcat!

The plugin was started by @cowelld, who took @bdbcat's Garmin radar plugin and the reverse engineered data from http://www.roboat.at/technologie/radar/ and created the first working version in 2012.

@canboat started helping Dave. Soon he implemented most of the 4G specific functionality, rewrote the control dialogs, implemented the guard zones and cleaned the code considerably.

@nohal contributed the packaging installers, without which this would still be a set of sources instead of deliverable packages for various platforms.

@Hakansv did a lot of testing and contributed the idle timer, and contributed work on the translations.

@douwefokkema implemented the heading on radar functionality, optimised the OpenGL drawing and implemented the refresh rate code.

@seandepagnier shader support and some optimizations
