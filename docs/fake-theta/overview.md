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
