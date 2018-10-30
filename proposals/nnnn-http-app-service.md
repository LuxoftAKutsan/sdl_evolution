# HTTP App service 

* Proposal: [NNNN](nnnn-http-app-service.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [Core]

## Introduction

This proposal is to create additional service type HTTP with HTTPS connection for AppServices. 

## Motivation

In case in-vehicle cellular data is not available but it's required for Policies, SDL may perform HTTP request via HTTP AppService. 

Robust internet connection is required for:
 - Policy update
 - System updates
 - Vehicle status monitoring
 - Emergency event 

SDL should provide internet connection through mobile within HTTP service in case in-vehicle cellular connection is off.

## Proposed solution

### API extension
Add additional AppServiceType 

```
<enum name="AppServiceType">
	 ...
  <element name = "HTTP"/>
</enum>
```

Add folowing manifest :

```
<struct name="HTTPServiceManifest">
		<param name="httpsSupported type="Boolean" mandatory="false"/>
		<param name="cellularConnection" type="Boolean" mandatory="false"/>
  <param name="traficLimitations" type="Boolean" mandatory="false"/>
	</struct>
```

Add folowing data that service may process.

```
<struct name="HTTPServiceData">
		<param name="url" type="String" mandatory="true"/>
		<param name="http_request_type" type="HTTPRequestType" mandatory="true"/>
		
	</struct>
 
 <enum>
   <element> GET </element>
   <element> POST </element>
   <element> PUT </element>
   <element> DELETE </element>
   <element> DOWNLOAD </element>
 </enum>
 ```
 
 Extend AppServiceData with folowing parameter : 
 
 ```
   <struct name="AppServiceData">
     	<param name="httpServiceData" type="HTTPServiceData" mandatory="false"/>
      ...
   </struct>
 ```

### Usage of HTTP service
Usage of service will be performed by  calling  `GetAppServiceData` RPC. 
HTTP AppService should perform HTTP requestto url and send `GetAppServiceData` response.


## Potential downsides
 - SDL should trust HTTP App service. HTTP App service may replace data from server.
 
## Impact on existing code
 SDL core changes expected. AppService implementation extension
 
## Alternatives considered
 1. Encrypt information from server. But it will limit web serveices for communication. Because web services will have to support encryption.
 2. Avoid using RPC for communicaiton. Implement HTTP service and low level service https://github.com/LuxoftAKutsan/sdl_evolution/blob/registration_of_low_layer_non_rpc_services/proposals/nnnn-low-level-non-rpc-services.md
 
