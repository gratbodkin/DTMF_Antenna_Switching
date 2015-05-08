# DTMF_Antenna_Switching
Software for wireless DTMF controlled antenna switching control for amateur radio - for use with Atmega328
/*
The purpose of this software is to be able to switch between multiple antennas connected to the Amateur radio
repeater at UCSC.  One antenna is vertically polarized, while the other is circularly polarized, and as a result
they each have different radiation emmision patterns, resulting in different signal strengths, depending on where
you are. Switching from one antenna to the other is achieved by means of wireless DTMF control from a handheld
transceiver in the field. The software is set up to require a 5-digit DTMF code to enable antenna switching.
Default codes are (5,6,7,8,9) for enabling the circularly polarized antenna, and (9,8,7,6,5) for enabling the
vertically polarized antenna.

Upon successfully receiving a code to enable either of the antennas, the software will check to see if that
particular antenna is already enabled, and if it is, the software simply returns to an idle state.  Otherwise,
before switching antennas, the software will first send a signal to disable the NHRC2 repeater controller, followed
by disabling the currently enabled antenna.  A feedback signal ( (X)POL_STATUS)  is checke to confirm that the
antenna was correctly switched off.  One the status bit is confirmed, an enable signal is sent to the desired
antenna, followed lastly by checking the status bit of the newly enabled antenna in order to confirm that it was
correctly switched on.

This software is written for use with a MT8870 DTMF decoder chip. The input pin ST_CTRL_BIT acts as
a control signal letting the software know that a new DTMF tone has been detected.  Upon detecting a rising edge
from te CTRL bit, the inputs corresponding to DTMF bits 0-3 are read as binary, and compared to a lookup table
in order to confirm which digit has been sent.



This software requires the Arduino LiquidCrystal library to run as is.
If you dont want to use the LiquidCrystal library, simply comment out the
print statements that use it, and use the serial output for debugging.

Although this software was written for a somewhat specific system, the DTMF decoding portion of it is portable and ca$
certainly be used for other applications requiring software that reacts to dtmf events. (with an 8870 dtmf decoder ch$

*/
