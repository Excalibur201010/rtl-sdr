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
* `cmake ../` (if this gives an error related to libusb, make sure it is installed `brew install libusb`)
  * If you don't want binaries installed to `/usr/local`, you can set the install location with `cmake ../ -DCMAKE_INSTALL_PREFIX=/path/to/wherever`
* `make` 
* `sudo make install` (or `make install` if you are installing to a non-privileged location)
