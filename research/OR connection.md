# What other ways are there to connect to Open Remote(OR)?

*Possible ways to interface with OR using a microcontroller.*<br/>

This document was made to document my exploration of possible methods of connecting a device to OR after having trouble with the originally chosen method. the plan was to use OR's built in solution to connect the device. but after having struggled with said solution it became clear that I needed to find an alternative route to the solution for prototyping purposes.
<br/><br/>

## The problem
When trying to Connect to OR built in MQTT broker using the Microcontroller(IoT device), you will get error code 5: **authorization error**. This error has shown up using multiple different chipsets(ESP8266 and ESP32). after trail, error, and communicating with OR's CTO(Chief Technology Officer) Richard Turner, we realized it was an issue with either the TLS configuration on the microcontroller or the lack of a self signed certificate.

# MQTT
>“MQTT (originally an initialism of MQ Telemetry Transport) is a lightweight, publish-subscribe network protocol that transports messages between devices. The protocol usually runs over TCP/IP, however, any network protocol that provides ordered, lossless, bi-directional connections can support MQTT.[1] It is designed for connections with remote locations where resource constraints exist or the network bandwidth is limited. The protocol is an open OASIS standard and an ISO recommendation (ISO/IEC 20922). " -wikipedia.org

This protocol is one that I have a bit of experience with and wanted to use in the final product. Interfacing the microcontroller with OR seemed more difficult then originally anticipated. I ran into several problems connecting a device to OR to send/ receive data using my d1 mini. Making a connection using MQTT explorer proved to be much easier and well [documented](https://github.com/openremote/openremote/wiki/Tutorial%3A-Connect-your-MQTT-Client) to setup. But the main problem still  lies in the fact that I simply cant seem to get rid of my authentication error, as previously mentioned.

 
# Possible ways to connect to open remote.
After looking though the OR wiki, I have found the following ways to connect to OR:
-	Bluetooth Mesh
-	HTTP
-	KNX
-	LoRa
-	MQTT
-	Simulator
-	SNMP
-	Serial
-	TCP
-	UDP
-	Velbus
-	Websocket
-	Z-Wave

After having reviewing these possibilities, I have deemed the following solutions the most relevant the the project/situation.

## Serial
Serial means that data is being send one bit at a time instead of multiple bits.
Looking at the OR wiki page, I get the idea that It should be pretty doable. All I would need to do is setup a agent that uses a specific serial port on my laptop and setup the device to send data via the serial bus.

## Velbus
“What is Velbus? Velbus is a very reliable modular home automation system. Interconnection is done via a bus cable consisting of 4 wires (2 for power and 2 for data). There is no central unit making the system extremely reliable and simple.” – velbus.eu
Looking at the OR side of things, I see that I can use both TCP and Serial protocols to connect to a Velbus network. But considering that this is a preexisting network used for the Velbus home automation devices, I don’t think this will help with our project.

## Simulator
The simulator could be used to simulate a device, this can be useful for when the service connected is offline. The nice part about this option is that it doesn’t require any connection at all. This means I just must set it up and it will mock my device on OR. I hope I don’t have to use this method but it is nice to have it as an option.

## MQTT external broker
 Possible way to connect to OR might be through the use of a external broker like mosquito. The way this would work is that my devices would connect to my own standalone broker. After that connection is setup, which I have done multiple times in the past already to test and compare OR’s MQTT broker with a mosquito broker, I will need to connect OR to my own broker using an agent link. this setup would mean the following:<br/>
 **Microcontroller** -> **External MQTT broker** -> **OR MQTT Client**<br/>
 instead of 
 **Microcontroller** -> **OR MQTT broker**<br/>
 The external MQTT broker could be run locally or cloud based.

## Hypertext Transfer Protocol (HTTP)
HTTP is a protocol for communication between a webclient and a webserver. Using this protocol would mean having to setup HTTP webserver on a microcontroller that sends out data to a OR webclient.


 <br/><br/>


# Conclusion
In conclusion, I am going to move forward using the Serial protocol. From what I’ve seen it shouldn’t be too difficult to setup and would prove to be a valuable and simple end-to-end solution. I will continue to try and get it working via MQTT but having a working communication protocol will allow me to work on different userstories.

# Addendum 21-4-2022
As of the end of this sprint(2 weeks after this document was made) we decided to go a different route then our original conclusion. We have decided to make the connection from the IoT device to OR using an **external broker**. We are currently using **HiveMQ**'s public broker.

