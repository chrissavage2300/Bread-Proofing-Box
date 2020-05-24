# Bread-Proofing-Box
A PID controlled bread proofing box with heater

<H3>Change log</H3>
<b>5/24/2020</b> A major error was found. The power IC's IC2 and 3 are backwards. I thought I fixed it from an older revision, but guess not. Either way the current board is a dud :(. Also the transformer doesnt fit either, so this is now in pause while I wait and do another PCB revision.

<b>5/11/2020</b> Added in documents to show heatsink calculations along with heater wire calculations


<b>5/11/2020</b> Idea: Timer function on screen, count down? Time Remaining. Have buzzer go off when "done". This would be useful for a hydrate function.

<b>5/08/2020</b>- Board sent to PCB maker.

<b>5/03/2020</b>-Initially started with a PIC16F15356 but realized that it may need more memory for running a glcd. Also may need more processing power and higher clock frequency's so I may go with a 18F26Q10. 

Also I may rethink the heater. It kind of smells like burning plastic when on, so I may design my own using Nichrome 60 wire

<b>4/28/2020</b>-Got mechanical encoder code working. Also stuck the heater in the box to get an idea of what kind of temps I could expect. It seemed to max out to around 114F and then the shutoff kicked in slightly after that. So the max temp should be around 120F. It took around 10 minutes to get up to this temp. Its not high enough for dehydration, but it is hot enough for bread making and yogurt making. Wonder how hot it would get if the over temp switch was bypassed. 

Display thoughts:
* Internal Temperature (°F)
* External Temperature (°F)
* Humidity (%)
* Run Time (HH:MM:SS)
* Set Temperature (°F)

More thoughts: I could use this box to dry soap.

Since I want to keep the integrity of the box, maybe I should mount the system on the top of the box. This way I can still use the box for storage when not in use. So have the heater fan on top and it can be a dual use fan for intake, and then have another fan on the opposite end on top for exhaust. 


<b>4/26/2020-Initial Idea</b>


Ideas/wants: Spawned from the sour dough book I have that talks about a storage box or a cooler along side a light to proof bread dough or proof sour dough starter. They use a light bulb, but my experience with bulbs is that they get pretty hot, almost to 90-100F. I only know this because I used them to start seeds as well. I had then begun to search around for heaters, initially I thought of winding my own using nichrome or kanthal wire, but deemed that too be unsafe as I could possibly touch it by accident.

Next I thought of using a cartridge heater, it could work but felt like it would be too inefficient. I finally settled on using just a small space heater. When this is done there is another added benefit: I can dehydrate food or make yogurt. I dont know yet what the lower and upper temperature bounds are of a 250W heater.

Features/Additions:
* A HDX 12 gallon storage bin is just big enough for the bowl I use and can fit a jar or two inside as well
* 250W 120VAC Heater from Walmart. Cant wait to take it apart! I have a suspicion its like the so called "100W 12V PTC heater" on ebay.
* I figure I'll add in an intake fan as well for cool or room temp air. Oh boy..if I wanted to cool the air that would be interesting. 
* Which suggests a dual PID of sorts. I dont have one PID working yet, but I have some code that might work thats unfinished. 
* PID 1 will control the heater
* Maybe have the heater fan run at 100% all the time and just be on/off control. 
  * Control Strategy
  1) PWM Will vary the heater to accommodate a set temperature.
  2) Heater Fan will Turn on or off depending on if its needed or not. So, if the heater is ramping up, the fan will come on. This suggests really long loop refresh times, maybe 10 seconds should be good. Its a small box.
  3) So if the box is at the set temperature, the heater will be at some value, and the fan will be circulating air pretty much. The heater doesnt need to be shut off in this case, but the duty cycle will be low probably. Maybe add in an input to shut the PID off but keep the fan on to circulate air? 
* Optional: Cool Air/Room temperature Air intake. Control scheme would probably be to turn on this fan if its get too hot and shut the heater off completely and just keep the recirculation fan running.   
* Complex Add on: 3D printed louver doors so heat isnt lost when the cooling fan isnt on. 
* Exhaust fan and intake fan. Heater fan will be the recirculation fan. 

IO List:
* Start Button
* Stop Button
* Quadrature Encoder Knob to select temperature
* Internal Analog Temperature (MCP 9700)
* External Analog Temperature
* Internal Analog Humidity
* Intake Fan-PWM or DO
* Exhaust Fan-DO
* Heater fan/Recirculation Fan-PWM or DO
* I2C Display, so 2 extra IO
* ZCD input to sync heater but this can be acommplished with extra circuitry too
* 32kHz Crystal for clock

Based on this, I would use one of the following PIC micro's
* PIC16F1773
* PIC16F15355
* ~~PIC18F24Q10~~
* ~~PIC18F24K40~~

The Box:
![Box](https://raw.githubusercontent.com/chrissavage2300/Bread-Proofing-Box/master/Photos/20200428_120737%5B1%5D.jpg)
