rtl-sdr
=======

Software to use a Realtek RTL2832 based DVB dongle as an SDR receiver

Original project page: http://sdr.osmocom.org/trac/wiki/rtl-sdr

Mac OS X Build Notes
--------------------

These instructions were tested on OS X 10.11 'El Capitan'

### Dependencies:

* Mac OS Developer Tools (might be able to just install `gcc` directly, not sure)
* Homebrew (to install other dependencies)
* cmake - install with `brew install cmake` (you can also use autotools, per the documentation)
* libusb1.0 - install with `brew install libusb` 

### Building:

* `git clone <desired fork of code>`
* `cd rtl-sdr`
* `mkdir build && cd build`
* `cmake ../ -DCMAKE_MACOSX_RPATH=ON` 
  * if this gives an error related to libusb, make sure it is installed `brew install libusb`
  * If you don't want binaries installed to `/usr/local`, you can set the install location
    with `cmake ../ -DCMAKE_INSTALL_PREFIX=/path/to/wherever`
* `make` 
* `sudo make install` (or `make install` if you are installing to a non-privileged location)

### Testing:

* Plug in the RTL-SDR dongle
  * If desired, check using the System Information tool, most should enumerate as 
    "RTL2832U" or similar
* Run `rtl_test` and verify that it does not produce errors
* To test demodulation, install Sox (to enable commandline audio playback)
  * `brew install sox`
* `rtl_fm -M wbfm -s 200000 -r 48k -f 90.9M | play -traw -r48k -es -b16 -c1 -V1 -`
  * This didn't work particularly well for me; I had to use the `-F 0` or `-F 9` filter
    options, to hear anything but the strongest broadcast FM stations
  * This worked better: 
    `./rtl_fm -M wbfm -s 256k -r 24k -f 90.1M -g 20 -F 0 | play -traw -r24k -es -b16 -c1 -V1 -`
  * Generally you have to play with the bandwidth (`-s` option) based on the signal;
    for FM broadcast, something around 256k seems to work fairly well.
