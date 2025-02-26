---

title: AEP service class IDs
description: Association Endpoint (AEP) services provide a programming contract for services that a device supports over a given protocol. Several of these services have established identifiers that should be used when referencing them.
ms.date: 05/04/2023
ms.topic: article

ms.localizationpriority: medium
---

# AEP service class IDs

Association Endpoint (AEP) services provide a programming contract for services that a device supports over a given protocol. Several of these services have established identifiers that should be used when referencing them. These contracts are identified with the **System.Devices.AepService.ServiceClassId** property. This topic lists several well-known AEP service class IDs. The AEP service class ID is also applicable to protocols with custom class IDs.

An app developer should use Advanced Query Syntax (AQS) filters based on the class IDs to limit their queries to the AEP services they plan to use. This will both limit the query results to the relevant services and will significantly increase the performance, battery life, and quality of service for the device. For example, an application can use these service class IDs to use a device as a Miracast sync or DLNA digital media renderer (DMR). For more information about how devices and services interact with each other, see [**DeviceInformationKind**](/uwp/api/Windows.Devices.Enumeration.DeviceInformationKind).

**Important APIs**

- [**Windows.Devices.Enumeration**](/uwp/api/Windows.Devices.Enumeration)

## Bluetooth and Bluetooth LE services

Bluetooth services fall under one of two protocols, either the Bluetooth protocol or the Bluetooth LE protocol. The identifiers for these protocols are:

- Bluetooth protocol ID: {e0cbf06c-cd8b-4647-bb8a-263b43f0f974}
- Bluetooth LE protocol ID: {bb7bb05e-5972-42b5-94fc-76eaa7084d49}

The Bluetooth protocol supports several services, all following the same basic format. The first group of digits in the GUID vary based upon the service, but all Bluetooth GUIDs end with **-0000-1000-8000-00805F9B34FB**. For example, the RFCOMM service has the precursor of 0x0003, so the full ID would be **00000003-0000-1000-8000-00805F9B34FB**. The following table lists some common Bluetooth services.

| Service name                         | GUID                                     |
|--------------------------------------|------------------------------------------|
| RFCOMM                               | **00000003-0000-1000-8000-00805F9B34FB** |
| GATT - Alert notification service    | **00001811-0000-1000-8000-00805F9B34FB** |
| GATT - Automation IO                 | **00001815-0000-1000-8000-00805F9B34FB** |
| GATT - Battery service               | **0000180F-0000-1000-8000-00805F9B34FB** |
| GATT - Blood pressure                | **00001810-0000-1000-8000-00805F9B34FB** |
| GATT - Body composition              | **181B0000-0000-1000-8000-00805F9B34FB** |
| GATT - Bond management               | **0000181E-0000-1000-8000-00805F9B34FB** |
| GATT - Continuous glucose monitoring | **0000181F-0000-1000-8000-00805F9B34FB** |
| GATT - Current time service          | **00001805-0000-1000-8000-00805F9B34FB** |
| GATT - Cycling power                 | **00001818-0000-1000-8000-00805F9B34FB** |
| GATT - Cycling speed and cadence     | **00001816-0000-1000-8000-00805F9B34FB** |
| GATT - Device information            | **0000180A-0000-1000-8000-00805F9B34FB** |
| GATT - Environmental sensing         | **0000181A-0000-1000-8000-00805F9B34FB** |
| GATT - Generic access                | **00001800-0000-1000-8000-00805F9B34FB** |
| GATT - Generic attribute             | **00001801-0000-1000-8000-00805F9B34FB** |
| GATT - Glucose                       | **00001808-0000-1000-8000-00805F9B34FB** |
| GATT - Health thermometer            | **00001809-0000-1000-8000-00805F9B34FB** |
| GATT - Heart rate                    | **0000180D-0000-1000-8000-00805F9B34FB** |
| GATT - Human interface device        | **00001812-0000-1000-8000-00805F9B34FB** |
| GATT - Immediate alert               | **00001802-0000-1000-8000-00805F9B34FB** |
| GATT - Indoor positioning            | **00001821-0000-1000-8000-00805F9B34FB** |
| GATT - Internet protocol support     | **00001820-0000-1000-8000-00805F9B34FB** |
| GATT - Link loss                     | **00001803-0000-1000-8000-00805F9B34FB** |
| GATT - Location and navigation       | **00001819-0000-1000-8000-00805F9B34FB** |
| GATT - Next DST change service       | **00001807-0000-1000-8000-00805F9B34FB** |
| GATT - Phone alert status service    | **0000180E-0000-1000-8000-00805F9B34FB** |
| GATT - Pulse oximeter                | **00001822-0000-1000-8000-00805F9B34FB** |
| GATT - Reference time update service | **00001806-0000-1000-8000-00805F9B34FB** |
| GATT - Running speed and cadence     | **00001814-0000-1000-8000-00805F9B34FB** |
| GATT - Scan parameters               | **00001813-0000-1000-8000-00805F9B34FB** |
| GATT - Tx power                      | **00001804-0000-1000-8000-00805F9B34FB** |
| GATT - User data                     | **0000181C-0000-1000-8000-00805F9B34FB** |
| GATT - Weight scale                  | **0000181D-0000-1000-8000-00805F9B34FB** |

For a more complete listing of available Bluetooth services, see the [GATT Services specification](https://www.bluetooth.com/specifications/gatt/services/). You can also use the [**GattServiceUuids**](/uwp/api/Windows.Devices.Bluetooth.GenericAttributeProfile.GattServiceUuids) API to get some common GATT services.

## Custom Bluetooth LE services

Custom Bluetooth LE services use the following protocol identifier: {bb7bb05e-5972-42b5-94fc-76eaa7084d49}

Custom profiles are defined with their own defined GUIDs. This custom GUID should be used for **System.Devices.AepService.ServiceClassId**.

## UPnP services

UPnP services use the following protocol identifier: {0e261de4-12f0-46e6-91ba-428607ccef64}

In general, all UPnP services have their name hashed into a GUID using the algorithm defined in RFC 4122. The following table lists some common UPnP services defined in Windows.

| Service name                       | GUID                                      |
|------------------------------------|-------------------------------------------|
| Connection manager                 | **ba36014c-b51f-51cc-bf71-1ad779ced3c6**  |
| AV transport                       | **deeacb78-707a-52df-b1c6-6f945e7e25bf**  |
| Rendering control                  | **cc7fe721-a3c7-5a14-8c49-4419dc895513**  |
| Layer 3 forwarding                 | **97d477fa-f403-577b-a714-b29a9007797f**  |
| WAN common interface configuration | **e4c1c624-c3c4-5104-b72e-ac425d9d157c**  |
| WAP IP connection                  | **e4ac1c23-b5ac-5c27-8814-6bd837d8832c**  |
| WFA WLAN configuration             | **23d5f7db-747f-5099-8f21-3ddfd0c3c688**  |
| Printer enhanced                   | **fb9074da-3d9f-5384-922e-9978ae51ef0c**  |
| Printer basic                      | **5d2a7252-d45c-5158-87a4-05212da327e1**  |
| Media receiver registrar           | **0b4a2add-d725-5198-b2ba-852b8bf8d183**  |
| Content directory                  | **89e701dd-0597-5279-a31c-235991d0db1c**  |
| DIAL                               | **085dfa4a-3948-53c7-a0d7-16d8ec26b29b**  |

## WSD services

WSD services use the following protocol identifier: {782232aa-a2f9-4993-971b-aedc551346b0}

In general, all WSD services have their name hashed into a GUID using the algorithm defined in RFC 4122. The following table lists some common WSD services defined in Windows.

| Service name | GUID                                     |
|--------------|------------------------------------------|
| Printer      | **65dca7bd-2611-583e-9a12-ad90f47749cf** |
| Scanner      | **56ec8b9e-0237-5cae-aa3f-d322dd2e6c1e** |

## AQS sample

This AQS will filter for all UPnP **AssociationEndpointService** objects that support DIAL. In this case, [**DeviceInformationKind**](/uwp/api/Windows.Devices.Enumeration.DeviceInformationKind) is set to **AsssociationEndpointService**.

``` syntax
System.Devices.AepService.ProtocolId:="{0e261de4-12f0-46e6-91ba-428607ccef64}" AND
System.Devices.AepService.ServiceClassId:="{085DFA4A-3948-53C7-A0D7-16D8EC26B29B}"
```
