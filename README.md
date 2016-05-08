# GP20U7 GPS Library
A very simple library for interfacing with the [GP-20U7 GPS unit](https://www.sparkfun.com/products/13740). Supports the P1, Core, Photon, and Electron devices.

## Hardware Connection
Connect the power pins on the GP-20U7 to the 3.3V and GND connections on your particle device. Connect the TX pin of the unit to the RX pin on your particle board. 

## Installation
Include the GP20U7_PARTICLE library in your Web IDE project.

## Usage
### Constructor
```c
GP20U7(Stream*);
```

### Methods
| Method         | Description                                                                                                                                           |
|----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| begin          | Called in the setup() function to initialize the gps and prepare the associated stream                                                                |
| read           | Called repeated in the loop() function to check for new location information. Returns true if new position information is available. False otherwise. |
| getGeolocation | Returns the currently stored geolocation information. 

## Example
```c
// include the library code:
#include "gp20u7_particle/gp20u7_particle.h"

// initialize the library with the serial port to which the device is
// connected
GP20U7 gps = GP20U7(Serial1);

// Set up a Geolocation variable to track your current Location
Geolocation currentLocation;

void setup() {
  // Start the GPS module. You don't need to call setup() on the serial
  // object as this is taken care of for you
  gps.begin();
}

void loop() {
  // The call to read() checks for new location information and returns 1
  // if new data is available and 0 if it isn't. It should be called
  // repeatedly.
  if(gps.read()){
    currentLocation = gps.getGeolocation();
    // do something with the new geolocation information
  }
}
```
