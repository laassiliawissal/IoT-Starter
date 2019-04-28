# IoT-Starter
This tutorial walks you through simulating an IoT device, gathering data in the Watson IoT Platform, exploring data and creating visualizations.

# Objectives:
  - Set up IoT Simulator.
  - Send collection data to Watson IoT Platform.
  - Create visualizations.
  
# 1. Create a Free Ibm Cloud Account :
click bellow to create an ibm cloud account https://ibm.biz/BdzE6G 

# Services used
This tutorial uses the following runtimes and services:

- IBM Watson™ IoT Platform
- Node RED
- IBM Cloudant

# Architecture

  - Devices send sensor data to IBM Watson IoT Platform using MQTT protocol
  - Historical data is exported into a IBM Cloudant database
  - sensor data are displayed in a dashboard

# 2. Create an IoT Platform Starter Kit:

1. Create the Internet of Things Platform Starter and connect to a virtual sensor
In this first section, you'll deploy the Internet of Things Platform Starter in IBM Cloud, which is a boilerplate application, and connect it to a virtual sensor on a web page. You don't need your Raspberry Pi device for this section.

Log into IBM Cloud and click Catalog > Starter Kits > Internet of Things Platform Starter. Enter a name and host for your application. Both names must be unique. Then, click Create.

After the application launches, click Visit App URL and then on go to the Node-RED flow editor. Answer the prompts in the Node-RED editor to secure it. Click Go to your Node-RED flow editor.

You should see Flow 1 running on IBM Cloud with a virtual thermometer. For now, you'll work with the Temperature Monitor flow (second flow):

# 3. Simulate sensors data : 

After you start your Internet of Things Platform Starter instance, open the temperature simulator so that you can connect it to the IBM IoT app In node as shown in blue in Flow 1:

Copy the value in the upper-right corner of the virtual thermometer. In this example, the value is 03075c7af9d9.

In the flow editor, double-click the IBM IoT App In node.

Paste the ID of the sensor into Device Id field. Click Done and then deploy the flow.

Go to the virtual sensor and increase the temperature to 41° C or more.

In the flow editor, note that the flow has three green output debug nodes that show flow data in the debug pane.

Disconnect the top green Debug output payload node in the top flow by clicking the connecting line and pressing Delete on your keyboard. Disconnect the device data node on the bottom flow as shown in the following image. Then, click Deploy.

You might need to scroll down in the debug pane to see the simplified view of temperatures.

 
# 4. Create the flow : 
get temprature and humidity data from sensors send it to the Ibm IoT platform then add it into a database.

to get the flow import "flow1" into your Node RED workspace 

verify that the data is added into cloudant
# 5. Gather and Visualize Sensor Data:
  # 5.1. Lunch ibm ito platform
  # 5.2. create device type
  # 5.2. create device type
  
# 6. Step furthur:
  - analyze sensore data in watson studio
  - Add watson services into NodeRed Flow
