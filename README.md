# Plant-Sensor
This Repo contains the code and technical data for the Plant Sensor.

# Setup
In this guide I am going to touch an the basic requirements and steps that have been and should be taken in order to get the sensor working and connected to Open remote.

## Prerequisites
First things first, what do you need?<br/>
### Hardware
For the hardware you will need the following:
![TTGO-T-Higrow.png](media/TTGO-T-Higrow.png)
-   **TTGO-T-HIGrow.** *This device is the IoT device that will actually measure your plant. The TTGO-T-HIGrow will be used to detect the following: soil moisture, light, temperature and air moisture. that and the WIFI capabilities will be required for the device to function within this context<br/> apart from the device being able to collect all the relative data, it also comes with a nice protective housing and battery.*<br/>

### Software

-   **This repo.** *This repo contains the code for the IoT device. Included with that are a total of 4 libraries from external sources: Adafruit_BME280_Library, NTPClient, PubSubClient and Timelib.*
-   **[Docker](https://docs.docker.com/desktop/windows/install/).** *Docker is required to for the Open Remote instance to run.*
-   **[Open Remote](https://github.com/openremote/openremote/blob/master/README.md) instance (Docker).** *Open Remote is used to display sensor data.*
-   **[Visual Studio Code](https://code.visualstudio.com/) with [PlatformIO extension](https://platformio.org/install/ide?install=vscode).** *VSC is a code editor and PlatformIO is a extension that will help you run and monitor code for the IoT device.*



## IoT device
This project is based of of [Pesor's TTGO-T-HIGrow project](https://github.com/pesor/TTGO-T-HIGrow) code. Before you can start configuring, you need to make sure you have the right environment setup, for this you will need **Visual Studio Code** paired with the **PlatformIO extension**. The following video will give you a good idea how to set them both up.
[![explanation video](https://img.youtube.com/vi/sm6QxJkWcSc/0.jpg)](https://youtu.be/sm6QxJkWcSc?t=263)


Before you can upload the code to your device you need to setup the config file located at include/user-variables.h.
You need to setup your network connection, broker connection and configure sensor data.
<br/><br/>

![network_settings.png](media/network_settings.png)<br/>
In order to configure the device to your needs, you need to set your network name/names instead of NETWORK_1 and NETWORK_2. the password should be put inside the `password` field. If you have more or less networks to connect to you must also change the `ssidArrNo` accordingly.
<br/><br/>

![broker_settings.png](media/broker_settings.png)<br/>
For the broker you need to insert your brokers address and your port. The port usually is 1883.
If you are using a broker that requires credentials you can add them in the `mqttuser` and `mqttpass` field
<br/><br/>

![sensor_settings.png](media/sensor_settings.png)<br/>
To calibrate the soil sensor.....
<br/><br/>

For more info please visit [Pesor's TTGO-T-HIGrow project setup guide](https://github.com/pesor/TTGO-T-HIGrow/wiki/05.-user-variables.h)

## Broker
### Using HiveMQTT(no setup required)

### Using Mosquito

## Open Remote

### Installing open remote
Open Remote's wiki page has a really good and comprehensive [quick start guide](https://github.com/openremote/openremote/blob/master/README.md) that will help you setup your staring OR environment.

### Configuring
https://youtu.be/sm6QxJkWcSc?t=263