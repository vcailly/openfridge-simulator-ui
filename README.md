# Openfridge UI (Node-RED Application)

This repository is an Node-RED application to simulate events from virtual appliances of the [openfridge](https://github.com/IBM/openfridge)  sample application.
With this Node-RED application you do not need to use the Paho or Mosquitto MQTT client for simulating events from the virtual devices, you can just do it from a web application.

It  can be deployed into Bluemix with only a couple of clicks. 

# Prerequisites

### 1- Deploy the openfridge sample Application

Follow the instructions provided at :

1. [Set up the Bluemix services (Cloudant, SendGrid, Watson IoT, and a Cloud Foundry app)](docs/BLUEMIX.md).
2. [Set up the OpenWhisk actions, triggers, and rules](docs/OPENWHISK.md).


#### 2- Once the openfridge sample Application deployed - update records for each device in  the CLOUDANT_APPLIANCE_DATABASE database of the Openfridge application

For each device you need to add a deviceId attribute wich contains the device ID (as defined on the IBM IoT platform) of the appliance 

```json
{
  "_id": "aaaabbbbcccc",
  "deviceId": "1",
  "serial": "aaaabbbbcccc",
  "warranty_expiration": 1467259200,
  "owner_name": "Vincent Cailly",
  "owner_email": "vcailly@example.com",
  "owner_phone": "18885551212"
}
```

**Important**: the email address specified here will be eventually used to receive email notifications by the OpenWhisk actions - make sure it is valid.

#### 3- Create a Cloudant instance for Node-RED

From the bluemix console or using the Bluemix CLI, create an instance of the Cloudant 
service, and call it `sample-node-red-cloudantNoSQLDB`. This is where your Node-RED 
instance will store its data.

**Remark:** If you want to change the name of this Cloudant instance, you must  update  `manifest.yml` accordingly.

# Deployment into Bluemix

You can easily deploy into bluemix by clicking on the following link:


[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/vcailly/openfridge-simulator-ui.git)

### How does this work?

When you click the button, you are taken to Bluemix where you get a pick a name
for your application at which point the platform takes over, grabs the code from
this repository and gets it deployed.

When you first access the application, you'll be asked to set some security options
to ensure your flow editor remains secure from unauthorised access.

# Configuration of the Node-Red flow with your own seetings from the Node-RED flow editor
Once the  `Openfridge UI` application deployed into bluemix you need to configure the `cloudant IN` an the 3 `MQTT OUT` nodes with your own settings  (server and credentials parameters for authentication to the cloudand and IoT platform services)

### For the `cloudant IN` node 

* Open the `cloudant IN` node

![Cloudant IN node](doc/cloudant_in.PNG)

* Click the Edit button of the Server attribute

![Server Attribute](doc/cloudant_in_step1.PNG)

 * Fill the fields with the credentials for the CLOUDANT_APPLIANCE_DATABASE database of the Openfridge application. Then click on UPDATE and Then DONE
![Credentials](doc/cloudant_in_step2.PNG)
   
    
### For the `MQTT OUT` node
