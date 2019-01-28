# Add an Edge Module and Deploy to Edge Device

## Overview

One of the key capabilities of Azure IoT Edge is being able to deploy modules to your IoT Edge devices from the cloud. An IoT Edge module is an executable package implemented as a container. In this section, you deploy a module that generates telemetry for your simulated device.

## Steps

In the Azure portal

* Navigate to your IoT hub.

* Go to IoT Edge under Automatic Device Management and select your IoT Edge device.

* Select Set Modules.
  
A three-step wizard opens in the portal, which guides you through

    * adding modules,
    * specifying routes, and
    * reviewing the deployment.

Under Explorer select **IoT Edge** and select Edge Device
![Edge Device](/edgemodule/images/01_iot_edge_device.png)

Click on **Set Modules**

![Set Modules](/edgemodule/images/02_iot_edge_set_modules.png)

In the Add Modules step of the wizard, find the Deployment Modules section. Click Add then select IoT Edge Module.

![Add Edge Module](/edgemodule/images/03_edge_module.png)

Use the Temperature Sensor Simulator pre-built module.

In the Name field, enter tempsensor.

In the Image URI field, enter mcr.microsoft.com/azureiotedge-simulated-temperature-sensor:1.0.

Leave the other settings unchanged, and select Save.

![Temp Sensor](/edgemodule/images/04_edge_tempsensor.png)

In the Specify Routes step of the wizard, you should have a default route that sends all messages from all modules to IoT Hub. If not, add the following code then Click **Next**

![Modules Runing](/edgemodule/images/05_edge_module_running.png)

```json
{
    "routes": {
        "route": "FROM /messages/* INTO $upstream"
    }
}
```

In the Review Deployment step of the wizard, select Submit.

![routes](/edgemodule/images/06_edge_module_routes.png)

Click **Submit**

![Submit](/edgemodule/images/07_edge_module_submit.png)

Return to the device details page and select **Refresh**.

In addition to the **edgeAgent** module that was created when you first started the service, you should see another runtime module called **edgeHub** and the **tempSensor** module listed.

It may take a few minutes for the new modules to show up. The IoT Edge device has to retrieve its new deployment information from the cloud, start the containers, and then report its new status back to IoT Hub.

![modules](/edgemodule/images/08_edge_module_deployed.png)

SSH into Linux VM and list the modules. You will see the 3 modules deployed on to the edge device. Use command

```linux
iotedge list
```

![modules](/edgemodule/images/09_edge_deployed_modules.png)

Look at tempSensor module logs, you will see telemetry being sent to the cloud

```linux
iotedge logs tempsensor
```

![telemetry](/edgemodule/images/10_edge_telemetry.png)

 **Note**: tempsensor module will stop sending messages after 500 messages have been sent. You can restart it using the following command:

    ```shell
    iotedge restart tempsensor
    ```