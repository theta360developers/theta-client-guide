# fake-theta

A limited simulation of the RICOH THETA API is available at
[https://fake-theta.vercel.app/](https://fake-theta.vercel.app/).

## Usage Examples

### info

```text
curl https://fake-theta.vercel.app/osc/info
{"api":["/osc/info","/osc/state","/osc/checkForUpdates","/osc/commands/execute","/osc/commands/status"],"apiLevel":[2],"_bluetoothMacAddress":"00:45:de:78:3e:33","endpoints":{"httpPort":80,"httpUpdatesPort":80},"firmwareVersion":"1.41.0","gps":false,"gyro":false,"manufacturer":"Ricoh Company, Ltd.","model":"RICOH THETA X","serialNumber":"10100001","supportUrl":"https://theta360.com/en/support/","uptime":67,"_wlanMacAddress":"00:45:78:bc:45:67"}
```

### state

Specify `POST` protocol.

```text
 curl -X POST https://fake-theta.vercel.app/osc/state
{"fingerprint":"FIG_0001","state":{"_apiVersion":2,"_batteryInsert":true,"batteryLevel":0.33,"_batteryState":"disconnect","_cameraError":[],"_captureStatus":"idle","_capturedPictures":0,"_currentMicrophone":"Internal","_currentStorage":"IN","_function":"normal","_latestFileUrl":"http://192.168.1.1/files/100RICOH/R0010015.JPG","_mySettingChanged":false,"_pluginRunning":false,"_pluginWebServer":false,"_recordableTime":0,"_recordedTime":0,"_storageID":"90014a68423861503e030277e0c2b500","storageUri":"http://192.168.1.1/files/"}}
```

### take picture

```text
curl -X POST  -H "Content-Type: application/json" -d "{\"name\
": \"camera.takePicture\"}" https://fake-theta.vercel.app/osc/commands/execute
{"id":"10","progress":{"completion":0},"name":"camera.takePicture","state":"inProgress"}
```

### emulate Z1

The default model is RICOH THETA X.  Switch to Z1 by adding this
to the header.

```text
emulating-theta-model:z1
```

Example:

```text
curl -H "emulating-theta-model:z1" https://fake-theta.vercel.app/osc/info
{"api":["/osc/info","/osc/state","/osc/checkForUpdates","/osc/commands/execute","/osc/commands/status"],"apiLevel":[2],"_bluetoothMacAddress":"00:45:de:78:3e:33","endpoints":{"httpPort":80,"httpUpdatesPort":80},"firmwareVersion":"2.20.3","gps":false,"gyro":true,"manufacturer":"RICOH","model":"RICOH THETA Z1","serialNumber":"10100001","supportUrl":"https://theta360.com/en/support/","uptime":67,"_wlanMacAddress":"00:45:78:bc:45:67"}
```

## Sample Media

Oppkey manages a separate community API server with sample media
from the RICOH THETA X. The physical device RICOH THETA has a HTTP server
inside the camera that provides a GET API endpoint for videos and images.

To simulate working with images, the Oppkey server provides links
to actual images from the RICOH THETA X. This only works when the camera
model is _x_, the default model.

The API endpoint for the Oppkey API simulation server is: [https://fake-theta-alpha.vercel.app]( https://fake-theta-alpha.vercel.app)

`camera.listFiles` and `state` are modified to show RICOH THETA X sample images. File name are R0010001 through R0010015.

### Request listFiles example

```javascript
{
  "name": "camera.listFiles", 
  "parameters": {
    "fileType": "image",
    "entryCount": 10,
    "maxThumbSize": 0
  }
}
```

### Example output of listFiles

```javascript
{
"results": {
  "entries": [
    {
      "dateTime": "2015:07:10 11:05:18",
      "_favorite": false,
      "fileUrl": "https://codetricity.github.io/fake-storage/files/100RICOH/R0010001.JPG",
      "isProcessed": true,
      "name": "R0010001.JPG",
      "previewUrl": "",
      "size": 4051440
    },
    {
      "dateTime": "2015:07:10 11:05:18",
      "_favorite": false,
      "fileUrl": "https://codetricity.github.io/fake-storage/files/100RICOH/R0010002.JPG",
      "isProcessed": true,
      "name": "R0010002.JPG",
      "previewUrl": "",
      "size": 4051440
    },
...
```

If you use an API tester such as Insomnia or Postman, you can easily
click on the URL to see the files.

![fake-theta list files](../images/fake_theta/fake-server-list-files.png)

The images are approximately 11MB.  There are no thumbnails.

![show image](../images/fake_theta/show_image.png)


## Using theta-client with fake-theta

![minimal theta-client](../images/fake_theta/minimal-theta-client.png)

1. specify endpoint   `final String endpoint = 'https://fake-theta-alpha.vercel.app';`
2. initial `ThetaClientFlutter()` with the endpoint `await _thetaClient.initialize(endpoint);`

```dart
class MiniApp extends StatefulWidget {
  const MiniApp({Key? key}) : super(key: key);

  @override
  State<MiniApp> createState() => _MiniAppState();
}

class _MiniAppState extends State<MiniApp> {
  final _thetaClient = ThetaClientFlutter();
  String _mobilePlatform = 'device unknown';
  String _cameraInfo = 'unable to get camera info';
  // real camera
  // final String endpoint = 'http://192.168.1.1:80/';
  // Oppkey fake camera
  final String endpoint = 'https://fake-theta-alpha.vercel.app';

  @override
  void initState() {
    super.initState();
    _initializeTheta();
  }

  void _initializeTheta() async {
    try {
      var mobilePlatform = await _thetaClient.getPlatformVersion();
      await _thetaClient.initialize(endpoint);
      var thetaInfo = await _thetaClient.getThetaInfo();
```