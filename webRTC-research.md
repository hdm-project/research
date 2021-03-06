# Web RTC Research

MD File to track research progress on Web RTC

## Tasks

* get Audio/Video
* communicate Audio/Video
* communicate data

## Main APIS

### Media Stream

* For Video and Audio  
* getUserMedia(constraints, successCB, erorCB)  
* constraints decide video/audio etc.  
  * video can eg. define resoultion
  * screen capture! 
* optional (can also only use data)

### RTC Peer Connection

* Media Stream into Peer Connection, comes out as Media Stream etc.
* Features:
  * Signal Processing
  * Codex
  * Routing
  * Encrypt
  * Bandwidth
* Offer and Answer
* can transmit to own local peer (useful for testing, can use on same page)

### RTC Data Channel

* requires Peer Connection
* send JSON in Peer
* on data callbacks (similar to socket.io?)
* P2P -> low latency
* reliable/unreliable setting (speed)

#### some API calls
``` javascript
//get connection
pc = new webkitRTCPeerConnection(servers, {optional: [{RtpDataChannels: true}]});
//on data channel initialized
pc.ondatachannel = function(event) {
  receivechannel = event.channel;
  ...
}
// could also use reliable: true
sendchannel = pc.createDataChannel("sendDataChannel", {reliable: false});
```

## Server Role (Signaling)

* Exchange Session Description Objects
* Use any Messaging Protocol
* Might be able to do some crazy stuff modifying this Session Description (later)

### ICE
Decides on STUN/TURN - finds best solution

#### STUN
1. connect to STUN server to get public IP
2. send this IP to other client

#### TURN (when P2P is impossible)
1. Cloud Fallback
2. Data passes through Server

### Deploy Servers
Amazon VM image straight from google:  `rfc5766-turn-server` - take and plug into Cloud
alternative: `restund`

## Security
* natively integrated (mandatory, data and media)
* AES
* Runs inside Chrome Sandbox
* Encryption
  * Signaling: Https
  * Audio/Video: SRTP
  * Data: DTLS

# Multiple Peers

## Mesh
Copy for all (N clients, N-1 connections per client)

## Star
Most capable Device is center

## MCU
For large amount of clients, MCU is no client (gotta be reliable etc.)

# Phones
* sipML5
* Phono
* Zingaya

# Building an App
* chrome://webrtc-internals (while on a call, gives information - useful for Debugging/Monitoring!)
* adapter.js (for different versions of RTC)

## Frameworks
* Video stuff
  * SimpleWebRTC
  * easyRTC
  * webRTC.io
* P2P Data
  * PeerJS
  * Sharefest
  
## TurnKey Servers
some production servers are out there, register, get key, have fun.


# Sources
* http://io13webrtc.appspot.com/ (2016-10-20)
* https://www.youtube.com/watch?v=p2HzZkd2A40 (GoogleIO WebRTC 2013)
