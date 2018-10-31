# netcool-NodeRed-Dashboard

This solution provides a jazzy real-time dashboard to the user community for understanding alert trending pattern in detail, health widgets at this monitoring dashboard will provide a over all health status and insight of alert catogries which contibuted more. 

Key at dashbaord
- Gauges for alert catogories
- Aggregate the top contibuted alerts
- Realtime graph of alarm count along with timeline

Alert normalization used is as mentioned below, before implementing please ensure whether this normalization is aplicable for target envionment. 
If not do replace at flow file with respective field before importing to node-red.

Node         - Server/Device name must be present
AlertKey     - Monitoring category 
AlertGroup   - Monitoring category 
TicketGroup  - ITSM tool Support group where ticket should go 
TicketNumber - ITSM tool ticket number
CILocation   - Configuration iteam location (Enrichment from extenal source) 
OSCatogory   - Configuration iteam OS information (Enrichment from extenal source)


Dashboard :
----------
 ![dashboard](dashboard.jpg)

## Implementation Steps:

### Step 1:Enable Http Interface at Object server
- To enable the interfaces, set the NRestOS.Enable property to TRUE.
- To configure the embedded HTTP server so that the interfaces are active on an HTTP port, specify the listening port for the connection type. For example, to make the interfaces listen on port 8080, set the properties as follows:

```
NHttpd.EnableHTTP : TRUE
NHttpd.ListeningPort : 8080

```
- If you want the interfaces to be active on an HTTPS port on 9090, set the properties that are shown in the following example. Because an HTTPS port is SSL encrypted, a certificate file that contains an appropriate certificate needs to be created and protected by a password.
```
NHttpd.SSLEnable : TRUE
NHttpd.SSLListeningPort : 9090
NHttpd.SSLCertificate : “certificatelabel”
NHttpd.SSLCertificatePwd : “password”

```
### Step 2:Install Node.js,node-red and node-red dashboard module at linux desktop/Server
- Below are the command sets to install reqired node-red platform to host this dashboard solution
```
curl --silent --location https://rpm.nodesource.com/setup_9.x | sudo bash -
yum install -y nodejs
yum install gcc-c++ make
/bin/npm install -g --unsafe-perm node-red
npm i node-red-dashboard --save
```

### Step 3:Securing Node-red dashboard
- There are couple of authentication mechanism avilable to make dashboard (1.http static id 2.twitter and git hub Oauth services) secure please reffer to below link to implemenet 
   https://nodered.org/docs/security 
   
### Step 4:Import the dashboardFlow.json
- Login to the flow editor using url https://localhost:1880/red 
- import the dashboardFlow.json using option avilable at top right corner
- once imported flow will look like content at below picture

  #### Flow post import on node-red flow editor :
     ![flow](flow.jpg)
- Edit the [NetcoolObjectServer Query] Node to feed in Netcool omnibus Http access url and cerentials.
  (please do verfiy from browser before feed data to this while accessing it must return a object server alert data on browser)
  
  ### Step 5:Accessging dashboard
  - you can access the dashboard via url http://localhost:1880/ui/#/0
  
## Production Senarios were this dashboard can be user
  
- lighter version solution to alert data visualization is in need
- Critical care application monitoring dashboard
- Command center single status console summary
