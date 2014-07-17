## XBee notes


### coordinator node

**firmware** = ZigBee Coordinator API

**ID** = unique to this coordinator _i.e. unique to this building / sensor network_

**AR** = e.g. 6 _to set up "many-to-one" routes back to this coordinator every 6*10 seconds = 1 minute_


### sensor node

**firmware** = ZigBee Router AT

**PAN ID** = same as coordinator

(default) **DH/DL** = 0/0 _which sets the destination to be the coordinator_

(default) **AR** = 0xFF _which disables broadcasting routes to the sensor, because no one will ever be talking to the sensor_

**D1** = 2 _to set AD1 as analog read_

**IR** = e.g. 60000 _to sample every 60,000ms = 1 minute_

_TODO_ is it important to connect VREF to VCC?


## Raspberry π notes

### overview

connect to the coordinator node via usb board

listen for IO frames, which are of the form 0x7E....92

use a (manually maintained) mapping of 64-bit sensor addresses to apartments, to record apartment temperatures

### FTDI

VCP drivers don't seem to work on ARM (and thus π), so options are D2XX which seems annoying, or libftdi

to test on a Mac:

    brew install libftdi
    pip3 install pylibftdi
    sudo kextunload -bundle-id com.apple.driver.AppleUSBFTDI
