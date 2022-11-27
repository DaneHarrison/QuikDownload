## 802.11 standard defines the link layer wireless protocol

## 3 Different packet types:
1. Data packets (higher level data)
2. Management packets (control management of the network)
3. Control packets (media access control - used to access shared mediumms)

### (management) Beacons - serve as announcements that a WIFI signal exists (what makes routers appear in windows wifi search for example)
### (management) Deauthentication packets - used to terminate a wifi connection
### (control) Request to send (RTC)     |
### (control) Clear to send (CTS)       | These work together to reduce packet collisions in a transfer RTC (from device) -> CTS (from router)

## Unlike Ethernet, most 802.11 packets have three addresses: 
1. a source address
2. a destination address
3. a Basic Service Set ID (BSSID which is a unique identifier for the access point - MAC is usually the same address)

<br>
<hr>

## two very different encryption techniques used to protect 802.11 networks: Wired Equivalency Protocol (WEP) and Wi-Fi Protected Access (WPA)
1. WEP = older, extremely vulnerable (relies on static 40-104bit key that each client should know - used to initialize a stream cipher (RC4))
2. WPA can be configured in two very different modes: 
    1. pre-shared key (or passphrase) 
        - PTK = pairwise transiet key which is recalculated for every new connection
        - MIC = message integrity code
    2. enterprise mode
        -  PMK is generated at the authentication server and then transmitted down to the client. The AP and the authentication server speak over a protocol called RADIUS which uses the access point as a relay

## When attacking WPA, you are most interested in recovering the PMK. If the network is set up in pre-shared key mode, the PMK allows you to read all the other clients’ traffic (with some finagling) and to authenticate yourself successfully

<br>

## When authenticating to a WPA-based network in enterprise mode, the PMK is created dynamically every time a user connects. This means that even if you recover a PMK, you could impersonate a single user for a specific connection

### Access points send out beacon packets every tenth of a second. Each packet contains the same set of information that would be in a probe response, including name, address, supported rates, and so on

### The major drawback of active scanners is that outside of probe requests (and possibly beacons), they cannot see any other wireless traffic

### Another drawback... Most tools that implement active scanning will only be able to locate networks that your operating system could have found on its own

### 2.4-GHz spectrum is unlicensed, it is a shared medium meaning if u put a wieless card into monitor mode you may see what your neighbors are doing as well

<br>
<hr>

## Starting to hack:
#### An SSID is not a secret. It is included in plaintext in many packets, not just beacons. In fact, the reason the SSID is so important is that you need to know it in order to associate with the AP. This means that every legitimate client transmits the SSID in the clear whenever it attempts to connect to a network.

#### Deauthenticating Users

## Sometimes referred to as Management Frame Protection (MFP), this enhancement makes it possible to stop common deauthenticate attacks, but does little to stop the many other denial of service (DoS) attacks possible against Wi-Fi deployments

## Reaver and hacking WPS - p.163 - around this is also the part when its talking about watching 4 way handshakes taking place and trying to authenticate from thsoe -> 4 way handshakes can be forced by deauthing users
## Having a PSK is not enough - need to still deauth them to get a transient key

## Hacking clients can basically redirect them and get their information but we dont really want that in our situation

# WPA-PSK is particularly challenging as the character set for the pre-shared key can be between 8 and 63 printable ASCII characters and the chosen passphrase is HMAC-SHA1 hashed 4096 times before using it within the PMK