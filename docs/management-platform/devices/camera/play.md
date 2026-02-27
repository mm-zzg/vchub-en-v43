# Play Camera Video From External Network

If you want to access the camera video over the Internet, deploying a Coturn traversal service can enable external access.Coturn is a free open source implementation of TURN and STUN Server. The TURN Server is a VoIP media traffic NAT traversal server and gateway.

- ***Coturn NAT traversal service only needs to be deployed when the SCADA system’s Camera component requires external network access***
- ***The server hosting the Coturn service must be able to access the internet and be accessible from the external network, with a fixed public IP address or domain name***
- ***Additionally, the firewall must allow TCP and UDP traffic on ports 3478, 3479, and 5349, as well as UDP traffic on ports 49152–65535***

#### Download Coturn

Official website:  [GitHub - coturn/coturn: coturn TURN server project](https://github.com/coturn/coturn)

#### Deploy Coturn

###### Docker

The following steps are based on Docker being already installed.

If Docker is not installed, please refer to the official documentation  [Install | Docker Docs](https://docs.docker.com/engine/install/)

**Method 1:** Use a Docker image

```bash
# Note: This method may fail to start the container on underperforming servers because it maps a large number of UDP ports. This can cause the port mapping process to hang or result in deployment failures
# -a -r {server machine's external IP or domain} -u {account}:{password}
docker run -d -p 3478:3478 -p 3478:3478/udp -p 5349:5349 -p 5349:5349/udp -p 49152-65535:49152-65535/udp coturn/coturn --log-file=stdout -v -a -r 122.254.123.122 -u admin:mm123456789
```
 
**Method 1:** Use the host network (recommended)

```bash
# This method will directly use the host’s network. Please ensure that the TCP and UDP ports 3478, 3479, and 5349 on the host remain free
# --min-port={min udp port} --max-port={max udp port} -a -r {server machine's external IP or domain} -u {account}:{password}
docker run -d --network=host coturn/coturn --log-file=stdout -v --min-port=49152 --max-port=65535 -a -r 122.254.123.122 -u admin:mm123456789
```
 
Note： [ Docker does not perform well with a large range of ports](https://github.com/instrumentisto/coturn-docker-image/issues/3).

##### Linux

```bash
# install coturn
apt install coturn
# start turn server
# turnserver --log-file=stdout -v --min-port={min udp port} --max-port={max udp port} -a -r {server machine's external IP or domain} -u {account}:{password}
turnserver --log-file=stdout -v --min-port=49152 --max-port=65535 -a -r 122.254.123.122 -u admin:mm123456789
```
 
The above method has a problem: when the server restarts or is unexpectedly disconnected, the service will shut down and not automatically restart. Therefore, we need to convert the service into a systemd service unit, which makes it easier to manage startup, restarts, and logs.

```bash
# install coturn
apt install coturn

# Enter the service unit folder
cd /etc/systemd/system

# Create a file named 'coturnservice.service' in the /etc/systemd/system directory, and enter the following content into the file.

[Unit]
Description=Coturn TURN Server
After=network.target

[Service]
Type=simple
# ExecStart=turnserver --min-port={min udp port} --max-port={max udp port} -a -r {server machine's external IP or domain} -u {account}:{password}
ExecStart=turnserver --min-port=49152 --max-port=65535 -a -r 122.254.123.122 -u admin:mm123456789
Restart=on-failure

[Install]
WantedBy=multi-user.target  

# After saving, enable and start the service.
sudo systemctl daemon-reload
sudo systemctl enable coturnservice
sudo systemctl start coturnservice
```
 
##### Window

The Coturn server currently does not have an official Windows version since its design and development are primarily aimed at Linux/Unix systems. If you want to deploy Coturn in a Windows environment, you have the following options:

1. Using Windows Subsystem for Linux (WSL)

   - Enable WSL on Windows 10 or Windows 11 and install a Linux distribution (e.g., Ubuntu). For details, please refer to Microsoft's official documentation:  [Install WSL](https://learn.microsoft.com/en-us/windows/wsl/install)
   - Please refer to the above **Linux** instructions for the remaining steps.
2. Using Docker for Windows

   - Please refer to the above **Docker** instructions.
#### How to Use?

After the Coturn server is deployed, we can use its configuration in WebRtc Streamer by attaching startup parameters when launching WebRtc Streamer. For example:

```bash
# Append parameters to the original startup command. -s "{server machine's external IP or domain}:3478" -t "{account}:{password}@{server machine's external IP or domain}:3478" -R {min udp port}:{max udp port}
# 3478：The default port at the time of Coturn deployment
# external IP or domain：The external IP address or domain name of the server where Coturn is deployed
# account：The username specified with the -u command during Coturn deployment
# password：The password specified with the -u command during Coturn deployment
# -R {min udp port}:{max udp port}：During Coturn startup, set the UDP port range. For example, when starting with Docker, use -p 49152-65535:49152-65535/udp, or in a binary installation, use --min-port=49152 --max-port=65535. Please ensure that the UDP port range of WebRtc Streamer matches the UDP port range of Coturn.
```
 
###### Docker

```bash
# docker run -d --network=host -it mpromonet/webrtc-streamer -o -s "{server machine's external IP or domain}:3478" -t "{account}:{password}@{server machine's external IP or domain}:3478" -R {min udp port}:{max udp port}
docker run -d --network=host -it mpromonet/webrtc-streamer -o -s "122.254.123.122" -t "admin:mm123456789@122.254.123.122:3478" -R 49152:65535
```
 
###### Linux

```bash
# ./webrtc-streamer -H 0.0.0.0:8000 -o -s "{server machine's external IP or domain}:3478" -t "{account}:{password}@{server machine's external IP or domain}:3478" -R {min udp port}:{max udp port}
 ./webrtc-streamer -H 0.0.0.0:8000 -o -s "122.254.123.122:3478" -t "turn:mm123456789@122.254.123.122:3478" -R 49152:65535
```
 
###### Windows

```bash
# webrtc-streamer.exe -H 0.0.0.0:8000 -o -s "{server machine's external IP or domain}:3478" -t "{account}:{password}@{server machine's external IP or domain}:3478" -R {min udp port}:{max udp port}
webrtc-streamer.exe -H 0.0.0.0:8000 -o -s "122.254.123.122:3478" -t "turn:mm123456789@122.254.123.122:3478" -R 49152:65535
```
 


