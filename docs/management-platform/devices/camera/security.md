# Security Settings for WebRTC Streamer

By default, WebRTC Streamer is installed using the HTTP protocol. When SSL is required, additional configuration and handling are necessary.

WebRTC Streamer supports deployment using the **HTTPS** protocol.

#### Obtain an HTTPS certificate

We can use certificates issued by official authorities or generate our own development certificates.

###### How to generate a development certificate?

1. Use OpenSSL 
2. Use of third-party websites

On **Windows**, the following steps can be used (on **Linux**, replace `"copy"` with `"cp"` and `"type"` with `"cat"`):

```bash
  openssl genrsa -des3 -out server.key 2048
  openssl req -new -key server.key -out server.csr
  copy server.key server.key.orig
  openssl rsa -in server.key.orig -out server.key
  openssl x509 -req -days 3650 -in server.csr -signkey server.key -out server.crt
  copy server.crt server.pem
  type server.key >> server.pem
```
 
The server.pem file created must contain a 'CERTIFICATE' section as well as a 'RSA PRIVATE KEY' section. It should look like this (x represents BASE64 encoded data):

```plain
-----BEGIN CERTIFICATE-----
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
-----END CERTIFICATE-----
-----BEGIN RSA PRIVATE KEY-----
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
-----END RSA PRIVATE KEY-----
```
 
#### Deploy WebRTC Streamer using HTTPS

Place the previously generated `server.pem` file in the root directory of the WebRTC Streamer program.

Run the following command to start the WebRTC Streamer service with HTTPS.

1. **Windows**

```powershell
# 7443s is the HTTPS port 7443.
webrtc-streamer.exe -H 7443s -c server.pem
```
 
2. **Linux**

```powershell
# 7443s is the HTTPS port 7443.
webrtc-streamer -H 7443s -c server.pem
```
 
3. After the startup is complete, the logs will be visible.

```prolog
nullLogger level:4
HTTP Listen at 7443s
```
 
#### Common Problems

In case the OpenSSL configuration is not set up correctly, the server will not start. Configure an error log file in 'civetweb.conf' to get more information:

```Plain Text
  error_log_file error.log
```
 
Check the content of 'error.log':

```Plain Text
load_dll: cannot load libeay32.*/libcrypto.*/ssleay32.*/libssl.*
```
 
This error message means, the SSL library has not been installed (correctly). For Windows you might use the pre-built binaries. A link is available at the OpenSSL project home page ( [http://www.openssl.org/related/binaries.html](http://www.openssl.org/related/binaries.html)). Choose C:\Program Files\OpenSSL-Win64 as installation directory - this is the default location.

```Plain Text
set_ssl_option: cannot open server.pem: error:PEM routines:*:PEM_read_bio:no start line
set_ssl_option: cannot open server.pem: error:PEM routines:*:PEM_read_bio:bad end line
```
 
These error messages indicate, that the format of the ssl_certificate file does not match the expectations of the SSL library. The PEM file must contain both, a 'CERTIFICATE' and a 'RSA PRIVATE KEY' section. It should be a strict ASCII file without byte-order marks. The instructions above may be used to create a valid ssl_certificate file.