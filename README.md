# Spidermon
Monitoring of a Spider Terrarium

Last year, my son got a pet velvet spider which required background heating. Instead of getting something off the shelf, I opted to build a controller with an ESP8266 and setup a thermostat so I could actively monitor the temperature and switch on the heat mat as and when required. I also wanted to monitor from Home Assistant so I could be alerted should thresholds be breached or even if the device itself went offline.

This year [2024] we got another spider (Phidippus Johnsoni) so I set about building a second controller, this time documenting the build.

## Components
Intially I was going to use a spare ESP I had laying around and a relay I also had left over from another project, but I came across a board with a built-in ESP8266 and relay which didn't require an additional 5V transformer to power the ESP so in the end I opted for that. Down the line, I will likely replace this for a relay board with a built-in ESP32 but for now the 8266 is doing the trick. For temperature/humidy reading I went with an SHT35, built into a probe for ease. I also got a USB socket so I could easily detach the SHT35 if needed.

[ESP Board](https://www.amazon.co.uk/dp/B09TGWPGCC?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=f60928b5a14e1d836d181dc494a0e8c3&camp=1634&creative=6738)

[SHT35](https://www.amazon.co.uk/dp/B09Z71YV74?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=339debb8c164a07f08e727f403a7a7f3&camp=1634&creative=6738)

[Case](https://www.amazon.co.uk/dp/B097RPCQVC?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=54d488b503d1b4e075b3e8d6c0c66f07&camp=1634&creative=6738)

[USB Socket](https://www.amazon.co.uk/dp/B002O1W7FY?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=b3855a40ffc9b383c56a0b4c0e7534f4&camp=1634&creative=6738)

[USB Terminal Connector](https://www.amazon.co.uk/dp/B07WNRLCTZ?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=1dfbfcab70f27f38aa2d4288be2a9c85&camp=1634&creative=6738)

[Heat mat](https://www.amazon.co.uk/dp/B093L9KPYT?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=29d23b692e9df1d99caf9fbe832f72d4&camp=1634&creative=6738)


## Flashing the ESP

The ESP board has some dedicated headers to flash the device and as with other 8266 chips, it needs to be put into flash mode by putting GPIO0 to GND at boot. I used a dupont to achieve this then just pulled it out when it was ready to flash. I flashed through the ESPHome interface on Home Assistant using a USB FDDI Connector. 

<img src="https://github.com/iaah05/Spidermon/assets/66481071/fe34d322-85e4-42fa-a422-205eb1cbbd50" width="300" height="380">


## The Build

I began by putting some holes in the case to feed the wires through and terminating on connecter blocks. I also used some C13/14 connecters for the heat mat for quick disconnection, without having to disturb the mat. 

<img src="https://github.com/iaah05/Spidermon/assets/66481071/f6f95e0a-8b80-44d2-9645-f44900052a0c" width="600" height="300">


Then wired the ESP board's power input and relay connection for the heat mat.

<img src="https://github.com/iaah05/Spidermon/assets/66481071/60b34722-3915-4188-b9a1-92d9ec00a743" width="600" height="300">


A hole was drilled into the rear of the spider terrarium and the SHT35 probe was inserted. I have propped this up behind one of the decorative sticks so it is less visiable and still provides a good reading.

<img src="https://github.com/iaah05/Spidermon/assets/66481071/a9ccf2db-b8dc-4f04-9782-b368e72630c3" width="300" height="300">


On the other end of the probe, it came with pre-terminated ferrules that I wired this into the USB connector with the below colours. Again this allows me to move the controller away for maintenance without disturbing the probe in the terrarium. 
\+  Red (5v)\
\-  Black (Gnd)\
D- Yellow (sdl)\
D+ Green (sda)\

<img src="https://github.com/iaah05/Spidermon/assets/66481071/f24404e4-8cfa-44da-9997-b9691f7125d8" width="400" height="200">
