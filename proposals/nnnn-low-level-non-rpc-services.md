# Low level non RPC application services 

* Proposal: [NNNN](nnnn-http-app-service.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting Review**
* Impacted Platforms: [Core]

## Introduction

Provide ability for application to register own non RPC services that may handle arbitary data. 

Communication between SDL and mobile consists of different levels:
 
 1. Transport level
 2. Protocol level
 3. RPC/Streaming/Bulk level

SmartDeviceLink Protocol may also transfer arbitary data. 
So application will not be required to implement and to use RPC for communication with SDL for some use cases. 


## Motivation



### Motivation for OEM producers
SDL RPC Service (using MOBILE_API) is rather complicated and huge for support.
Also it adds a lot of additional requirements for both OEM provider and application developer. 

OEM provider may need some custom communication with mobile application and RPC usage is too complicated and overloaded.
Any modification of RPC service requires experience in SDL core. 
Any modification of RPC service adds big possibility of regression to existing open source SDL functionality.

Adding additional custom service support with plugin extensible system will provide ability for seamless integration of proprietary features using SmartDeviceLink for OEM producers 

OEM provider can use raw data exchange for custom services, but SDLP (SmartDeviceink Protocol) is better.
Benefits of SDLP usage described below. 

SDLP guarantees:
 - Messages uniqueness 
 - Delivery guaratee.
 - Keep connection/session alive (heart beat)
 - Session multiplexing
 - Malformed messages filtering
 - Messages encryption

### Motivation for application developers 


SDL should provide ability to use only [SmartDeviceink Protocol](https://github.com/smartdevicelink/protocol_spec) as protocol for data transfer. 

SDL should provide RESTfull API for in-car resources that will be used by web applications that will connect to SDL via cloud transport adapter. 

## Proposed solution


## Potential downsides

## Impact on existing code

## Alternatives considered
