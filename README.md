# OpenLinkHub interface for Linux
Open source Linux interface for iCUE LINK Hub and other Corsair AIOs, Hubs.

![Build](https://github.com/jurkovic-nikola/OpenLinkHub/actions/workflows/go.yml/badge.svg)

![Web UI](https://github.com/jurkovic-nikola/OpenLinkHub/blob/main/static/img/ui.png?raw=true)

# Info
- This project was created out of own necessity to control fans and pumps on workstations after switching everything to Linux.
- I take no responsibility for this code at all. Use this at your own risk. 
- Most of the devices are actually tested on live hardware.
- OpenLinkHub supports multiple devices.
- Take care and have fun!
## Supported devices

| Device                 | VID    | PID                | Sub Devices                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|------------------------|--------|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| iCUE LINK System Hub   | `1b1c` | `0c3f`             | <details><summary>Show</summary>iCUE LINK QX Fan<br />iCUE LINK RX Fan<br/>iCUE LINK RX RGB Fan<br/>iCUE LINK RX MAX Fan<br/>iCUE LINK H100i<br/>iCUE LINK H115i<br/>iCUE LINK H150i<br/>iCUE LINK H170i<br/>XC7 Elite<br/>XG7<br/>XD5 Elite<br/>XD5 Elite LCD <br/>VRM Cooling Module<br />iCUE LINK TITAN H100i<br />iCUE LINK TITAN H150i<br />iCUE LINK TITAN H115i<br />iCUE LINK TITAN H170i</details>                                                                                                                                                                   | |                                                                                                                                                                   |
| iCUE COMMANDER Core    | `1b1c` | `0c32`<br />`0c1c` | <details><summary>Show</summary>H100i ELITE CAPELLIX<br />H115i ELITE CAPELLIX<br />H150i ELITE CAPELLIX<br />H170i ELITE CAPELLIX<br />H100i ELITE LCD<br />H150i ELITE LCD<br />H170i ELITE LCD<br />H100i ELITE LCD XT<br />H115i ELITE LCD XT<br />H150i ELITE LCD XT<br />H170i ELITE LCD XT<br />H100i ELITE CAPELLIX XT<br />H115i ELITE CAPELLIX XT<br />H150i ELITE CAPELLIX XT<br />H170i ELITE CAPELLIX XT<br />1x Temperature Probe<br /> 4-LED RGB Fan<br /> 8-LED RGB Fan<br /> QL Fan Series<br /> LL Fan Series<br /> ML Fan Series<br />Any PWM Fan</details> |
| iCUE COMMANDER Core XT | `1b1c` | `0c2a`             | <details><summary>Show</summary>External RGB Hub<br />2x Temperature Probe<br /> 4-LED RGB Fan<br /> 8-LED RGB Fan<br /> QL Fan Series<br /> LL Fan Series<br /> ML Fan Series<br />Any PWM Fan<br />H55 RGB AIO<br />H100 RGB AIO<br />H150 RGB AIO</details>                                                                                                                                                                                                                                                                                                                 |
| iCUE H100i RGB ELITE   | `1b1c` | `0c35`<br />`0c40` |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| iCUE H115i RGB ELITE   | `1b1c` | `0c36`             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| iCUE H150i RGB ELITE   | `1b1c` | `0c37`<br />`0c41` |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Lighting Node CORE     | `1b1c` | `0c1a`             | <details><summary>Show</summary>HD RGB Series Fan<br />LL RGB Series Fan<br />ML PRO RGB Series Fan<br />QL RGB Series Fan<br />8-LED Series Fan<br />SP RGB Series Fan</details>                                                                                                                                                                                                                                                                                                                                                                                              |
| Lighting Node PRO      | `1b1c` | `0c0b`             | <details><summary>Show</summary>2x External RGB Hub<br />HD RGB Series Fan<br />LL RGB Series Fan<br />ML PRO RGB Series Fan<br />QL RGB Series Fan<br />8-LED Series Fan<br />SP RGB Series Fan</details>                                                                                                                                                                                                                                                                                                                                                                     |
| Commander PRO          | `1b1c` | `0c10`             | <details><summary>Show</summary>2x External RGB Hub<br />4x Temperature Probe<br />Any PWM Fan</details>                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |

## Installation (automatic)
As of 0.1.5 version, OpenLinkHub ships with `.deb` and `.rpm` packages for ease of installation.
Packages will automatically set up all the required device and folder permissions.
Packages will also take care of systemd service creation and first startup.
1. Download either .deb or .rpm package from the latest Release, depends on your Linux distribution
2. Open terminal
3. Navigate to the folder where the package is downloaded
```bash
# Debian Based (deb)
$ sudo dpkg -i OpenLinkHub_X.X.X_amd64.deb 

# RPM based (rpm)
$ sudo rpm -ivh OpenLinkHub-X.X.X-1.x86_64.rpm
```

## Installation (manual)
### 1. Requirements
- libudev-dev
- go 1.22.2 - https://go.dev/dl/
```bash
# Required packages (deb)
$ sudo apt-get install libudev-dev

# Required packages (rpm)
$ sudo dnf install libudev-devel
```
### 2. Build & install
```bash
$ git clone https://github.com/jurkovic-nikola/OpenLinkHub.git
$ cd OpenLinkHub/
$ go build .
$ chmod +x install.sh
$ sudo sh install.sh
```

### 3. Installation from compiled build
```bash
# Download latest build from https://github.com/jurkovic-nikola/OpenLinkHub/releases
$ wget https://github.com/jurkovic-nikola/OpenLinkHub/releases/download/0.1.6-rc/OpenLinkHub_0.1.6_amd64.tar.gz
$ tar xvf OpenLinkHub_0.1.6_amd64.tar.gz
$ cd OpenLinkHub/
$ chmod +x install.sh
$ sudo sh install.sh
```

### 4. Configuration
```json
{
  "listenPort": 27003,
  "listenAddress": "127.0.0.1",
  "cpuSensorChip": "k10temp",
  "manual": false,
  "frontend": true
}
```
- listenPort: HTTP server port.
- listenAddress: Address for HTTP server to listen on.
- cpuSensorChip: CPU sensor chip for temperature. `k10temp` or `zenpower` for AMD and `coretemp` for Intel
- manual: set to true if you want to use your own UI for device control. Setting this to true will disable temperature monitoring and automatic device speed adjustments. 
- frontend: set to false if you do not need WebUI console, and you are making your own UI app. 

## Running in Docker
As an alternative, OpenLinkHub can be run in Docker, using the Dockerfile in this repository to build it locally. A configuration file has to be mounted to /opt/OpenLinkHub/config.json
```
$ docker build . -t openlinkhub
$ # To build a specific version you can use the GIT_TAG build argument
$ docker build --build-arg GIT_TAG=0.1.3-beta -t openlinkhub .

$ docker run --privileged -v ./config.json:/opt/OpenLinkHub/config.json openlinkhub

# For WebUI access, networking is required
$ docker run --network host --privileged -v ./config.json:/opt/OpenLinkHub/config.json openlinkhub
```

## Device Dashboard
- Simple Device Dashboard is accessible by browser via link `http://127.0.0.1:27003/`
- Device Dashboard:
  - System Overview
  - Device Overview:
    - Change temperature profile per channel
    - Change RGB mode per device
  - Temperature Overview:
    - Create new profiles
    - Update existing profiles
    - Delete existing profile
  - General dashboard settings
- You should use Device Dashboard for any configuration
- Bootstrap 5 Dark Admin template

## RGB Modes
- RGB configuration is located at `database/rgb.json` file.
### Configuration
- profiles: Custom RGB mode data
  - key: RGB profile name
    - speed: RGB effect speed, from 1 to 10
    - brightness: Color brightness, from 0.1 to 1
    - smoothness: How smooth transition from one color to another is.
      - the smoothness is in range of 1 to 40
    - start: Custom starting color in (R, G, B, brightness format)
    - end: Custom ending color  (R, G, B, brightness format)
      - If you want random colors, remove data from start and end JSON block. `"start":{}` and `"end":{}`

## API
- OpenLinkHub ships with built-in HTTP server for device overview and control.
- Documentation is available at `http://127.0.0.1:27003/docs`
## Automatic startup
### systemd config
- This is a plain basic systemd example to get you running. You can create systemd service how you like. 
```
[Unit]
Description=Open source interface for iCUE LINK System Hub

[Service]
User=your-user
WorkingDirectory=/opt/OpenLinkHub
ExecStart=/opt/OpenLinkHub/OpenLinkHub
ExecReload=/bin/kill -s HUP $MAINPID
RestartSec=5

[Install]
WantedBy=multi-user.target
```
- Modify User= to match user who will run this
- Modify WorkingDirectory= to match where executable is
- Modify ExecStart= to match an executable path
- Save content to `/etc/systemd/system/OpenLinkHub.service` (deb based)
- Save content to `/usr/lib/systemd/system/OpenLinkHub.service` (rpm based)
- Run `systemctl enable --now OpenLinkHub`
