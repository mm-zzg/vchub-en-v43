# System.PTZControl.move


## Description
Get roles of the currently logged in user.

## Grammar

System.PTZControl.move(streamName: string,

cameraName: string,

operation: "Home" | "MoveUp" | "MoveDown" | "MoveLeft" | "MoveRight" | "ZoomIn" | "ZoomOut"

): Promise<void>

- Parameter

    streamName - The name of the WebRTC Streamer

    cameraName - The name of the camera

    operation - The PTZ control command. Possible values are:

         "Home" - Reset，

         "MoveUp" - Move up，

         “MoveDown” - Move down，

         “MoveLeft” - Move left，

         "MoveRight" - Move right，

         "ZoomIn" - Zoom in，

         “ZoomOut” - Zoom out  

- Return

    Nothing

## Code Example                                                                                                                                                                                                                                                                                                          
Displays the role of the currently logged in person on a  label.
```typescript 

const roles = System.Security.getRoles();
const label = await System.UI.findControl('Label1');
label.text = roles;
label.applyChanges();

```   