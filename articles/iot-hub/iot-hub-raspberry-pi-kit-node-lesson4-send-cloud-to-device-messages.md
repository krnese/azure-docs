---
title: Run the sample application to receive cloud-to-device messages | Microsoft Docs
description: The sample application runs on Pi and monitors incoming messages from your IoT hub. A new gulp task sends messages to Pi from your IoT hub to blink the LED.
services: iot-hub
documentationcenter: ''
author: shizn
manager: timlt
tags: ''
keywords: 'cloud to device, message from cloud'

ms.assetid: 6ae6539e-1163-4490-8d72-fdf7803e3054
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/28/2016
ms.author: xshi

---
# Run the sample application to receive cloud-to-device messages
In this article, you deploy a sample application on Raspberry Pi 3. The sample application monitors incoming messages from your IoT hub. You also run a gulp task on your computer to send messages to Pi from your IoT hub. When the sample application receives the messages, it blinks the LED. If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## What you will do
* Connect the sample application to your IoT hub.
* Deploy and run the sample application.
* Send messages from your IoT hub to Pi to blink the LED.

## What you will learn
In this article, you will learn:
* How to monitor incoming messages from your IoT hub
* How to send cloud-to-device messages from your IoT hub to Pi.

## What you need
* Raspberry Pi 3, set up for use. To learn how to set up Pi, see [Configure your device](iot-hub-raspberry-pi-kit-node-lesson1-configure-your-device.md).
* An IoT hub that is created in your Azure subscription. To learn how to create your IoT hub, see [Create your IoT hub and register Raspberry Pi 3](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md).

## Connect the sample application to your IoT hub
1. Make sure that you're in the repo folder `iot-hub-node-raspberrypi-getting-started`. Open the sample application in Visual Studio Code by running the following commands:
   
   ```bash
   cd Lesson4
   code .
   ```
   
   Notice the `app.js` file in the `app` subfolder. The `app.js` file is the key source file that contains the code to monitor incoming messages from the IoT hub. The `blinkLED` function blinks the LED.
   
   ![Repo structure in the sample application](media/iot-hub-raspberry-pi-lessons/lesson4/repo_structure.png)
2. Initialize the configuration file by using the following commands:
   
   ```bash
   npm install
   gulp init
   ```
   
   If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on this computer, all the configurations are inherited, so you can skip to the task of deploying and running the sample application. If you completed the steps in [Create an Azure function app and storage account](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md) on a different computer, you need to replace the placeholders in the `config-raspberrypi.json` file. The `config-raspberrypi.json` file is in the subfolder of your home folder.
   
   ![Contents of the config-raspberrypi.json file](media/iot-hub-raspberry-pi-lessons/lesson4/config_raspberrypi.png)

* Replace **[device hostname or IP address]** with the IP address of Pi or the host name that you get by running the `devdisco list --eth` command.
* Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id} -g iot-sample {resource group name}` command.
* Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name} -g iot-sample {resource group name}` command.

> [!NOTE]
> Run **gulp install-tools** as well, if you haven't done it in Lesson 1.

## Deploy and run the sample application
Deploy and run the sample application on Pi by running the following command:

```bash
gulp deploy && gulp run
```

The command deploys the sample application to Pi. Then, it runs the application on Pi and a separate task on your host computer to send 20 blink messages to Pi from your IoT hub.

After the sample application runs, it starts listening to messages from your IoT hub. Meanwhile, the gulp task sends several "blink" messages from your IoT hub to Pi. For each blink message that Pi receives, the sample application calls the `blinkLED` function to blink the LED.

You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to Pi. The last one is a "stop" message that tells the application to stop running.

![Sample application with gulp command and blink messages](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_blink.png)

## Summary
You’ve successfully sent messages from your IoT hub to Pi to blink the LED. The next task is optional: change the on and off behavior of the LED.

## Next steps
[Change the on and off behavior of the LED](iot-hub-raspberry-pi-kit-node-lesson4-change-led-behavior.md)

