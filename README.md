# netcool-NodeRed-Dashboard

Apart from webgui widgets for those who need realtime monitoring of aggregation data can use this dashboard.

Advantages:- 
- Economic solution to alert data visualization.
- Dashboard serves as key for identifying anomalies 
- Provides insight on real-time alert data
- Portable to multiple platforms
- Easy to deploy at IBM Bluemix node-r

Dashboard :
----------
 ![flow](dashboard.jpg)

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

### Step 3:Install Node.js,node-red and node-red dashboard module at linux desktop/Server
### Step 4:Import the dashboardFlow.json
- Login to the flow editor using url https://localhost:1880/red 
- import the dashboardFlow.json using option avilable at top right corner
- once imported flow will look like below picture
  Flow post import on node-red flow editor :
  -----------------------------------------
     ![flow](flow.jpg)
- Edit the [NetcoolObjectServer Query] Node to feed in Netcool omnibus Http access url and cerentials
  (please do verfiy from browser before feed data to this while accessing it must return a object server alert data on browser)
  
