# IoT-Starter
This tutorial walks you through simulating an IoT device, gathering data in the Watson IoT Platform, exploring data and creating visualizations, this is from one hand. From the other hand, it simulate a smart home, that can be able to warn you if there is a fire at home, it turns on/off you air-conditionner depending on the room temprature and can water you internal flower spots if it sense that spots have no Humidity.  

# Services used
This tutorial uses the following runtimes and services:

- IBM Watson IoT Platform
- Node RED
- IBM Cloudant
- [Simulated Sensors](ibm.biz/iotsensor) 

# 1. Create a Free Ibm Cloud Account :
Click bellow to create an [ibm cloud account](https://ibm.biz/BdzE6G ) you will need a valid email address so that you can confirm you registration.

# 2. Create the Internet of Things Platform Starter

In this first section, you'll deploy the Internet of Things Platform Starter in IBM Cloud, which is a boilerplate application, and connect it to a virtual sensor on a web page.

Log into [IBM Cloud](https://ibm.biz/BdzE6G ) and click Catalog > Starter Kits > Internet of Things Platform Starter. Enter a name and host for your application. Both names must be unique. Then, click Create.

![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/create%20iot%20nde%20red%20starter%20kit.png)
After the application launches, click Visit App URL -> go to the Node-RED flow editor. Answer the prompts in the Node-RED editor to secure it -> Click Go to your Node-RED flow editor.

![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/node%20red%20editor.png)

Click the plus icon to add a new flow, double click and rename it 'Smart House Basics'. from github repository, copy [basic flow.json](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/master/basic%20flow.json) into your clipboard. Go back to the NodeRed flow Editor and Click on hamburger menu on the left->import->clipboard -> paste flow1 that you copied. 

now you 'll be able to see this basic flow.

![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/debug%20data.png)

# 3. Simulate sensors data : 

After you start your Internet of Things Platform Starter instance, open the temperature and humidity [sensor simulator](ibm.biz/iotsensor), so that you can connect it to the IBM IoT app.

Copy the device id value in the upper-right corner of the virtual sensor. In this example, the value is a547824b3b3e.

![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/temp%20sensor.png)

In the flow editor, double-click the 'IBM IoT Sensor Data In' node.

Paste the ID of the sensor into 'Device Id' field and choose Quick Start into the 'Authentication' field. Click 'Done' and then click 'deploy' button in the upper-right corner to deploy the flow.

Go to the virtual sensor and increase the temperature to 41° C or more. in the debug pane you'll see the increased value of temperature.

# 4. Store Sensor Data into Cloudant: 
Now, double click on "Cloudant" node and pick a database name "smarthousedb".

To verify that the data have been added correctly, Go back to the ibm dashboard -> cloud Foundary Apps -> your app name -> connections -> select the cloudant db connected to your app name -> click on the alias on the top-right-> click on lunch db dashboard.

![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/app%20connection.png)

 after lunching the Dashboard -> click on the database icon -> click on your database name -> you should see your sensor data added succesfully, as shown in the image bellow.
 
![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/cloudant%20db%20smarthousedb%20data.png)

# 5. Gather and Visualize Sensor Data into IBM IoT Platform:
you can follow the steps bellow or you can follow this [tutorial](https://cloud.ibm.com/docs/tutorials?topic=solution-tutorials-gather-visualize-analyze-iot-data)
  ## 5.1. Lunch ibm IoT Platform
  Go back to the ibm dashboard -> cloud Foundary Apps -> your app name -> connections -> select the IoT Platform within the App -> Click on lunch button.
  
  ![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/ibm%20iot%20platform.png)
  
  ## 5.2. create device type
  From the IoT Platform homepage select Add Device Type menu -> choose Device -> give a name -> click -> next -> Done.
    
  ## 5.3. create device
  From the IoT Platform HomePage click on Browse menu -> click on Add Device -> Select Device type you just created -> give a device ID -> add Authentification Token -> Done
  
  ## 5.4. Send Data to your New Created Device
  Copy your device Id and Device type, and Go back to Node-Red Flow Editor, doucle click on 'Send temp sensor data to IBM IoT Platform'    node and update the node info :
  
   Authentication: Bluemix Service
   Output Type: Device Event
   Device Type: 'device type you added in IoT Platform'
   Device Id: 'device id you added in IoT Platform'
   Event Type: event1
   Format: json
   Data: temp:10
   
   ![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/info%20to%20out%20device.png)
   
   after updating click deploy, lets Make sure sensor data is sent to Ibm IoT platformand, Go back to the IoT Platform -> Browse Devices -> Click on your Device name -> Recent Events, you should be able to see your temprature sensor data :
   
   ![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/RecentEvent%20Right%20one.png)
    
  ## 5.5. create a Sensor Data Dashboard
  Now, click on the Broard icon -> create New Board -> Name it smart house -> Click on Add new Card Button -> choose a chart type  'Gauge' for expl -> select your device from the device list -> add new dataset.
  data set refer to an important information :
  - Event : is the same we just added 'event1'
  - Property : is the the variable we want to display in the Gauge here is 'temp'
  
  ![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/temp%20value%20or%20variable.png)
  
  - Type : is the type of this property here is 'Number'
 
  ![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/datasetinfo.png)
  
  After entering the dataset info click next -> Done, now you should be able to vusualise temp sensor data from your simulated device to Ibm IoT Platform.
  
  ![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/temp.png)

# 7. Advanced Smart room:
After we've learned the basics, let's create our simulated smart room that can be able to warn you if there is a fire at home, it turns on/off you air-conditionner depending on the room temprature and can water you internal flower spots if it sense that spots have no Humidity. In order to that follow these steps.
## 7.1. get the smart home flow
copy [smart house flows.json](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/master/smart%20house%20flows.json) into your clipboard and import to your Node-RED flow editor. you should see the flow in the image bellow:

![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/smart%20house%20simulation.png)

## 7.2. create new device types and devices into your Ibm IoT Platform
device type : 
- humidity
- thermostate
devices :
- humiditySensorRoom1
- humiditySensorRoom2
- tempSensorRoom1
- tempSensorRoom2
{}

## 7.3. Create new Cards into the Board section in IBM IoT Platform
Create more cards into the board you created to match the cards in the image bellow. pay attention to the Event and property, they should be the same in the IoT out node in flow2, the event in flow2 case is 'event' and the property change depending on the value you want to showcase in you Card.

![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/smart%20house%20temprature.png)
![alt text](https://github.com/wissallaassiliabouchama/IoT-Starter/blob/wissallaassiliabouchama-patch-1/smart%20house%20humidity.png)

# 6. What's next:
  - analyze sensore data in watson studio:
    + [Create a fun, simple IoT accelerometer game](https://developer.ibm.com/tutorials/iot-simple-iot-accelerometer-game/)
    + [Develop the IoT apps for a home automation system ](https://developer.ibm.com/tutorials/iot-smart-home-03/)
    + [Build a cognitive IoT app in just 7 steps ](https://developer.ibm.com/tutorials/iot-cognitive-iot-app-machine-learning/)
  
  - Add watson services into NodeRed Flow:
    + [Build a spoken universal translator using Node-RED and Watson AI services](https://developer.ibm.com/tutorials/build-universal-translator-nodered-watson-ai-services/)
