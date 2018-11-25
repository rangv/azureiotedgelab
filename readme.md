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

## IoT Edge Pattern

Cloud Analytics are deployed down to IoT Devices to run them locally so that your business still operates reliabily even when connectivity is not consistent. In edge you are getting similar insights as the cloud.

![IoT Edge Pattern](/images/01_cloud_edge_pattern.png)

Steps involved in building this pattern include

1. 
    * Create an Azure IoT Hub PaaS Service
    * Identify a device to run edge capabilities and install Azure IoT Edge runtime
    * Connect Edge device to IoT Hub
  
    ![IoT Edge Pattern](/images/02_iot_hub_managed_edge.png)

2. Create Azure Services and solutions to be deployed on the Edge. Azure Services which can run on the cloud include
    * Azure Stream Analytics
    * Azure Functions
    * Azure Machine Learning
    * Azure Cognitive Services
    * Azure Event Grid

    ![IoT Edge Pattern](/images/03_iot_edge_containers_on_cloud.png)

3. Create containers and store them in a container registry like Azure Container Registry

    ![IoT Edge Pattern](/images/04_iot_edge_container_registry.png)

4. Create a deployment manifest on the cloud with Azure IoT Hub

    ![IoT Edge Pattern](/images/05_iot_hub_deployment_manifest.png)

5. Deployment manifest and associated containers are deployed to the edge device to capture insights and take actions.

    ![IoT Edge Pattern](/images/06_iot_edge_deployment_complete.png)

## Deploy Azure IoT Edge Enabled Linux VM

[Go To Azure Market Place](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft_iot_edge.iot_edge_vm_ubuntu?tab=Overview) to deploy an Azure IoT Edge enabled Linux VM.

## Modules

* [Module 1 - Create IoT HuB using VSCode](Module1)

## Useful Resources

* [Azure IoT Reference Architecture](http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
), The reference architecture provides guidance for building secure and scalable, device-centric solutions for connecting devices, conducting analysis, and integrating with back-end systems.
