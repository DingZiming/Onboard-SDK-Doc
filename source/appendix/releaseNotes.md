---
title: Release Notes for Onboard SDK 3.8.1
version: 3.8.1
date: 2019-06-04
keywords: [SDK, M210, Point Cloud, Camera, Disparity Map, collision avoidance, GPS-denied]
---

## OSDK 3.8.1 Highlights

<span style="font-size:larger;">Release Date: <strong>2019-06-04</strong></span>

- **Onboard - Payload SDK communication:** Add Onboard - Payload SDK communication APIs (with Payload SDK v1.4.0+).
- **Camera zooming:** Add camera zooming API for Matrice 210 V2 and Matrice 210 RTK V2 (with firmware V 01.00.0450).
- **STM32 TimeSync sample:** Add TimeSync sample in STM32 platform for Matrice 210 V2 and Matrice 210 RTK V2.

## Bug Fixes

- **X4s, X5s video stream support:** Fix bug of getting X4s, X5s, X7 camera video stream for Matrice 210 V2 and Matrice 210 RTK V2.
- **STM32 platform support:** Fix compiling issue of STM32 platform.
- **STM32 platform Waypoint sample:** Fix bug of crashing while more than 95 points of Waypoint Mission are uploaded in STM32 platform.
- **STM32 gimbal sample:** Fix bug of crashing while gimbal sample is running in STM32 platform.

## Improvements

- **Onboard - Mobile SDK communication error detection:** Improve Onboard - Mobile SDK communication API and alarms error when it is not activated.


## OSDK 3.8 Highlights

<span style="font-size:larger;">Release Date: <strong>2019-04-05</strong></span>

- **Support for M210 V2:** OSDK features are now supported for M210 V2. Currently, hardware synchronization and Multi-function IO are not supported. 
- **New Time Sync feature:** The new time sync feature for M210 V2 is added. 
- **Waypoint Mission V2 (beta):** A new generation of waypoint mission for M210 V2 is released for beta developers.

## Supported Firmware

<span style="font-size:larger;">New Feature Support:</span>

- M210/M210 RTK V2: 1.0.0300+

<span style="font-size:larger;">Compatiblity:</span>

- A3/A3 Pro: 1.7.1.5+
- N3: 1.7.1.5+
- M100: 1.3.1.0+
- M600/M600 Pro: 1.0.1.65+
- M210/M210 RTK: 1.1.0410+

<hr>

## Previous Releases

### OSDK 3.7 Highlights

<span style="font-size:larger;">Release Date: <strong>2018-08-14</strong></span>

- **Many new telemetry topics:** Local position in both GPS and GPS-denied situations, data from ESCs, more detailed RC data and additional state information. For a full list see [API Reference](https://developer.dji.com/onboard-api-reference/group__telem.html)
- **New APIs**: `KillSwitch` API for emergency situations, new `MobileDevice` API in preparation of a future update
- **Improved samples, docs and misc. updates** Telemetry documentation has been revamped, samples now demonstrate some additional typical use cases

#### Improvements

- **Deprecation Macros** Some incorrect enum descriptions and old APIs - specfically the MobileCommunication class - are now deprecated, and a `DJI_DEPRECATED` macro has now been added
- **Serial Connection Improvements** Removed serialDevice validation routine that sometimes reported false positives
- **Version String Improvements** Hardware versions can now be accessed as `Version::M210` etc.


### OSDK 3.6 Highlights

- **Major stereo vision stack update:** New samples have been added for better rectification, disparity, and point cloud projection, accurate to a few cm.
- **3D object localization sample:** Building on this stack, we now showcase a CNN-based 3D object detection and localization sample.
- **Multiple performance improvements and bugfixes:** Over twenty bugs have been fixed, and error handling and reporting have been made more robust.

#### Bug Fixes

- **Samples hang when no data on serial line:** The read thread now quits as expected, allowing clean exit.
- **Memory Leaks:** Fixed a few memory leaks in osdk-core, mainly related to buffers.
- **Flight Control Sample height/altitude references:** Previously, flight control samples used an incorrect reference for height, causing unpredictable real-world behavior. This has been fixed.
- **Many other smaller bugfixes:** Undefined return values, uninitialized variables, unreliable initial connection, etc.

#### Improvements

- **Components initialize on successful activation:** All components of Vehicle are now only initialized after activating successfully to allow error handling without the use of exceptions.
- **Actionable error messages:** Errors at various stages will now offer possible causes and remedies.
- **Subscription cleanup:** The vehicle initialization routine will automatically clean up if a previous subscription exists in an unclean state. There is a similar fix for the Advanced Sensing library as well.

#### Developer Notes
- Since program components are no longer initialized prior to activation, please ensure that the first API your program calls after initialization is *activate*.
- Please be sure to update your Advanced Sensing binary to 2.0.1, supporting x86 and 64-bit ARMv8.

### OSDK 3.5 Highlights

- **Access to live camera streams of M210 and M210 RTK**: both FPV camera and main gimbaled camera
- **Comprehensive Samples for live camera streams APIs**: from basic data accessing samples to more advanced target tracking samples
- **More complete license information is added**

### OSDK 3.4 Highlights

- **Support for M210 and M210 RTK:** 
OSDK features are now supported for M210. Currently, hardware synchronization and Multi-function IO are not supported.
- **Stereo vision data from M210 and M210 RTK:** Raw images and disparity map from stereo camera pairs of M210 are now available.
- **M600 backward compatibility:** Supports M600 firmware 1.0.1.20.
- **ROS RTK support:** RTK data via ROS topics.
- **Protocol layer refactor:** Improved performance and better abstraction.
- **Platform Manager:** Better abstraction layer for different computing platforms.
- **Dynamic logging control:** Developers can now start or stop logging.
- **Encryption flag:** Implemented getter/setter to modify encryption flag.


#### Bug Fixes

- **Multi-threaded segmentation fault fix:** Prevents access to unallocated memory in callback thread.
- **Qt sample failed to initialize serial port:** Fixed QThreadManager with renamed pure virtual functions and added mutex to protect init function from being called in two threads.
- **OpenProtocol activation fix:** Performs activation before using encryption.
- **Waypoint push data event handling:** Waypoint PushData variable was not set properly.
- **Local position reference state fix:** Returns state when setting local position.

### Old Releases

- Release notes for pre-3.3 releases can be found [here](../M100-Docs/old-release-notes.html).
