# Create Azure IoT Hub using VSCode

## Overview

**Azure IoT Hub** is the core Azure PaaS. IoT Hub enables reliable and securely bidirectional communications between millions of IoT devices and a cloud solution. IoT Hub helps you meet IoT implementation challenges such as:

* High-volume device connectivity and management.
* High-volume telemetry ingestion.
* Command and control of devices.
* Device security enforcement.

### Install VSCode Editor

Open VSCode Editor. If you have not installed VSCode, Click [here](https://code.visualstudio.com/) and download the IDE based on your machine OS. macOS, Windows and Linux are supported.

```editor
Press (Control + Shift + P) in VSCode editor.
```

### Sign-in to Azure

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