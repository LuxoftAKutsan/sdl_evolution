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
So if application will not be required to implement and to use RPC for communication with SDL for some use cases. 

 
## Motivation

SDL RPC Service (using MOBILE_API) is rather complicated and huge for support.
Also it adds a lot of additional requirements for both OEM provider and application developer. 

OEM provider may need some custom communication with mobile application and RPC usage is too complicated and overloaded.

SDL should provide ability to use only [SmartDeviceink Protocol](https://github.com/smartdevicelink/protocol_spec) as protocol for data transfer. 

OEM provider can use raw connection for custom services, but SDLP(SmartDeviceink Protocol) is better.
Benefits of SDLP usage described below. 

SDLP guarantees:
 - messages uniquness 
 - delivery guaratees.
 - Keep connection/session alive (heard beat)
 - Session multiplexing
 - Malformed messages filtering
 - Messages encryption

OEM may create custom service as plugin for extracting proprietary logic without modification SDL core code.

Add additional service OpenSource SDL can implement layer of for providing RESTfull API for web applicaitons that will work with SDL via CloudTransportAdapter.

## Proposed solution
![New design approach](../assets/proposals/nnnn-split_policies/new_design.png)

## Potential downsides

## Impact on existing code

## Alternatives considered
