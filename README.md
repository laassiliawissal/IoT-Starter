# IoT-Starter
This tutorial walks you through simulating an IoT device, gathering data in the Watson IoT Platform, exploring data and creating visualizations.

# Objectives:
  - Set up IoT Simulator.
  - Send collection data to Watson IoT Platform.
  - Create visualizations.
# Services used
This tutorial uses the following runtimes and services:

- IBM Watson™ IoT Platform
- Node RED
- IBM Cloudant  

# 1. Create a Free Ibm Cloud Account :
click bellow to create an ibm cloud account https://ibm.biz/BdzE6G 
you will need a valid email adress so that you can confirm you registration.

# 2. Create the Internet of Things Platform Starter (and connect to a virtual sensor)

In this first section, you'll deploy the Internet of Things Platform Starter in IBM Cloud, which is a boilerplate application, and connect it to a virtual sensor on a web page.

Log into IBM Cloud https://ibm.biz/BdzE6G and click Catalog > Starter Kits > Internet of Things Platform Starter. Enter a name and host for your application. Both names must be unique. Then, click Create.

After the application launches, click Visit App URL and then on go to the Node-RED flow editor. Answer the prompts in the Node-RED editor to secure it. Click Go to your Node-RED flow editor.

Click the plus icon to add a new flow, double click and rename it Smart House. from github repository, copy flow1.txt into your clipboard. Go back to the NodeRed flow Editor and Click on hamburger menu on the left->import->clipboard -> paste flow1 that you copied. 

now you 'll be able to see this basic flow.
{image}

# 3. Simulate sensors data : 

After you start your Internet of Things Platform Starter instance, open the temperature and humidity sensor simulator, from ibm.biz/iotsensor, so that you can connect it to the IBM IoT app.

Copy the device id value in the upper-right corner of the virtual sensor. In this example, the value is a547824b3b3e.

In the flow editor, double-click the 'IBM IoT Sensor Data In' node.

Paste the ID of the sensor into 'Device Id' field and choose Quick Start into the 'Authentication' field. Click 'Done' and then click 'deploy' button in the upper-right corner to deploy the flow.
{image}

Go to the virtual sensor and increase the temperature to 41° C or more. in the debug pane you'll see the increased value of temperature.

(# 4. Create the flow : 
get temprature and humidity data from sensors send it to the Ibm IoT platform then add it into a database.

to get the flow import "flow1" into your Node RED workspace 

verify that the data is added into cloudant!)

# 4. Store Sensor Data into Cloudant: 
In the Node-RED flow Editor, click on filter nodes on the left, and look for Cloudant, choose the one with output property, drag and drop into the your flow. I've already done it for you, now, double click on Cloudant and pick a database name "smarthousedb".

To verify that the data have been added correctly, Go back to the ibm dashboard -> cloud Foundary Apps -> your app name -> connections -> select the cloudant db connected to your app name -> click on the alias on the top-right-> click on lunch db dashboard -> click on the database icon -> click on your database name -> you should see your sensor data added succesfully.

{image}

# 5. Gather and Visualize Sensor Data into IBM IoT Platform:
  ## 5.1. Lunch ibm IoT Platform
  Go back to the ibm dashboard -> cloud Foundary Apps -> your app name -> connections -> select the IoT Platform within the App -> Click on lunch button.
  {image}
  
  5.2. create device type
  From the IoT Platform homepage select Add Device Type -> choose Device -> give a name -> click -> next -> Done.
  {}
  
  5.3. create device
  From the IoT Platform HomePage click on Browse menu -> click on Add Device -> Select Device type you just created -> give a device ID -> add Authentification Token -> Done
  
  5.4. Send Data to your New Created Device
  Copy your device Id and Device type, and Go back to Node-Red Flow Editor, doucle click on 'Send temp sensor data to IBM IoT Platform'    node and update the node info :
  
   Authentication: Bluemix Service
   Output Type: Device Event
   Device Type: 'device type you added in IoT Platform'
   Device Id: 'device id you added in IoT Platform'
   Event Type: event1
   Format: json
   Data: temp:10
   
   after updating click deploy, lets Make sure sensor data is sent to Ibm IoT platformand, Go back to the IoT Platform -> Browse Devices -> Click on your Device name -> Recent Events, you should be able to see your temprature sensor data :
   {image}
    
  5.5. create Dashboar 
  Now, click on the Broard icon -> create New Board -> Name it smart house -> Click on Add new Card Button -> choose a chart type 'Gauge' for expl -> select your device from the device list -> add new dataset.
  data set refer to an important information :
  - Event : is the same we just added 'event1'
  - Property : is the the variable we want to display in the Gauge here is 'temp'
  
  {image function}
  
  - Type : is the type of this property her is 'Number'
 
  {data set info}
  

  
# 6. Step furthur:
  - analyze sensore data in watson studio
  - Add watson services into NodeRed Flow
