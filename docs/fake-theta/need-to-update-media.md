# Sample Media

Oppkey manages a separate community API server with sample media
from the RICOH THETA X. The physical device RICOH THETA has a HTTP server
inside the camera that provides a GET API endpoint for videos and images.

To simulate working with images, the Oppkey server provides links
to actual images from the RICOH THETA X. This only works when the camera
model is _x_, the default model.

The API endpoint for the Oppkey API simulation server is: [https://fake-theta-alpha.vercel.app]( https://fake-theta-alpha.vercel.app)

`camera.listFiles` and `state` are modified to show RICOH THETA X sample images. File name are R0010001 through R0010015.

## Request listFiles example

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

## Example output of listFiles

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
