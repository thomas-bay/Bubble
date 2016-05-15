# Bubble
My Photon project for monitoring progress of fermentation of beer:

Project includes:
* I2C interface to the MMA8451 Accelerometer
  The principle is that the accelerometer detects vibration caused the CO2 rushing/bubbling through he airlock.
  The MMA is set up to detect single taps in z direction. The photon polls the chip every second and reports a tap event via UDP to the server.
* UDP client is used for reporting each bubble event (requires a UDP server running somewhere).
  The connection is established at every event.
* A class for executing generic registered events at specific intervals (or once)
* uses: serial
* uses: a few cloud variables.

UDP server (no part of this project):
* receives the UDP datagram and stores the payload without formatting in a file Bubble.log
* listens for connections at port 9843

EventClass:
Method AddEvent(void * f(), int period) add an function pointer to the event list together with a period (in ms) and the time (in ms) for next call.    
If period is 0, only one call is made.
