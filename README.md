# Spidermon
Monitoring of a Spider Terrarium

Last year, my son got a pet velvet spider which required background heating. Instead of getting something off the shelf, I opted to build a controller with an ESP8266 and setup a thermostat so I could actively monitor the temperature and switch on the heat mat as and when required. I also wanted to monitor from Home Assistant so I could be alerted should thresholds be breached or even if the device itself went offline.

This year [2024] we got another spider (Phidippus Johnsoni) so I set about building a second controller, this time documenting the build.

## Components
Intially I was going to use a spare ESP I had laying around and a relay I also had left over from another project, but I came across a board with a built-in ESP8266 and relay which didn't require an additional 5V transformer to power the ESP so in the end I opted for that. Down the line, I will likely replace this for a relay board with a built-in ESP32 but for now the 8266 is doing the trick. For temperature/humidy reading I went with an SHT35, built into a probe for ease. I also got a USB socket so I could easily detach the SHT35 if needed.

[ESP Board]([https://www.amazon.co.uk/dp/B09TGWPGCC](https://www.amazon.co.uk/dp/B09TGWPGCC?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=f60928b5a14e1d836d181dc494a0e8c3&camp=1634&creative=6738))
[SHT35]([https://www.amazon.co.uk/dp/B09Z71YV74](https://www.amazon.co.uk/dp/B09Z71YV74?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=339debb8c164a07f08e727f403a7a7f3&camp=1634&creative=6738))
[Case]([https://www.amazon.co.uk/dp/B097RPCQVC](https://www.amazon.co.uk/dp/B097RPCQVC?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=54d488b503d1b4e075b3e8d6c0c66f07&camp=1634&creative=6738))
[USB Socket]([https://www.amazon.co.uk/dp/B002O1W7FY](https://www.amazon.co.uk/dp/B002O1W7FY?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=b3855a40ffc9b383c56a0b4c0e7534f4&camp=1634&creative=6738)https://www.amazon.co.uk/dp/B002O1W7FY?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=b3855a40ffc9b383c56a0b4c0e7534f4&camp=1634&creative=6738)
[USB Terminal Connector]([https://www.amazon.co.uk/dp/B07WNRLCTZ](https://www.amazon.co.uk/dp/B07WNRLCTZ?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=1dfbfcab70f27f38aa2d4288be2a9c85&camp=1634&creative=6738)https://www.amazon.co.uk/dp/B07WNRLCTZ?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=1dfbfcab70f27f38aa2d4288be2a9c85&camp=1634&creative=6738)
[Heat mat]([https://www.amazon.co.uk/dp/B093L9KPYT](https://www.amazon.co.uk/dp/B093L9KPYT?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=29d23b692e9df1d99caf9fbe832f72d4&camp=1634&creative=6738)https://www.amazon.co.uk/dp/B093L9KPYT?&_encoding=UTF8&tag=iaah05-21&linkCode=ur2&linkId=29d23b692e9df1d99caf9fbe832f72d4&camp=1634&creative=6738)
