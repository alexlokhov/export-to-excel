# 'Export to Excel' plugin for Tableau Server
Use this plugin to export data from multiple views in a single dashboard. The plugin generates an Excel file with multiple tabs; each tab contains data from a different view.

![alt text](https://user-images.githubusercontent.com/9513594/27134313-1c2b71be-510d-11e7-8440-9348ad9e3d12.gif "Export to Excel demo")

### How to install it
* Download xlsx_exporter.html
* Publish it as a web data connector to your Tableau Server:
   ```
   tabadmin import_webdataconnector xlsx_exporter.html
   ```
   Note down the URL which was returned from the command. The URL should look like this:
   ```
   http://<your Tableau Server address>/webdataconnectors/xlsx_exporter.html  
   ```
   Once you have the URL you can test it in a browser. You should see an empty page with an 'Export to Excel' button:
![alt text](https://user-images.githubusercontent.com/9513594/27134333-28cfbfc4-510d-11e7-968a-e7802f7497cf.png "Web page test")

### How to use it
* When creating a dashboard embed a web page object using the URL of the published connector.
* Publish the dashboard to Tableau Server.

### How it works
The plugin uses JavaScript API to access data from the dashboard. In order to use JavaScript API without embedding, we  publish the page with the JavaScript code as a web data connector to Tableau Server. See http://databoss.starschema.net/auto-refresh-tableau-dashboard-without-embedding/ for a detailed explaination of this method.

The script iterates over *all* views in the current dashboard and uses `getSummaryDataAsync()` function to load aggregated data into the browser memory. Once the data is loaded, the Excel file is constructed on the client side by the browser.

### Known limitations
This method does not work with Tableau Online as Tableau Online does not permit publishing of customised web data connectors.
