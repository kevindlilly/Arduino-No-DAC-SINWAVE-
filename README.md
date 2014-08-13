Arduino-No-DAC-SINWAVE-
=======================

Output a sine wave with just resistors on your Arduino

If you want a sine wave out you do not need a DAC . Just attach a resistive array to a set of pins . I used a bus terminator.
Eight 1 meg ohm resistors tied together . Each pin provides additional current to the common point. By creating a loop of count up , count down nested loops you get 1-8 then 8-1 . Using an oscilloscope you will see a sine wave.

This method will provide almost no current . A high impedance amplifier will be required to make the output usefull.

At full speed the rise and fall time will smooth the output . As you add delay between each step you lower the frequency but see a more stepwise waveform.

The included code will demonstrate full speed and then a lower speed. 
I have also included a swept wave that adds delay then subtracts delay.

I will comment out the sweep to make testing easier.

The max frequency will depend on the system clock.

I know a faster method is possible but this is easy to understand.

