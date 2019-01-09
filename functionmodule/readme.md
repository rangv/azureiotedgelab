## Build Azure Fucntion Module for Edge

### Install .NET Core

To create Azure Functions locally using Visual Studio Code you will need .NET Core. Complete the following steps to install .NET Core.

1. Open a browser and navigate to [.NET Downloads](https://dotnet.microsoft.com/download).

2. Select the **Windows** tab and click **Download .NET Core SDK**

    **Note**: We are using .NET Core **not** .NET Framework.

    Once the download has completed, continue.

3. Launch the downloaded Microsoft .NET Core installer and click **Install**.

    When the **User Access Control** prompt is displayed, click **Yes**.

4. Once the installation has completed, click **Close**.

5. Open a **Command prompt** and enter the following command:

    ```script
    dotnet --version
    ```

    You should see a response similar to:

    ```script
    Microsoft Windows [Version 10.0.18267.1001]
    (c) 2018 Microsoft Corporation. All rights reserved.

    C:\>dotnet --version
    2.2.100

    C:\>
    ```

You have now installed .NET Core.

#### Download Docker

In this task, you will install Docker on your Windows PC.

1. Before you begin, consider saving your work and closing application windows that you don't need at this time.

    Installing Docker and running it for the first time is likely to require one or more system reboots. We recommend saving your work and closing any apps that you don't really need to have open at this time.

2. Open a browser window, and review the Docker for Windows documentation [here](https://docs.docker.com/docker-for-windows/).

    Notice that this documentation page provides a link to system requirements.

3. Navigate to the Docker for Windows installation guide.

    You can open the link on the documentation page above, or use the link [here](https://docs.docker.com/docker-for-windows/install/).

4. On the **Install Docker for Windows page**, click **Download from Docker Store**.

5. On the **Docker Community Edition for Windows**, click **Please Login to Download**.

    If you have a docker username and password, jump down to **Install Docker** below, otherwise, continue to **Create a Docker Account**.

#### Create a Docker Account

1. On the **Welcome to Docker** page, click **Create Account**

2. On the account creation page, under **Choose a Docker ID**, enter a unique ID.

3. Under **Email**, enter the email you wish to use.

4. Under **Password**, enter a strong password.

5. Read the **Terms of Service** and, if you agree, select **I agree to Docker's Terms of Service**.

6. Read the **Privacy Policy and Data Processing Terms** and, if you agree, select **I agree to Docker's Privacy Policy and Data Processing Terms**.

7. If you desire to receive email from Docker, select **I would like to receive email updates from Docker, including its various services and products**.

8. Complete the **I am not a robot** captcha.

9. Check you email and click on the email verification link.

Now you have created and verified an account, return to the login page.

#### Install Docker

1. On the **Welcome to Docker** page, enter your username and password, the click **Login**.

2. On the **Docker Community Edition for Windows**, click **Get Docker**.

3. Once the **Docker for Windows Installer** download has completed, click **Run** (if you aren't prompted to run, find the downloaded installer and run it).

    If a Windows **User Account Control** prompt is displayed, click **Yes**.

    The Docker for Windows installer will then download and install the necessary components.

4. In the **Installing Docker for Windows** window, on the **Configuration** pane, ensure **Use Windows containers...** is not selected, then click **Ok**.

    The installer will then unpack files.

5. Once installation has completed, click **Close and logout**.

    Docker will create a shortcut on the Desktop, or it can be found in the Start menu.

6. Log back in and Run Docker for Windows.

    The first launch may take a few minutes.

    The whale icon in the notification area indicates that Docker is running, and accessible from a terminal. If the whale is hidden in the Notifications area, click the up arrow on the taskbar to show it. 

#### Verify Installation

We can run a few simple docker commands to verify that it is installed correctly.

1. Open the Windows **Start** menu, search for **cmd** and launch it.

2. In the **Command Prompt** window, enter the following:

    ```command
    docker --version
    ```

    Verify that a version is displayed.

### Create Azure Container Registry

In this section, we are going to use the Azure Portal to create a Azure Container Registry (ACR).

1. Open a browser and navigate to [Azure Portal](https://portal.azure.com)

2. Click on **Create a Resource** -> **Containers** -> **Container Registry**

    ![Azure Portal](images/01createcontainerregistry.png)

3. Provide a unique name to your container registry, enable admin user and click **Create**

    ![Create Container Registry](images/02createcontainerregistry.png)

4. Once your registry is created go to resource for details

    ![Registry Overview](images/03registryoverview.png)



### Create a Function Project

The Azure IoT Edge extension for Visual Studio Code that you installed provides management capabilities as well as some code templates. You will use Visual Studio Code to create an IoT Edge solution that contains an Azure function.

1. In Visual Studio Code, open the Command Palette by pressing **CONTROL + SHIFT + P** and enter **Azure IoT Edge: New**.

    Choose **Azure IoT Edge: New IoT Edge Solution**.

2. A **Choose Folder** window will open, choose the location where you wish to create the solution.

3. In Visual Studio Code, under **Provide a Solution Name**, enter **EdgeFunction**.

4. Under **Select Module Template**, select **Azure Functions - C#**.

5. Under **Provide a Module Name**, enter **FilterFunction**.

6. Under **Provide Docker image repository for the module**, replace the value with the following:

    ```shell
    [registry name].azurecr.io/filterfunction
    ```

    Replace `[registry name]` with the registry name you created earlier. 

    **Note**: the repository name must be lowercase

7. In the VS Code explorer, open **modules > FilterFunction > FilterFunction.cs**.

8. Replace the contents of the **FilterFunction.cs** file with the following code:

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.Azure.Devices.Client;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Extensions.EdgeHub;
    using Microsoft.Azure.WebJobs.Host;
    using Microsoft.Extensions.Logging;
    using Newtonsoft.Json;

    namespace Functions.Samples
    {
        public static class FilterFunction
        {
            [FunctionName("FilterFunction")]
            public static async Task FilterMessageAndSendMessage(
                [EdgeHubTrigger("input1")] Message messageReceived,
                [EdgeHub(OutputName = "output1")] IAsyncCollector<Message> output,
                ILogger logger)
            {
                const int temperatureThreshold = 20;
                byte[] messageBytes = messageReceived.GetBytes();
                var messageString = System.Text.Encoding.UTF8.GetString(messageBytes);

                if (!string.IsNullOrEmpty(messageString))
                {
                    logger.LogInformation("Info: Received one non-empty message");
                    // Get the body of the message and deserialize it.
                    var messageBody = JsonConvert.DeserializeObject<MessageBody>(messageString);

                    if (messageBody != null && messageBody.machine.temperature > temperatureThreshold)
                    {
                        // Send the message to the output as the temperature value is greater than the threshold.
                        var filteredMessage = new Message(messageBytes);
                        // Copy the properties of the original message into the new Message object.
                        foreach (KeyValuePair<string, string> prop in messageReceived.Properties)
                        {filteredMessage.Properties.Add(prop.Key, prop.Value);}
                        // Add a new property to the message to indicate it is an alert.
                        filteredMessage.Properties.Add("MessageType", "Alert");
                        // Send the message.
                        await output.AddAsync(filteredMessage);
                        logger.LogInformation("Info: Received and transferred a message with temperature above the threshold");
                    }
                }
            }
        }
        //Define the expected schema for the body of incoming messages.
        class MessageBody
        {
            public Machine machine {get; set;}
            public Ambient ambient {get; set;}
            public string timeCreated {get; set;}
        }
        class Machine
        {
            public double temperature {get; set;}
            public double pressure {get; set;}
        }
        class Ambient
        {
            public double temperature {get; set;}
            public int humidity {get; set;}
        }
    }
    ```

9. Save the changes to the of the **FilterFunction.cs** file.

10. Open the VS Code integrated terminal by selecting View > Terminal.

11. Sign in to your container registry by entering the following command in the integrated terminal. 

    Use the username and login server that you copied from your Azure container registry earlier.

    ```shell
    docker login -u <ACR username> <ACR login server>
    ```

    When you are prompted for the password, paste the password for your container registry and press Enter.

    ```shell
    Password: <paste in the ACR password and press enter>
    Login Succeeded
    ```

    Hit **ENTER** to submit the password.

12. In the VS Code explorer, open the **deployment.template.json** file in your IoT Edge solution workspace.

    This file tells the IoT Edge runtime which modules to deploy to a device. Notice that your Function module, **FilterFunction** is listed along with the **tempsensor** module we deployed in an earlier task, that provides test data.

    If you scroll down to line 86, you will see a definition for the routes on the IoTEdge module:

    ```json 
    {
        "routes": {
        "telemetryToCloud": "FROM /messages/modules/tempsensor/* INTO $upstream",
        "alertsToCloud": "FROM /messages/modules/StreamAnalyticsJob/* INTO $upstream",
        "alertsToReset": "FROM /messages/modules/StreamAnalyticsJob/* INTO BrokeredEndpoint(\"/modules/tempsensor/inputs/control\")",
        "telemetryToAsa": "FROM /messages/modules/tempsensor/* INTO BrokeredEndpoint(\"/modules/StreamAnalyticsJob/inputs/temperature\")",
        "FilterFunctionToIoTHub": "FROM /messages/modules/FilterFunction/outputs/* INTO $upstream",
        "sensorToFilterFunction": "FROM /messages/modules/tempsensor/outputs/temperatureOutput INTO BrokeredEndpoint(\"/modules/FilterFunction/inputs/input1\")"
        }
    }
    ```

    This replaces the existing route which takes the output of the **tempsensor** module and sends it to **\$upstream** (which is the IoT Hub in the cloud). The new routes take the output of **tempsensor** and routes it to the **FilterFunction** and then takes the output from **FilterFunction** and routes it to **$upstream** .

13. Open the **.env** file in your IoT Edge solution workspace. 

    This git-ignored file stores your container registry credentials so that you don't have to put them in the deployment manifest template. Provide the username and password for your container registry.

14. In the **.env** file, provide the username and password for the Azure Container Registry.

15. Save the changes to the **.env** file.

16. In the VS Code explorer, right-click the **deployment.template.json** file and select **Build and Push IoT Edge solution**.

    When you tell Visual Studio Code to build your solution, it first takes the information in the deployment template and generates a deployment.json file in a new folder named config. Then it runs two commands in the integrated terminal: docker build and docker push. These two commands build your code, containerize the functions, and then push the code to the container registry that you specified when you initialized the solution.

    You will see a lot of output generated during the process.

### View your Container Image

Visual Studio Code outputs a success message when your container image is pushed to your container registry. If you want to confirm the successful operation for yourself, you can view the image in the registry.

1. In a browser, open the Azure Portal [https://portal.azure.com](https://portal.azure.com).

    Login using your Azure Subscription if required.

2. In the **Search resources, services, and docs**, enter the name of the ACR  you created earlier, and then select it from the displayed list.

3. In the left hand nav area of the **Container registry** blade, under **Services**, click **Repositories**.

    You should see the **filterfunction** repository in the list.

4. In the list of repositories, click **filterfunction**.

    The **Repository** blade will open. In the Tags section, you should see the **0.0.1-amd64** tag. This tag indicates the version and platform of the image that you built. These values are set in the **module.json** file in the FilterFunction folder.

### Deploy and Run the Solution

You can use the Azure portal to deploy your function module to an IoT Edge device like you did in the quickstarts. You can also deploy and monitor modules from within Visual Studio Code. The following sections use the Azure IoT Edge extension for VS Code that was listed in the prerequisites. Install the extension now, if you didn't already.

1. In Visual Studio Code, open the Command Palette by pressing **CONTROL + SHIFT + P** and enter **Azure: Sign in**

    In the filtered list of commands, select **Azure: Sign in**.

    A notification will appear.

2. On the notification, click **Copy & Open**.

    A code will be copied into the clipboard and a web browser will open and display the login page.

3. In the web browser, under **Code**, paste the device code.

    The web page will automatically check the code and will determin that Visual Studio Code is the source.

4. On the web page, click **Continue** and login to Azure.

    Once the login succeeds, you may close the web page. Visual Studio Code is now logged in. You will see a message in the Visual Studio Code statusbar `Azure: <your username>`. 

5. In Visual Studio Code, open the Command Palette by pressing **CONTROL + SHIFT + P** and enter **Azure IoT Hub: Select IoT Hub**.

6. Select the subscription that has your IoT hub.

7. Select the IoT hub that you want to access.

8. In the VS Code explorer, expand the Azure IoT Hub Devices section.

9. Right-click the name of your IoT Edge device, and then click **Create Deployment for single device**.

10. In the **Open** dialog, browse to the solution folder that contains the CSharpFunction. 

11. Open the **config** folder, select the **deployment.amd64.json** file and then click **Select Edge Deployment Manifest**.

12. Refresh the **Azure IoT Hub Devices** section. You should see the new `FilterFunction` running along with the `tempsensor` module and the `$edgeAgent` and `$edgeHub`.

    It may take a few moments for the new modules to show up. Your IoT Edge device has to retrieve its new deployment information from IoT Hub, start the new containers, and then report the status back to IoT Hub.

13. To see all of the messages that arrive at your IoT hub, open the Command Palette by pressing **CONTROL + SHIFT + P** and enter **Azure IoT Hub: Start Monitoring D2C Message**.

14. To filter the view to see all of the messages that arrive at your IoT hub from a specific device, right-click the device in the Azure IoT Hub Devices section and select **Start Monitoring D2C Messages**.

15. To stop monitoring messages, open the Command Palette by pressing **CONTROL + SHIFT + P** and enter **Azure IoT Hub: Stop monitoring D2C message**.
