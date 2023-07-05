---
comments: true
---

# Fake THETA with React Native

## Overview

[Fake THETA](https://github.com/ricohapi/fake-theta) is an API based on the real
[RICOH THETA API](https://github.com/ricohapi/theta-api-specs/tree/main/theta-web-api-v2.1).
To use Fake THETA with React Native you can swap out the Real THETA Base URL `http://192.168.1.1` with the Fake THETA URL `https://fake-theta.vercel.app` for any commands. This can be useful to people who want to code the RICOH THETA Cameras without having the actual device or connecting to it.

![gifURL](../images/fake_theta/react_native/url.gif)

## Resources

- [Snack Browser Demo](https://snack.expo.dev/@airtechwick/github.com-airtechwick-theta-j-demo-start-erik?platform=android) - Runnable Mobile App Demo in the Browser

- [THETA JavaScript Examples](https://github.com/theta360developers/theta-javascript/tree/main/fake-theta) - Examples of how to code the RICOH THETA API in JavaScript

- [Fake THETA Documentation](https://github.com/ricohapi/fake-theta) - RICOH Documentation on Fake THETA

## Limitations of using Fake THETA

Limits are Specified in the Fake THETA [README.md](https://github.com/ricohapi/fake-theta/blob/main/README.md)

- Fake THETA only supports required parameters for each command execution basically

- Non-required parameters, except for \_detail of camera.listFiles command, are ignored in the current implementation

- Dynamic responses simulation according to internal states of the camera are not supported

- Completely-reproduced error responses for each model are not supported

- Parameter validation of APIs are not supported

- Non-required parameters for each command are not supported

## Info Example

[JS Example Code](https://github.com/theta360developers/theta-javascript/blob/main/fake-theta/protocols/info.js)

```javascript
export { infoButtonControl };

const infoButtonControl = async (urlEndpoint) => {
  console.log("info");
  const response = await fetch(`${urlEndpoint}info`, {
    method: "GET",
    headers: { "Content-Type": "application/json;charset=utf-8" },
  });
  const data = await response.json();
  return JSON.stringify(data, null, 4);
};
```

![gifInfo](../images/fake_theta/react_native/info.gif)

## State Example

[JS Example Code](https://github.com/theta360developers/theta-javascript/blob/main/fake-theta/protocols/state.js)

```javascript
export { stateButtonControl };

const stateButtonControl = async (urlEndpoint) => {
  const response = await fetch(`${urlEndpoint}state`, {
    method: "POST",
    headers: { "Content-Type": "application/json;charset=utf-8" },
  });

  const data = await response.json();
  return JSON.stringify(data, null, 4);
};
```

![gifState](../images/fake_theta/react_native/state.gif)

## Take Picture

[JS Example Code](https://github.com/theta360developers/theta-javascript/blob/main/fake-theta/commands/takePicture.js)

```javascript
export { takePictureButtonControl };

const takePictureButtonControl = async (urlEndpoint) => {
  const body = { name: "camera.takePicture" };
  const response = await fetch(`${urlEndpoint}commands/execute`, {
    method: "POST",
    body: JSON.stringify(body),
    headers: { "Content-Type": "application/json" },
  });
  const data = await response.json();

  return JSON.stringify(data, null, 4);
};
```

![gifTakePic](../images/fake_theta/react_native/takepic.gif)

## List Files

[JS Example Code](https://github.com/theta360developers/theta-javascript/blob/main/fake-theta/commands/listFiles.js)

```javascript
export { listFilesButtonControl };

const listFilesButtonControl = async (urlEndpoint) => {
  const body = {
    name: "camera.listFiles",
    parameters: {
      fileType: "all",
      entryCount: 5,
      maxThumbSize: 0,
    },
  };
  const response = await fetch(`${urlEndpoint}commands/execute`, {
    method: "POST",
    body: JSON.stringify(body),
    headers: { "Content-Type": "application/json" },
  });
  const data = await response.json();

  return JSON.stringify(data, null, 4);
};
```

![gifListFiles](../images/fake_theta/react_native/listfiles.gif)
