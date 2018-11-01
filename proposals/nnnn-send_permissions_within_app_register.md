# Send app permissions within registration

* Proposal: [SDL-NNNN](nnnn-send_permissions_within_app_register.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [Core]

## Introduction
Application may send required policies within its registration. 
So SDL will not have to perform Policy Table Update after each app registration.

## Motivation
This approach resolves the following issues:

 - SDL requires Policy Update after each registration  
 - Big amount of data should be transferred for policy update  
 - Cellular connection may be not stable and not permanent

Providing policies within app registration will reduce amount of communications with policy server, and it does not require internet connection each time during app registration.

## Proposed solution
The proposed solution allows to avoid mandatory Policy Table Update right after a new application registration.  
It will reduce amount of data that SDL will exchange with Policy Server.

### Detailed design
Add new `app_policies` parameter to `RegisterAppInterfaceRequest` 

```
 <function name="RegisterAppInterface" functionID="RegisterAppInterfaceID" messagetype="request" since="1.0">
     <param name="app_policies" type="String" mandatory="true" since="N.N">
            <description>Encrypted Application Permissions</description>
     </param>
```

![Architecture Approach](../assets/proposals/nnnn-send_permissions_within_app_register/arhitecture_approach.png)


The flow within implementation of proposal : https://github.com/LuxoftAKutsan/sdl_evolution/blob/policy_direct_connection/proposals/nnnn-policy_server_direct_cellular_connection.md 

![Registration with sending Application Policies](../assets/proposals/nnnn-send_permissions_within_app_register/register_with_policies.png)

### Certificates managment

SDL should regulary update certificates for application policies decryption.

Policy Table should contain certificates in `module_config` section by `certificate` key.

Triggers for update certificates:

   - Current date is "24 hours prior to module's certificate expiration date"
   - No "certificate" at "module_config" section
   - In case the invalid certificate exists in policies database

# Certification of application 

Application developer should provide list of MOBILE_API functions and parameters that are needed for OEM produces.  
OEM producer will send to application developer encrypted `app_policices` string.  
This string should be used for registration in `app_policies` parameter in `RegisterAppInterface`. 

### Update policies trigger changes

Policy table does not need following trigger for update anymore:

 - An app registered is not listed in PT (device consented)

## Potential downsides

This increases amount of data in RegisterAppInterface.

## Impact on existing code

This proposal will affect sdl_core and policies.

## Alternatives considered

Send `app_policies` in bson within `RegisterAppinterface`. This will not extend MOBILE_API.
