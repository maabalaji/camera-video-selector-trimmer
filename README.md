# Instagram like Assests Picker + Video Trim + Thumbnail Picker iOS
Library (Photo + Video) & Capture (Photo + Video)
Minimum iOS 9.0 & above. <br />

* Sample Preview <br />
![Alt Text](https://github.com/anoop-sharma/camera-video-selector-trimmer/blob/master/working.gif)

To test kindly download the example and run videoPlugin.xcworkspace under platform -> ios section. <br />

Resource plugin list : <br />
1) cordova-plugin-camera-preview <br />
2) cordova-plugin-photo-library <br />
3) cordova-plugin-video-editor <br />
4) cordova-plugin-instagram-assets-picker <br />

To integrate with your project , download the resource plugins & replace their exsiting files with our files after successfully building ios project.

# Steps to Implement
1) Run a camera session.
```
CameraPreview.startCamera(options, function() {
        console.log('successCamera')
    }, function(error) { 
        alert(error) }
);    
```
2) Load / Intialise the Device Library.
```
InstagramAssetsPicker.getMedia(
            function(result) { // success cb
                console.log('getMedia success, result: ', JSON.stringify(result, null, 2));
            },
            function(err) { // error cb
                console.log('getMedia error, err: ', err);
            }, { // options
                type: 'all', // accepts 'photo', 'video', or 'all' - defaults to all
                cropAfterSelect: false, // see the note above for when this is false - defaults to false
                showGrid: false // determines whether to show the grid for cropping - defaults to false
            }
        );
```
3) Add Capture Function for image capture.
```
CameraPreview.takePicture({ width: 640, height: 640, quality: 85, type: 1 }, function(pictureSource) {
                imageSrcData = 'data:image/jpeg;base64,' + pictureSource;
            }, function(error) { alert(error) });
```
4) Recording Start / Stop Instance for Video Recording.
```
CameraPreview.takePicture({ width: 640, height: 640, quality: 85, type: 2 }, function(videoSource) {
                // alert(videoSource);
            }, function(error) { alert(error) });

toggle same function for start & stop recording.
```
5) After selecting a video / recording a video Trim video into 20 sec with help of Video Slider & Trim video.
```
 VideoEditor.trim(
        trimSuccess,
        trimFail, {
            fileUri: // 'file-uri-here', // path to input video
            trimStart: 0, // time to start trimming in seconds
            trimEnd: 15, // time to end trimming in seconds
            outputFileName: 'ov' + Date.parse(new Date()), // output file name
            progress: function(info) {} // optional, see docs on progress
        }
    );
```
6) After Trim select a thumbnail from thumbnail slider.
```
VideoEditor.createThumbnail(
        success, // success cb
        error, // error cb
        {
            fileUri: // 'file-uri-here', // path to input video
            outputFileName: 'thumbnail-image' + Date.parse(new Date()), // output file name
            atTime: 10, // optional, location in the video to create the thumbnail (in seconds)
            width: 320, // optional, width of the thumbnail
            height: 480, // optional, height of the thumbnail
            quality: 100 // optional, quality of the thumbnail (between 1 and 100)
        }
    );
```
7) Output - Trim Video + Thumbnail Image for Video.
8) Optional - Switch camera view + flash mode (on/off).
```
 CameraPreview.getFlashMode(function(currentFlashMode) {
            var mode = currentFlashMode;
            if (mode == "on") {
                CameraPreview.setFlashMode(CameraPreview.FLASH_MODE.OFF);
            } else {
                CameraPreview.setFlashMode(CameraPreview.FLASH_MODE.ON);
            }
        });
```

* Reference for functions : index.js under www folder.

Thankyou,
Credits : http://www.terasoltechnologies.com/


