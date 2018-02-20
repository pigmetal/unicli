# UniCLI

Query and control some features of the UniFi controller directly from your command-line.

## Usage

### Settings

UniCLI needs to know three settings in order to work:

 * your UniFi controller's host
 * your username
 * your password

You may create another user, dedicated to be used with UniCLI.

In order to pass those settings to UniCLI, pass the following environment variables to the program: ```UNIFI_HOST```, ```UNIFI_USERNAME```, ```UNIFI_PASSWORD```.

### Devices

#### List devices

```
$ unicli devices list
ID                        Model   Name      IP address     MAC address         Uptime      Version            RX bytes    TX bytes

dmu898nx3c4sd8ylb3ctrfhd  UGW3    Gateway   172.17.0.254   00:11:22:33:44:55   1d 5h 52m   ✓ 4.4.18.5052168   3.53 GB     3.59 GB
dmu898nx3c4sd8ylb3ctrfhd  US24    Switch    172.17.0.1     00:11:22:33:44:55   2d 4h 42m   ✓ 3.9.19.8123      302.66 MB   2.73 GB
```

#### List ports on a device

```
$ unicli devices ports list dmu898nx3c4sd8ylb3ctrfhd
ID  Name      Enabled   Link   STP state    Speed   Duplex   RX bytes    TX bytes

1   Port 1    ✓         UP     forwarding   100     FDX      166.28 MB   611.74 MB
2   Port 2    ✓         UP     forwarding   1000    FDX      337.09 MB   2.38 GB
3   Port 3    ✓         DOWN   disabled     0       HDX      0 B         0 B
4   Port 4    ✓         DOWN   disabled     0       HDX      0 B         0 B
5   Port 5    ✓         DOWN   disabled     0       HDX      0 B         0 B
6   Port 6    ✓         DOWN   disabled     0       HDX      0 B         0 B
7   Port 7    ✓         DOWN   disabled     0       HDX      0 B         0 B
8   Port 8    ✓         DOWN   disabled     0       HDX      0 B         0 B
9   Port 9    ✓         DOWN   disabled     0       HDX      0 B         0 B
10  Port 10   ✓         DOWN   disabled     0       HDX      152.89 KB   3.07 MB
11  Port 11   ✓         DOWN   disabled     0       HDX      0 B         0 B
12  Port 12   ✓         DOWN   disabled     0       HDX      0 B         0 B
13  Port 13   ✓         DOWN   disabled     0       HDX      0 B         0 B
14  Port 14   ✓         DOWN   disabled     0       HDX      0 B         0 B
15  Port 15   ✓         DOWN   disabled     0       HDX      0 B         0 B
16  Port 16   ✓         DOWN   disabled     0       HDX      0 B         0 B
17  Port 17   ✓         DOWN   disabled     0       HDX      0 B         0 B
18  Port 18   ✓         DOWN   disabled     0       HDX      0 B         0 B
19  Port 19   ✓         DOWN   disabled     0       HDX      0 B         0 B
20  Port 20   ✓         DOWN   disabled     0       HDX      0 B         0 B
21  Port 21   ✓         DOWN   disabled     0       HDX      0 B         0 B
22  Port 22   ✓         DOWN   disabled     0       HDX      0 B         0 B
23  Port 23   ✓         DOWN   disabled     0       HDX      0 B         0 B
24  Port 24   ✓         UP     forwarding   1000    FDX      2.73 GB     302.66 MB
25  SFP 1     ✓         DOWN   disabled     0       HDX      0 B         0 B
26  SFP 2     ✓         DOWN   disabled     0       HDX      0 B         0 B
```

#### Enable/disable ports on a device

You may use ports range syntax to specify which port to enable or disable. ```1,10,20``` means ports 1, 10 and 20. ```10-20``` means ports 10 through 20.

```
unicli devices ports [enable|disable] dmu898nx3c4sd8ylb3ctrfhd 1,2,10-20
Port state dmu898nx3c4sd8ylb3ctrfhd/1,2,10-20 state changed.
```

### Networks

#### List networks

```
$ unicli networks list
ID                        Name                  Enabled   Purpose     Subnet             Domain                 VLAN

dmu898nx3c4sd8ylb3ctrfhd  00 - Management       ✓         corporate   172.17.0.254/24    mgmt.acme.local
dmu898nx3c4sd8ylb3ctrfhd  10 - WiFi Guests      ✓         guest       172.17.10.254/24   guests.acme.local   10
dmu898nx3c4sd8ylb3ctrfhd  20 - WiFi             ✓         corporate   172.17.20.254/24   wifi.acme.local     20
dmu898nx3c4sd8ylb3ctrfhd  30 - LAN              ✓         corporate   172.17.30.254/24   lan.acme.local      30
```

#### List wireless networks

```
$ unicli networks wlan list
ID                        Name             Enabled   Security   Encryption   VLAN

dmu898nx3c4sd8ylb3ctrfhd  ACME             ✓         wpapsk     wpa2/ccmp    20
dmu898nx3c4sd8ylb3ctrfhd  ACME Guests      ✗         open       wpa2/ccmp    10
```

#### Enable/disable wireless networks

```
$ unicli networks wlan [enable|disable] dmu898nx3c4sd8ylb3ctrfhd
Wireless network dmu898nx3c4sd8ylb3ctrfhd state changed.
```

### Clients

#### List all clients

```
$ unicli clients list
MAC address        Make       Hostname   Fixed IP address   Last seen    Wired?   Guest?   RX bytes   TX bytes

00:11:22:33:44:55  LcfcHefe   tialus                        1 day ago    ✓        ✗        10.62 MB   87.98 MB
00:11:22:33:44:55  Ubiquiti                                 2 days ago   ✓        ✗        0 B        0 B
00:11:22:33:44:55  Raspberr   alarm      192.22.0.253       2 days ago   ✓        ✗        0 B        0 B
00:11:22:33:44:55  Manufact                                 Never        ✓        ✗        0 B        0 B
```

#### Block/unblock a client

```
$ unicli clients block 00:12:34:56:78
Client 00:11:22:33:44:55 status changed.
```

### Vouchers

#### List all active vouchers

```
$ unicli vouchers list
ID                        Code         Validity   Usable   Down        Up          Quota   Note

dmu898nx3c4sd8ylb3ctrfhd  5190950304   1d         ∞        2.05 Mbps   2.05 Mbps   1 GB    Bob Dylan
dmu898nx3c4sd8ylb3ctrfhd  0338780149   1d         0/1      -           -           -       Mum
```

#### Create a voucher

When creating a voucher, you may pass the following options to specify the voucher's parameters:

```
$ unicli help vouchers create
create a voucher 0.0.1
Antoine POPINEAU <antoine.popineau@appscho.com>

USAGE:
    unicli vouchers create [-n NUMBER] [-e VALIDITY] [-t USAGE] [-c COMMENT] [-q QUOTA] [-d QUOTA_DOWNLOAD] [-u QUOTA_UPLOAD]

OPTIONS:

    -n        how many vouchers to create (default: 1)                          
    -e        validity duration (as ISO8601 durations, e.g. PT24H, etc.)        
              (default: 1440)                                                   
    -t        number of times this voucher can be used (0 for unlimited)        
              (default: 1)                                                      
    -c        comment (default: Created from UniCLI)                            
    -q        usage quota in MB (default: 0)                                    
    -d        download bandwidth limit in Kbps (default: 0)                     
    -u        upload bandwidth limit in Kbps (default: 0)
```

Nothing fancy here, those map to the same settings that can be found in the UniFi Hotspot manager.

```
$ unicli vouchers create -e P1W -c "Visitor from space" -q 1024 -d 128 -u 128
Voucher was created.
```

#### Revoke a voucher

```
$ unicli vouchers revoke dmu898nx3c4sd8ylb3ctrfhd
Voucher dmu898nx3c4sd8ylb3ctrfhd was revoked.
```
