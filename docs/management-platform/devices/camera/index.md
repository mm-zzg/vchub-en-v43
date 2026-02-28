# Camera

WAGO SCADA supports integration with network cameras through standard protocols.The system establishes a connection with the camera via the **RTSP** protocol to obtain real-time surveillance footage. Based on the **Onvif**  protocol, it enables remote control of the camera's direction (PTZ) and zoom operations.

The user can bind the created Camera device via the [Camera](../../../2d-visualization/controls/display/camera.md)   control and view what the camera is monitoring on the page.

If you want to successfully manage and use camera devices, please first deploy the WebRTC Streamer service. For details, see [Deploying the WebRTC Streamer Service](deploy.md)   .

| **Note:** <br> **If the SCADA system is deployed in an public network environment (i.e., it is accessible from the internet) and you want to view the Camera device’s real-time video from outside, you need to deploy the Coturn NAT traversal service.**  <br> **For details, please refer to** [Play Camera Video From External Network](play.md). |
|-------------------------------------------|

#### **Creating a WebRTC Streamer**

1. Navigate to ”**Device”** ->" **Camera"** page, then click the **"Add WebRTC Streamer"** button.
2. On the Add page, enter the WebRTC Streamer information.

![alt text](1.png)

**Configuration Fields **

| **Name** | **Description**                                     |
|:----------|:-----------------------------------------------------|
| Name     | The name of the WebRTC Streamer device.             |
| Host     | The network address of the WebRTC Streamer service. |
| Port     | The port of the WebRTC Streamer service.            |

3. Click the **"OK"** button. The data will be displayed in the Camera list.

![alt text](2.png)

#### **Creating a Camera Device**

1. In the actions column of the created device, click the **"Add Camera"** button to add a Camera for the current device.
2. On the Add page, enter the camera information.

![alt text](3.png)

**Configuration Fields**

| **Name** | **Description**      |
|----------|----------------------|
| Name     | The name of the Camera.               |
| Onvif    | Currently, only basic PTZ functionality (pan, tilt, zoom) is supported. Ensure the camera supports the Onvif protocol.  | Host     | The network address of the Onvif service.                        | |----------|------------------------------------------------------------------| | Port     | The listening port of the Onvif service.                         | | Username | The authentication username for connecting to the Onvif service. | | Password | The authentication password for connecting to the Onvif service. |  Click the **"Test Onvif Connection"** button to verify if the Onvif service is accessible.       |
| RTSP     | RTSP (Real-Time Streaming Protocol) is a network protocol used to control the transmission of audio and video streams.  | RTSP     | The playback address of the camera's real-time video stream.   For details on RTSP addresses, refer to the RTSP protocol overview below. | |----------|------------------------------------------------------------------------------------------------------------------------------------------| | Username | The authentication username for connecting to the RTSP stream (if not included in the address).                                          | | Password | The authentication password for connecting to the RTSP stream (if not included in the address).                                          |  If the RTSP URL contains username and password information, but the user has also set a username and password in the respective fields, the username and password entered in the username and password fields will be used as the RTSP username and password.  ![alt text](4.png) |

3. Click the **"OK"** button. The data will appear in the sub-list under the corresponding WebRTC Streamer device.

![alt text](5.png)

###### **Onvif Protocol Overview**

**ONVIF** (Open Network Video Interface Forum) is a standardized protocol jointly developed by security industry manufacturers. It aims to achieve interoperability among network cameras, NVRs, access control systems, and other devices from different brands. 

By providing a unified interface specification, ONVIF addresses device compatibility issues and supports functionalities such as device discovery, configuration management, real-time streaming, and PTZ control.

###### **RTSP Protocol Overview**

RTSP (Real Time Streaming Protocol) is a network protocol used for real-time streaming media delivery.An RTSP address is typically used to specify the location of a video or audio stream.The format of an RTSP address can vary depending on the situation, but usually follows some common rules.

The following is an example of a typical RTSP address:

```bash
rtsp://username:password@hostname:port/path
```
 
- `rtsp://`: indicates the protocol, Real Time Streaming Protocol.
- `username:password`: indicates the username and password used to access the stream. This part is optional and can be omitted if the stream does not require authentication.
- `hostname`: the hostname or IP address of the streaming server.
- `port`: the port number of the streaming server. The default RTSP port is 554.
- `path`: the path or identifier of the stream.

Here is a simple examples of how to resolve an RTSP address:

```bash
rtsp://admin:123456@192.168.1.100:554/live/stream1 //realtime
```
 
In this example:

- The protocol is RTSP.
- The username is admin and the password is 123456.
- The IP address of the server is 192.168.1.100.
- The port number of the server is 554.
- The path to the stream is /live/stream1.



**Notes:**  
- The exact format of the RTSP address may vary depending on the configuration of the streaming server and supported parameters. Some streaming servers may use other protocol prefixes, such as rtsps:// for RTSP over SSL (RTSP Secure Connection). 
- When using RTSP addresses, the format of the camera address may vary partially between brands, so please check the documentation of the corresponding brand to ensure that the address is parsed and used correctly! 

#### Application Scenarios

Although the WAGO SCADA system does not limit the number of camera devices, we do not recommend using it for CCTV security systems. Viewing multiple [Camera](../../../2d-visualization/controls/display/camera.md)   feeds simultaneously may result in significant bandwidth consumption, which could impact system performance.

The limitations on the number of monitored cameras are primarily influenced by two factors:

- **Number of Video Controls in the Browser**: The number of active video controls on the web browser is key factor. For example, opening 1  video control in 10 browsers is essentially equivalent in server bandwidth consumption to opening 10  video controls in a single browser.
- **Video Quality**: The resolution of the videos directly affects bandwidth usage. Video at 360p consumes considerably less bandwidth compared to streaming 4K video.

###### **Server Bandwidth Description (For Reference Only)**

| Parameter                             | Description              |
|:---------------------------------------|:--------------------------|
| Video Resolution                      | 1280 x 720 (HD, 720p)                                                                                                                |
| Video Frame Rate                      | 15 frames per second (common in surveillance video, suitable for low latency needs)                                                  |
| Video Encoding Format                 | H.264 (common in RTSP streams)                                                                                                       |
| Video Bitrate                         | 1024 kbps                                                                                                                            |
| Audio Bitrate (if applicable)         | 64 kbps                                                                                                                              |
| Total Bitrate                         | 1088 kbps (video + audio, ignore if no audio)                                                                                        |
| Server-side Traffic Consumption       | 1.5 MB/s (approximately 12 Mbps)                                                                                                     |
| Server Bandwidth Requirement          | 12 Mbps (for single user viewing)                                                                                                    |
| Audio Sampling Rate (if applicable)   | 16 kHz                                                                                                                               |
| Channel                               | Mono (surveillance videos are usually mono)                                                                                          |
| Network Latency                       | Low latency when network conditions are good                                                                                         |
| Concurrent User Bandwidth Requirement | Approximately 12 Mbps per user                                                                                                       |
| Total Bandwidth Calculation Example   | When 10 users are watching simultaneously, or one user is opening 10 videos at the same time, the server requires 120 Mbps bandwidth |

