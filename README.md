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

I know a faster method is possible but this is easy to understand

https://gist.github.com/kevindlilly/7d63093947ca887244fb



/*  RESISTIVE LADDER DAC OUTPUT
    THIS WILL PRODUCE A SINEWAVE
    
    Connect a 1 Meg resistor to each pin.
    Connect all the resistors together.
    At the common point you will measure a SINE WAVE.
    With an oscilloscope.
    To create a usefull output a high impedance amplifier is required.
    
*/    



void setup()
{
 pinMode(2,OUTPUT); 
 pinMode(3,OUTPUT); 
 pinMode(4,OUTPUT); 
 pinMode(5,OUTPUT); 
 pinMode(6,OUTPUT); 
 pinMode(7,OUTPUT); 
 pinMode(8,OUTPUT); 
 pinMode(9,OUTPUT); 
 pinMode(10,OUTPUT); 
 
}

void loop()
{
 // Call the Max Frequency loop 10,000 times
   for ( unsigned int lt=0; lt <= 10000; lt++){ // lt = loop time 
     MaxFrequency(); 
   } 
 
 delay(200);
 // Max frequency loop END
 
 //Call the LOWER FREQUENCY loop 10,000 times
  for ( unsigned int LFlt=0; LFlt <= 10000; LFlt++){ //LFlt = Lower Frequency loop time
     Frequency(10); // 10 delayMicroseconds
   } 
   delay(200);
   
    //Call the  LOWER FREQUENCY loop 10,000 times with a longer delay between steps
  for ( unsigned int LFlt=0; LFlt <= 10000; LFlt++){  //LFlt = Lower Frequency loop time
     Frequency(100); // 100 delayMicroseconds
   } 
   delay(200);
   
   // Lower Frequency END
 /*   Uncomment this block to enable sweep
 
 // Call the Frequency  function 200 times  the loop time is much longer so less loops
  for (unsigned int St=0; St <= 200; St ++)  // ST = Sweep time
{
  for (int F=1; F <= 30; F = F + 1) // F = Delay    Longer delay = lower frequency
  {
     Frequency(F); // Pass F as TIME to Frequency function
   } 
    for (int F=50; F >= 1; F = F - 1){
     Frequency(F); 
  } 
   delay(200);
  }
 
 // Sweep Frequency LOOP END   
 */ 
// Uncoment to enable sweep  
}

void MaxFrequency()
{
      for (int UP=2; UP <= 10; UP++)  // Count UP pins 2 - 10   Change or add pins here
     {
      digitalWrite(UP, HIGH);
      } 
     for (int DOWN=10; DOWN >= 2; DOWN--)  // Count Down   pins 10 - 2   Change or add pins here
     {
      digitalWrite(DOWN, LOW);
     }
}


void Frequency(int TIME) // TIME = Delay time 
{
   for (int UP=2; UP <= 10; UP++)  // Count UP pins 2 - 10   Change or add pins here
     {
      digitalWrite(UP, HIGH);
      delayMicroseconds(TIME);
     } 
   
    for (int DOWN=10; DOWN >= 2; DOWN--)  // Count Down   pins 10 - 2   Change or add pins here
     {
      digitalWrite(DOWN, LOW);
      delayMicroseconds(TIME);

     }
    delayMicroseconds(10); // Twiddle this for oscilloscope sync 
}
  


