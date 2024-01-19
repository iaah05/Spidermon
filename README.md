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


## The Code

I'm still tweaking aspects of the code but the full YAML for ESPHome is here: [spidermon2.yaml](https://github.com/iaah05/Spidermon/blob/main/spidermon2.yaml)

The key elements are setting up the i2c component, bang_bang thermostat and setting up times for thermostat preset changes.

### i2C Component

The SHT35 uses i2c, so your need to define in your ESPHome code which pins will be setup for i2c bus. I made a comment for the wire colours so I didn't forget.
```
i2c:
  sda: GPIO12 #green
  scl: GPIO13 #yellow
  id: bus_a  
  scan: true
```

This was then tied into the sht3xd sensor platform and given appropriate names and ids. Be sure to match i2c_id in your sensor to the id defined under the i2c component.
```
sensor:
  - platform: sht3xd
    i2c_id: bus_a
    temperature:
      name: "Spider2 Temperature"
      id: "Spider2_temperature"
    humidity:
      name: "Spider2 Humidity"
      id: "Spider2_humidity"
    update_interval: 25s
```    

### Relay/Heat Mat
The pin that connects to the on-board relay needs to be defined, on this board it is GPIO05. This is what will control power to the heat mat.
``` 
switch:
  - platform: gpio
    id: relay_heater2
    name: "Spider2 Heater"
    pin: GPIO05
```

### Thermostat

There are two different types of thermostats available in ESPHome, I went with bang_bang as only needed heating and it seemed to fit my needed. I have used two presets for this config, the default (home) which will run in the day and the "away" which I will switch to at night. I'm still tweaking some of these temperatures to best suit the spiders needs. This ties together the temperature readings with the heat mat.
```
climate:
  - platform: bang_bang
    id: Spider2_thermostat
    name: "Spider2 Thermostat"
    sensor: Spider2_temperature
    default_target_temperature_low: 22 C
    default_target_temperature_high: 24 C
    away_config:
      default_target_temperature_low: 17 C
      default_target_temperature_high: 18 C

    heat_action:
      - switch.turn_on: relay_heater2
    idle_action:
      - switch.turn_off: relay_heater2
```

### Auto-switch of Presets

I wanted to auto switch between the heating presets so that it would be cooler at night (mirroring a real habit a bit more) whilst still providing some background heat as it gets quite cold in the UK in Winter time. I used the time component to switch between the home and away presets.
```
time:
  - platform: homeassistant
    id: homeassistant_time  
  - platform: sntp
    on_time:
      - seconds: 0
        minutes: 00
        hours: 7
        then:
          - climate.control:
              id: Spider2_thermostat
              preset: HOME      
      - seconds: 0
        minutes: 00
        hours: 20
        then:
          - climate.control:
              id: Spider2_thermostat
              preset: AWAY
```

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


The other end of the probe came with pre-terminated ferrules that I wired this into the USB connector with the below colours. Again this allows me to move the controller away for maintenance without disturbing the probe in the terrarium.\
\+  Red (5v)\
\-  Black (Gnd)\
D- Yellow (sdl)\
D+ Green (sda)

<img src="https://github.com/iaah05/Spidermon/assets/66481071/f24404e4-8cfa-44da-9997-b9691f7125d8" width="400" height="200">


The other end of the USB socket had different colours, they went to the ESP Chip pins:\
5V  Red (5v)\
Gnd  Black (Gnd)\
GPIO13 White (sdl)\
GPIO12 Green (sda)

## Next Steps

Whilst the heating component is working at the moment, there are still some improvements I want to make. An obvious one is controlling the LED light I have over the top of the terrarium. It is powered using a USB plug so I plan on using a MOSFET controlled by software PWM on the ESP to simulate sunrise and sunset. I already have an automation in Home Assistant to alert me if the ESP goes offline but I plan to create additional automations for high/low temperature and humidity threasholds. 

Thank you for reading.

<img src="https://github.com/iaah05/Spidermon/assets/66481071/7fdc1ed6-551f-45bd-991a-41b0a37516ca" width="300" height="300">

