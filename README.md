# Spidermon
Monitoring of a Spider Terrarium

Last year, my son got a pet velvet spider which required background heating. Instead of getting something off the shelf, I opted to build a controller with an ESP8266 and setup a thermostat so I could actively monitor the temperature and switch on the heat mat as and when required. I also wanted to monitor from Home Assistant so I could be alerted should thresholds be breached or even if the device itself went offline.

This year [2024] we got another spider (Phidippus Johnsoni) so I set about building a second controller, this time documenting the build.

## Components
Intially I was going to use a spare ESP I had laying around and a relay I also had left over from another project, but I came across a board with a built-in ESP8266 and relay which didn't require an additional 5V transformer to power the ESP so in the end I opted for that. Down the line, I will likely replace this for a relay board with a built-in ESP32 but for now the 8266 is doing the trick. For temperature/humidy reading I went with an SHT35, built into a probe for ease. I also got a USB socket so I could easily detach the SHT35 if needed.

[ESP Board](https://www.amazon.co.uk/dp/B09TGWPGCC)
[SHT35](https://www.amazon.co.uk/dp/B09Z71YV74)
[Case](https://www.amazon.co.uk/dp/B097RPCQVC)
[USB Socket](https://www.amazon.co.uk/dp/B002O1W7FY)
[USB Terminal Connector](https://www.amazon.co.uk/dp/B07WNRLCTZ)
[Heat mat](https://www.amazon.co.uk/dp/B093L9KPYT)
