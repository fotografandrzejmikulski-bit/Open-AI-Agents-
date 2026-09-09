# iCar OBD2 — Mobile Diagnostics Reference

## Source boundary

Derived from `instrukcja icar.pdf`. This is a device/user-operation reference, not a vehicle repair manual.

## Compatibility model

The source describes Vgate iCar OBD2 Bluetooth/WiFi ELM327 interfaces and notes broad compatibility with vehicles exposing standard OBD2/eOBD connectors. It lists variants iCar2, iCar3 and iCar Pro with Bluetooth 3.0, Bluetooth 4.0 and WiFi combinations. Compatibility varies by interface, operating system and vehicle.

## Supported application examples

The source lists Car Scanner for Android/iOS, Torque Lite for Android, and additional Android applications including OBD Auto Doctor, OBD Arny, Obd Harry Scan, Olivia Drive and DashCommand. It also references SDprog as a paid Polish-language application.

## Android connection workflow

For Bluetooth variants the source describes: enable Bluetooth → select the Vlink device → pair (the document specifies code `1234`) → configure the diagnostic application for Bluetooth → select Vlink → switch on ignition/start the engine → establish connection. WiFi variants use device WiFi connection followed by selecting WiFi as the application connection type.

## Operational capabilities

Once connected, the source states that applications can read and clear diagnostic codes and display vehicle parameters. The source also documents troubleshooting through alternative applications when a desired parameter or code-clear function is unavailable.

## Safety boundary

The source explicitly warns that the interface does not replace a mechanic for safety-related matters. Diagnostic observations must not be treated as a definitive mechanical diagnosis without appropriate verification.

## Engineering opportunity

Reusable abstraction for a future vehicle-state ingestion layer:

```text
OBD2 ADAPTER → TRANSPORT (BT/WiFi) → ELM327/PROTOCOL → PID/DTC PARSER → NORMALIZED VEHICLE STATE → DIAGNOSTIC UI → VERIFIED INTERPRETATION
```

Potential integration target: device-state adapters and authoritative-readback patterns already used in the repository.

## Evidence class

`SOURCE_DERIVED`. Device compatibility and application behavior should be verified against the exact hardware, vehicle and current application version before implementation claims are promoted.