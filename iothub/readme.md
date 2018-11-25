# Azure IoT Edge Hands On Labs With Edge Enabled MarketPlace VM

## Overview

Azure IoT Edge is a fully managed service that delivers cloud intelligence locally by deploying and running

* Artificial Intelligence (AI)
* Azure Services
  * Azure Stream Analytics
  * Azure Functions
  * Azure Machine Learning
  * Azure Cognitive Services
  * Azure Event Grid
* Custom Logic
  
directly on cross-platform IoT devices. Run your IoT solution securely and at scale—whether in the cloud or offline.

This hands-on lab demonstrates what is involved in standing up an Azure IoT Edge enabled Linux VM on Azure Marketplace and running Edge Modules.

In this workshop you will:

* Create an Azure IoT Edge Linux VM from Azure Market Place

## Deploy Azure IoT Edge Enabled Linux VM



[Go To Azure Market Place](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft_iot_edge.iot_edge_vm_ubuntu?tab=Overview) to deploy an Azure IoT Edge enabled Linux VM.



For the lab hardware, you need at a minimum, a RaspberryPi (2, 3, or ZeroW), a DHT22 temperature and humidity sensor, LED, resistors, breadboard and wires.  If you don't already have hardware, you can buy the kits from the links below (among many other places)

## Modules

* [Module 1 - Azure IoT Remote Monitoring pre-configured solution](Module1) 
* [Module 2 - Connect Device to IoT Hub](Module2)
    * [(optional) Module 2b - Connect Device to IoTHub via Gateway](Module2b)
    * [(optional) Module 2c - An alternative to Module2 for when sensors are not available. This module simulates the sensor data](Module2c)
* [Module 3 - Azure Stream Analytics](Module3)
* [Module 4 - Azure Functions](Module4)
* [Module 5 - Device Management](Module5)

### Prerequisites

* Install python 2.7 https://www.python.org/downloads/
* Install the Device Explorer tool from https://github.com/Azure/azure-iot-sdks/releases/download/2016-11-17/SetupDeviceExplorer.msi
* Install Putty (if on a Windows PC) - http://www.putty.org/ 
* If you want to do the Gateway SDK module (2b), install the Arduino IDE at http://arduino.cc
* Install drivers for the USB to Serial cable (we provide the actual cable) - https://learn.adafruit.com/adafruits-raspberry-pi-lesson-5-using-a-console-cable?view=all 
* Access to an Azure Subscription

### Useful Resources 

#### Azure IoT Reference Architecture
The reference architecture provides guidance for building secure and scalable, device-centric solutions for connecting devices, conducting analysis, and integrating with back-end systems.

http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf

#### Azure IoT Preconfigured Solutions
The Azure IoT Suite preconfigured solutions are implementations of common IoT solution patterns that you can deploy to Azure using your subscription. You can use the preconfigured solutions: As a starting point for your own IoT solutions. To learn about common patterns in IoT solution design and development.

https://azure.microsoft.com/en-us/documentation/articles/iot-suite-what-are-preconfigured-solutions/

https://github.com/Azure/azure-iot-remote-monitoring 

#### SDKs

https://github.com/Azure/azure-iot-sdks - device sdk

https://github.com/azure/azure-iot-gateway-sdk - device gateway sdk

https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md - protocol gateway

#### Security
[Securing Your Internet of Things from the Ground Up](http://download.microsoft.com/download/8/C/4/8C4DEF9B-041B-47F3-AD7F-52F391B1D0AB/Securing_your_Internet_of_Things_from_the_ground_up_white_paper_EN_US.pdf)

[How enterprises can enable IoT security]( http://blogs.microsoft.com/iot/2016/03/07/how-enterprises-can-enable-iot-security/#QoDqUlfc7CWlYhHf.99)

#### Other Services
[Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/)

[Azure Stream Analytic](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-introduction )

[Azure App services](https://docs.microsoft.com/en-us/azure/app-service/app-service-value-prop-what-is) 

[Azure logic app](https://docs.microsoft.com/en-us/azure/logic-apps/) 

[Azure HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/ )

[Azure Machine Learning](https://studio.azureml.net/)

[PowerBi](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/ )

[SignalR](https://www.asp.net/signalr/overview/deployment/using-signalr-with-azure-web-sites) 
