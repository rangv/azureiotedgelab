# Deploy Azure IoT Edge Enabled Linux VM

## Azure Market Place Offering

Use a preconfigured virtual machine to get started quickly, and easily automate and scale your IoT Edge testing.

This **Ubuntu Server 16.04 LTS** based virtual machine will install the latest Azure IoT Edge runtime and its dependencies on startup, and makes it easy to connect to your IoT Hub.

Connect this VM to your IoT Hub by setting the connection string with the run command feature (via Azure portal or command line interface) to execute:

```Linux
/etc/iotedge/configedge.sh  "<your_iothub_edge_connection_string>"
```

## Steps to Create VM

1. Click [here](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft_iot_edge.iot_edge_vm_ubuntu?tab=Overview) to deploy an Azure IoT Edge enabled Linux VM.

    ![Azure IoT Edge VM](/marketplacedeployment/images/01_marketplace_offering.png)

2. Click **Get It Now** button and click **Continue** on the browser
    ![Azure IoT Edge VM](/marketplacedeployment/images/02_get_it_now_continue.png)

3. Logs your into Azure portal. Click **Create** button
    ![Azure IoT Edge VM](/marketplacedeployment/images/03_create_vm.png)

4. Provide Subscription details and resource group. Also select password radio button and provide user and password to use later
    ![Azure IoT Edge VM](/marketplacedeployment/images/04_create_vm_details.png)

   Allow SSH ports by selecting the inbound ports radio button
    ![Azure IoT Edge VM](/marketplacedeployment/images/05_allow_ssh_port.png)

5. Validation process happens and a web page is presented. Click **Create** button.

6. Deployment completes in around 3 minutes.
    ![Azure IoT Edge VM](/marketplacedeployment/images/06_deployment_complete.png)

7. Click on **Go To Resource** button

8. Click on **Connect** button and copy the ssh command
    ![Azure IoT Edge VM](/marketplacedeployment/images/07_connect_ssh.png)

9. Click on **Cloud Shell icon**, opens a cloud shell on the browser. Copy the shh command and press enter
    ![Azure IoT Edge VM](/marketplacedeployment/images/08_cloud_shell_ssh.png)

    ```Linux
    ssh iotedgeadmin@<Your VM IP>
    ```
    Provide pasword and press **Enter**

10. Confirm Azure Edge Runtime is installed on the VM

    ```Linux
    iotedge version
    ```

    ![Azure IoT Edge VM](/marketplacedeployment/images/09_edge_version.png)
