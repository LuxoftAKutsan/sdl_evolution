# Remote ATF Testing

* Proposal: [SDL-NNNN](NNNN-remote_atf_testing.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [ATF]

## Introduction

Providing ability for ATF to emulate `HMI_INTERFACE` in case if SDL located on remote workstation, and for communication with HMI used special local only transport.

## Motivation

Automated testing of SDL on OEM transport will significant reduce amount of efforts on integration step. 
Also it can guarantee that during integration business logic of SDL was not corrupted and successfully ported. 

On various OEM platforms communication between HMI and SDL performed throw transport that may not be exposed out the target (mqueue)
So ATF can't connect to SDL from HMI side and emulate HMI behavior. 
This proposal is about adding optional proxy(relay) layer that will connect to SDL locally on target and expose API to ATF located on other workstation via TCP


## Proposed solution

Create relay server interface that will expose following RPC's:
 - open (channel) -> status
 - send (channel, data) -> status
 - receive (channel) -> data 
 - close (channel) -> status

For communication with SDL OEM adapter will need to implement this API's.
In case if OEM requires additional functionality , relay server API may be extended.

ATF should use this API for sending/receiving data as HMI side.

![HMIReleyServer](/assets/proposals/nnnn-hmi-relay/HMIReleyServer.png)

Remote connection as Mobile side may be done in scope of following proposal : [ATF support of additional transports (BT and USB)](https://github.com/smartdevicelink/sdl_evolution/blob/master/proposals/0126-atf-additional-transports.md), or in case of using WiFi (TCP) transport - no additional implementation required. 



## Potential downsides



## Impact on existing code

Impacts only Automated test framework code. 


## Alternatives considered

Force OEM to use TCP and web-sockets for HMI communication
