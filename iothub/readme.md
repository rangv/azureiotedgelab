# Create Azure IoT Hub using VSCode

## Overview

**Azure IoT Hub** is the core Azure PaaS. IoT Hub enables reliable and securely bidirectional communications between millions of IoT devices and a cloud solution. IoT Hub helps you meet IoT implementation challenges such as:

* High-volume device connectivity and management.
* High-volume telemetry ingestion.
* Command and control of devices.
* Device security enforcement.

### Install VSCode Editor

If you have not installed VSCode, Click [here](https://code.visualstudio.com/) and download the IDE based on your machine OS. macOS, Windows and Linux are supported.

Open VSCode Editor.

## VSCode IoT Extensions

Install Azure IoT VSCode Extensions

![Extensions](/iothub/images/06_extensions.png)

Azure IoT supports 3 extensions

1. **Azure IoT Edge Tools** makes it easy to code, build, deploy, and debug your IoT Edge solutions.

    * Create new Azure IoT Edge project
    * Add new IoT Edge module (C#) to solution
    * Edit, build, run, and debug IoT Edge modules locally on your machine
    * Build and publish IoT Edge module Docker images
    * Manage IoT Edge devices and modules in IoT Hub (with Cloud Explorer)
    * Deploy IoT solutions to IoT Edge devices

2. **Azure IoT Toolkit** helps with Interact with Azure IoT Hub, IoT Device Management, IoT Edge Management and IoT Hub Code Generation.

    * IoT Hub Management
    * Device Management
    * Edge Module Management
    * Interact with IoT Hub
    * Interact with IoT Edge

3. **Azure IoT Workbench**, the IoT Workbench extension makes it easy to code, build, deploy and debug your IoT project with multiple Azure services and popular IoT development boards. IoT Workbench aims to support multiple popular IoT development boards and kits. It currently supports following IoT hardware:
    * MXChip IoT DevKit
    * teXXmo IoT button
    * Raspberry Pi
    * ESP32

### Sign-in to Azure

```editor
Press (Control + Shift + P) in VSCode editor.
Enter >Azure:Sign in to Azure Cloud
```

Select Sign In to Azure Cloud

![Sign In](/iothub/images/10_azure_signin.png)

Select Your Azure Cloud

![Sign In](/iothub/images/11_azure.png)

If you have not signed-in into Azure from VSCode you will be presented with a dialog to sign in to Azure.

![Sign In](/iothub/images/02_signing_to_iothub.png)

A browser URL and code will be provided. Click **Copy**, go to browser and type URL: http://microsoft.com/devicelogin and paste the code in the browser. You will be asked to sign in with your Azure credentials.

### Create IoT Hub Instance

Once successfully signed-in to Azure you will be presented with a Subscription list.

![Select Subscription](/iothub/images/03_select_subscription.png)

1. Select the subscription you would like to use for this lab.
2. Create a resource group or select an existing resource group.
3. Select the region in which you would like to create the IoT Hub
4. Select Pricing and scale tier. For this lab you can select a **Basic** or **Standard** Tier.
5. Provide a name to your IoT Hub. Make sure its a unique name

An IoT Hub will be created for you.

![Create IoT hub](/iothub/images/04_iothub_creation.png)

Go To Azure portal to verify IoT Hub creation

![IoT Hub](/iothub/images/05_iothub_overview.png)
