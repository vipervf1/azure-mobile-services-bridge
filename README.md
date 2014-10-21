azure-mobile-services-bridge
================

See the [component page](http://vipervf1.github.io/azure-mobile-services-bridge/components/azure-mobile-services-bridge/) for more information.

# Setup

Use bower to download the web component into your project

```
bower install --save azure-mobile-services-bridge
```

Import the web component into your page

```
<link rel="import" href="/bower_components/azure-mobile-services-bridge/azure-mobile-services-bridge.html">
```

Then use the web component by providing the app url and the app key

```
<azure-mobile-services-bridge appurl="https://api.azure-mobile.net/"
                           appkey="DNBjEutqGOCjnLfAdWhwWmAMBDxEbd50"
                           table="TableName">
</azure-mobile-services-bridge>
```
# Read Operations
## Simple Read
A simple read can be performed by using the component with all its defaults and supplying the auto flag so that it will execute right away

```
<azure-mobile-services-bridge appurl="https://api.azure-mobile.net/"
                           appkey="DNBjEutqGOCjnLfAdWhwWmAMBDxEbd50"
                           table="TableName"
                           auto></azure-mobile-services-bridge>
```

Like the ```core-ajax``` component, the response is in the event ```core-response``` and can be retrieved in the event details

```
ams.addEventListener("core-response",
  function (e) {
    var result = e.detail.response;
  }
);
```

Alternatively you can specify when the execution occurs by omitting the auto flag and calling ```go()``` on the component

```
var ams = document.querySelector("azure-mobile-services-bridge");
ams.go();
```

## Queried Read

Supply the azure ```where(...)``` query to the params property in the element using a json string

```
<azure-mobile-services-bridge appurl="https://api.azure-mobile.net/"
                           appkey="DNBjEutqGOCjnLfAdWhwWmAMBDxEbd50"
                           table="TableName"
                           params='{"col2":"test1-1"}'
                           auto></azure-mobile-services-bridge>
```

Or as a javascript object in the script section

```
var ams = document.querySelector("azure-mobile-services-bridge");
ams.params = { col2: "test1-1" };
ams.go();
```

# Insert Operations
```
<azure-mobile-services-bridge appurl="https://api.azure-mobile.net/"
                           appkey="DNBjEutqGOCjnLfAdWhwWmAMBDxEbd50"
                           table="TableName"
                           method="INSERT"
                           auto></azure-mobile-services-bridge>
```

Pass a java object with the columns and their data into the params property
```
var ams = document.querySelector("azure-mobile-services-bridge");
ams.params = { 
                col1: 'col1', 
                col2: 'col2' 
              };
ams.go();
```

The event ```core-response``` will contain the id of the newly created row
```
ams.addEventListener("core-response",
  function (e) {
    var result = e.detail.response.id;
  }
);
```

# Update Operations
```
<azure-mobile-services-bridge appurl="https://api.azure-mobile.net/"
                           appkey="DNBjEutqGOCjnLfAdWhwWmAMBDxEbd50"
                           table="TableName"
                           method="UPDATE"
                           auto></azure-mobile-services-bridge>
```

Pass a java object with the columns to update and the row id into the params property
```
var ams = document.querySelector("azure-mobile-services-bridge");
ams.params = {
               id: idToUpdate,
               text: newText
             };
ams.go();
```

# Delete Operations
```
<azure-mobile-services-bridge appurl="https://api.azure-mobile.net/"
                           appkey="DNBjEutqGOCjnLfAdWhwWmAMBDxEbd50"
                           table="TableName"
                           method="DELETE"
                           auto></azure-mobile-services-bridge>
```

Pass a java object with the row id to delete into the params property
```
var ams = document.querySelector("azure-mobile-services-bridge");
ams.params = {
               id: idToDelete
             };
ams.go();
```
