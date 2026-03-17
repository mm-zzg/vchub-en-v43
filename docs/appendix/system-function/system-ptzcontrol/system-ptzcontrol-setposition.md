# System.PTZControl.setPosition

## Description
Sets the absolute position of the PTZ camera.

## Grammar

**System.PTZControl.setPosition(streamName: string,cameraName: string,x: number,y: number,z: number): Promise<void>**

- Parameter

    streamName - The name of the WebRTC Streamer

    cameraName - The name of the camera

    x - The horizontal coordinate of the camera, range [-1, 1]

    y - The vertical coordinate of the camera, range [-1, 1]

    z - The zoom value of the camera, range [0, 1]

- Return

     Nothing



## Code Example

Set the camera Camera1 of WebRTC Streamer Streamer1 to horizontal coordinate -1, vertical coordinate -1, and zoom value 1.
```typescript
await System.PTZControl.("Streamer1","Camera1",-1,-1,1);
```