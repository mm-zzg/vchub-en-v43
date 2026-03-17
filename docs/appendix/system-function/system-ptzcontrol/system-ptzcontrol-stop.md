# System.PTZControl.stop

## Description
Stops the current movement operation of the PTZ camera.


## Grammar

System.PTZControl.stop(streamName: string,cameraName: string): Promise<void>
 - Parameter        
 streamName - The name of the WebRTC Streamer  
 cameraName - The name of the camera  
 - Return  Nothing 


## Code Example

Stop the movement operation of camera Camera1 of WebRTC Streamer Streamer1.

```typescript 
await System.PTZControl.stop("Streamer1","Camera1");

```