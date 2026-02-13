Used to display the video of the cameras configured in the **"Devices" -> "Camera"** list.

![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/ODbbH438wiKiYaQYZChscaWfGY2bYFpzBS0p1AqcB3Y.png)

**Properties**

| **Name**        | **Description**     |
|-----------------|--------------|
| Name            | The name of this control. |
| X               | The distance between the left side of the control and the left side of the canvas.         |
| Y               | The distance between the top of the control and the top of the canvas.     |
| W               | The width of the control.    |
| H               | The height of the control.      |
| Camera          | Select a Camera device for the control. This Camera  is created on the **"Devices"->"Camera"** page and supports dynamic binding.    |
| Enable PTZ      | When enabled, hovering the mouse over the control will display the PTZ (Pan-Tilt-Zoom) control panel. Ensure the bound camera has its Onvif service correctly configured.  It allows you to control the camera to rotate in the set direction, with one click resulting in one rotation.   | ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/K7WXLCSmJQk_aNrTxBWFQYA5H5Id0G3o9U2k6B7NnfM.png) | camera rotates upward | |---------------------------------------------------------------------------------------------------------------------------------------------|-----------------------| | ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/gbzeldWOe-_D5SqrGIU6cNU0dGBXDhVSAW0o6u_mMa8.png) | camera rotates down   | | ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/nuBPKQbjwAbqZoKeQObN1-5iSdsFYIpC3CbR6OXdcro.png) | Camera turns right    | | ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/eK6ElxWAbJuUX4TUTiy1D_aohWb37m1lhLSlf1PDdec.png) | Camera turns left     | | ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/yiBoPOtFpXP04wp2adeGB2QKOGLejVINAOt4iESojmM.png) | Reset the camera      | | ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/Gm7g104PoBPG3EGaZOzyQRZZhSmRJaRXwHYpgG8epkc.png) | Zoom in               | | ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/njAVwQpy8J7ZjnUEIhEpkYW4eSVktHwMDTyJMxdQocQ.png) | Zoom out              | |
| Enable Snapshot | When enabled, hovering the mouse over the control will display the screenshot button.  | ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/7n3fL6-qkncEk3mAeMOP2LiBWerPGETWst-fDyvs-To.png) | Click the button to save the current frame as an image. | |----------------------------------------------------------|                                       |
| View Coordinate | When enabled, hovering the mouse over the control will display the coordinate view button.  | ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/TpO5HeK6ws_GGMsHMWE1qVbsrwscvR4DZ6O0UBWyAi4.png) | Click the button to display the current coordinates of the camera. | |---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

**Event**

Allows you to perform specific events based on certain conditions. See the full description of each event on the[known-link]  page.

**Example**

View the real-time production status of workshop 1.

![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/71l5FOE6G8o4XmyQSW09QnmUQrLDzTQOz1fhwd5-IZw.png)

1. On the **"Devices"->"Camera"** page, create a new video name. See the[known-link]   for details .
2. Insert a "Camera" control on the page.
3. Set the camera for the control and select: **Streamer1/Workshop 1**.
4. Click the run button on the page to view the video.
5. Move the mouse over the control to display the operation buttons.

![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/6f4U66krp5qSnEeYFU04ii3hlH5U-Ioz-QK-EhCOas4.png)

| ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/Qnhrm-cFcTLZHqfQ_p8AnZu8s6AZM4Nxv6vUPcip_hg.png) | play button                                                       |
|---------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|
| ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/KiTpOrO50IJ3oXClII5VZNQpkyn9_iOTFAyMFM38MPM.png) | pause button                                                      |
| ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/b2JSIXaevpMBEc4nc_lVxpXy9FyBg-3NCpMpPOkW3JY.png) | Sound settings button                                             |
| ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/ZeonJJfY9nEvNMnJMlUmRnsAiLOtMj3PmjeACIE82gM.png) | full screen button                                                |
| ![img](https://docs.wagoscada.cn/wiki/api/wiki/external-editor/QHXVK91b/9rPAooNQ/resources/3jDP-5ZQojqyy5mOaM3mopR1FAARzbkLlmSn5diUaGo.png) | Picture-in-picture button, click to start picture-in-picture mode |

#### Autoplay policy

When a page link is opened directly, the video will not autoplay because the browser considers that there has been no interaction between the user and the domain  (click, tap, etc.). The user will need to manually click the play button.

In the following situations, browser allow autoplay with sound:

- The user has interacted with the domain (click, tap, etc.)；
- On desktop, the user's Media Engagement Index threshold has been crossed, meaning the user has previously played video with sound.
- The user has added the site to their home screen on mobile or installed the PWA on desktop.

For more details, please refer to the official website:  [https://developer.chrome.com/blog/autoplay?hl=zh-cn](https://developer.chrome.com/blog/autoplay?hl=zh-cn)