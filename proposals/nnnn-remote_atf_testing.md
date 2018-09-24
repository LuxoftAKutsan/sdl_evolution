# Remote Automated testing

* Proposal: [SDL-NNNN](NNNN-remote_atf_testing.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [ATF]

## Introduction

This proposal is to provide ability for ATF to test SDL separated on remote workstation.

## Motivation

Automated testing of SDL on real OEM hardware would significantly reduce the amount of efforts at integration stage. 
Also, it can ensure that during integration the business logic SDL will be ported successfully and will not be corrupted. 

On various OEM platforms communication between HMI and SDL is performed through transport that may not be retrieved from the target (mqueue). So ATF can't connect to SDL from HMI side and emulate HMI behavior.  
This proposal suggests adding optional proxy (relay) layer that will connect to SDL locally on target and expose API to ATF located on other workstation via TCP.

## Proposed solution

Create Remote ATF Adapter as separate application that will be executed on the same hardware with SDL and provide API for communication with SDL and controlling SDL life cycle.

### Remote ATF Adapter

ATF will use Remote ATF Adapter as a relay for sending data to SDL via HMI connection. 
Remote ATF Adapter may implement any local transport that is used for HMI-SDL connection on specific OEM hardware, but it will provide TCP for ATF and open source ATF will be used. 

![Remote ATF Adapter](/assets/proposals/nnnn-hmi-relay/HMIReleyServer.png)

Remote ATF Adapter should provide folowing functionality :

#### Connection management:
For sending and receving data. In some cases more than one connection (with different connection types) should be opened, so interface should be rather general.

Folowing RPCs's required : 
 - Open Connection (connection parameters)
 - send (connection, data) -> status
 - receive (connection) -> data 
 - Close Connection(connection) -> status

### RPCs for SDL life cycle managment:
Testing of some SDL requires performing ignitions cycle. For SDL ignition cycle means that it will be stopped and started again ( wth additional notifications before stop). So ATF need to control SDL life cycle. 
This can be done only with Remote ATF Adapter on remote workstation. 

Folowing RPCs's required :
 - Start SDL 
 - Stop SDL
 - CheckSDL state
 
### File managment :
Some automated use cases requires special preconditions as modification in ini file, capabilities, preloaded policy table, etc ... Also 
Remote ATF Adapter should provide functionality for file and folder management 
 - Upload file
 - Download file
 - Update file
 - Delete file
 - Check if file exist
 - Create directory
 - Delete directory
 - Check if directory exist 

# Low level OS management 
 - Command execute
 
For communication with SDL OEM adapter will need to implement this API's.  
In case OEM requires additional functionality, relay server API may be extended.

ATF should use this API for sending/receiving data as HMI side.


Remote connection as Mobile side may be done in scope of following proposal : [ATF support of additional transports (BT and USB)](https://github.com/smartdevicelink/sdl_evolution/blob/master/proposals/0126-atf-additional-transports.md), or in case of using WiFi (TCP) transport - no additional implementation required. 



## Potential downsides

N/A

## Impact on existing code

Impacts only Automated test framework code. 


## Alternatives considered

Determine to use TCP and web-sockets for HMI communication by OEM.
