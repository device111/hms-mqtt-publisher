# hms-mqtt-publisher

This tool fetches the current telemetry information from the HMS-XXXXW-T2 series of micro-inverters and publishes the information in JSON format to an MQTT broker. Please note that it doesn’t implement a DTU, but pulls the information off the internal DTU of these inverters. 

### How to run
The tool is distributed as source only — for now. You’ll have to download, compile and run it yourself. 

```
$ git clone https://github.com/DennisOSRM/hms-mqtt-publisher.git
$ cd hms-mqtt-publisher
$ cargo r --release [inverter] [mqtt broker] [mqtt user] [mqtt password]
```
![image](https://github.com/lumapu/ahoy/assets/1067895/32c0b9b6-5aea-41e3-b9f8-161ce82fb99a)

### Note of caution
Please note: The tool does not come with any guarantees and if by chance you fry your inverter with a funny series of bits, you are on your own. That being said, no inverters have been harmed during development. 

### Known limitations
- One can only fetch updates approximately twice per minute. The inverter firmware seems to implement a mandatory wait period of a little more than 30 seconds. If one makes a request within 30 seconds of the previous one, then the inverter will reply with the previous reading and restart the countdown. It will also not send updated values to S-Miles Cloud if this happens. 
- The tool is a CLI tool and not a background service. 
- The tools was developed for (and with an) HMS-800W-T2. It may work with the other inverters from the series, but is untested at the time of writing
