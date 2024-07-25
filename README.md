# Aardbei
EEPROM dumps from Aardbei

I have a 2014 Toyota Yaris 1.5 LE (NCP131) and the stock instrument cluster doesn't have a tachometer.
This bothered me.

I managed to obtain (thanks to Ebay) the instrument cluster from a Lithuanian Yaris/Vitz 1.3 Sport (NSP130) which miraculously had the golden combo of both a tachometer and speedometer markings in MPH.
I hoped it would be a nice and easy drop-in replacement and it *almost* was. The tachometer worked right off the bat, but the new cluster didn't properly display the current gear, the thermometer displayed temperatures in Celsius, and whenever I turned on the headlights the backlights on the climate controls and radio would turn off. I was also surprised to see that the odometer reading was wrong.

Luckily, I found some documentation online of people who have successfully reprogrammed the dash cluster EEPROM to correct the odometer reading after replacing the cluster.
The trick is to use a CH341A EEPROM programmer which has been modified to be able to read and write 93X series EEPROMs. The EEPROM on Toyota instrument clusters can usually be found on the top side of the PCB right under the speedometer faceplate. The chip on my dash is an M93C66, which is supported by AsProgrammer (I used version 2.0.4).
See this tutorial for modifying the programmer: https://www.youtube.com/watch?v=hPKckby54uA

After dumping the EEPROM from both the old and new instrument clusters (which can be found in this repository), I corrected the odometer reading based on this forum post: https://www.toyotanation.com/threads/diy-odometer-reprogramming-for-swapped-clusters.1504706/. Of course, I first tried to take the EEPROM from my old cluster and swap it into the new cluster. Everything worked except for the tachometer and speedometer T___T

After a few hours of staring at a hex diff comparing the old and new EEPROM dumps and systematically experimenting with swapping chunks of the code, I figured out how to get the tachometer to work and get the temperature to display in Farenheit. I'm continuing to work on figuring out how to get the current gear to display properly, and the radio lights are still weird.
The bin file I flashed to the new cluster can be found in this repository as "New Aardbei Dash EEPROM attempt 13.bin".

I hope this one day helps somebody else foolish enough to do the same thing!
