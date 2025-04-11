---
layout: default
title: Oniro Architecture
parent: Eclipse Oniro Project
---
### Architecture  
![alt text](./images/oniro-architecture.jpg)

The Eclipse Oniro architecture builds on the solid foundations of OpenHarmony, enhancing and expanding its capabilities. All system enhancements are rigorously managed by an **advanced IP toolchain** to ensure compliance throughout the development process. Within this framework:

- **React Native** extends the usability of existing applications and ecosystems on top of OpenHarmony, enabling seamless integration across platforms.
- **Eclipse Kanto** expands Oniro's ecosystem adaptability and scalability by empowering edge devices with advanced IoT functionalities, including seamless cloud connectivity and flexible device management.
- The incorporation of the **Rust language**, particularly for the **Servo web engine**, bolsters the overall system's safety and security.
- **Eclipse Theia** enhances the development workflow, simplifying application creation within the ecosystem.
- **libvsync** improves the performance and reliability of applications that require precise coordination across multiple processes.
Future enhancements will include the integration of **NearLink**, offering an alternative to Wi-Fi and Bluetooth with lower latency and improved connectivity, particularly suited for automotive and industrial environments.

Text from [here](https://oniroproject.org/)

### Features    
**Hardware collaboration and resource sharing**  
This feature is implemented through the following modules:

- **DSoftBus**
DSoftBus is a unified base for seamless interconnection among devices. It powers OpenHarmony with distributed communication capabilities to quickly discover and connect devices, and efficiently transmit data.

- **Distributed data management**  
Distributed data management leverages DSoftBus to manage application data and user data distributed on different devices. Under such management, user data is no longer bound to a single physical device, and service logic is decoupled from storage. As your applications are running across devices, their data is seamlessly transmitted from one device to another, creating a foundation for a user experience that is smooth and consistent.

- **Distributed Scheduler**  
Distributed Scheduler is designed based on technical features such as DSoftBus, distributed data management, and distributed profile. It builds a unified distributed service management mechanism (including service discovery, synchronization, registration, and invocation), and supports remote startup, remote invocation, binding/unbinding, and migration of applications across devices. This way, your application can select the most suitable device to perform distributed tasks based on the capabilities, locations, running status, and resource usage of different devices, as well as user habits and intentions.

- **Device virtualization**  
A distributed device virtualization platform enables cross-device resource convergence, device management, and data processing so that virtual peripherals can function as capability extensions of smartphones to form a Super Device.

**One-time development for multi-device deployment**

OpenHarmony provides you with the application, ability, and UI frameworks. With these frameworks, you can develop your applications once, and then flexibly deploy them across a broad range of different devices. One-time development for multi-device deployment

Consistent APIs ensure the operational compatibility of applications across devices.

- Adaptation of device capabilities (including CPU, memory, peripheral, and software resources) can be previewed.
- Resources can be scheduled based on the compatibility between applications and the software platform.  

**A unified OS for flexible deployment**

OpenHarmony enables hardware resources to be scaled with its component-based and small-scale designs. It can be deployed on demand for a diverse range of devices, including ARM, RISC-V, and x86 architectures, and providing RAM volumes ranging from hundreds of KiB to GiB.

Text from [here](https://docs.openharmony.cn/pages/v4.1/en/OpenHarmony-Overview.md)  
>**Note:** need verify the words used in this text like 'OpenHarmony' since we want to emphasize Oniro  


### System Types  

OpenHarmony supports the following system types:

- **Mini system**  
A mini system fits into devices that come with Micro Controller Units (MCUs), such as Arm Cortex-M and 32-bit RISC-V processors, and memory greater than or equal to 128 KiB. This system provides multiple lightweight network protocols, a lightweight graphics framework, and a wide range of read/write components with the IoT bus. Typical products include connection modules, sensors, and wearables for smart home.

- **Small system**  
A small system runs on devices whose memory is greater than or equal to 1 MiB and that are equipped with application processors such as Arm Cortex-A. This system provides higher security capabilities, standard graphics frameworks, and video encoding and decoding capabilities. Typical products include smart home IP cameras, electronic cat eyes, and routers, and event data recorders (EDRs) for easy travel.

- **Standard system**  
A standard system runs on devices whose memory is greater than or equal to 128 MiB and that are equipped with application processors such as Arm Cortex-A. This system provides a complete application framework supporting the enhanced interaction, 3D GPU, hardware composer, diverse components, and rich animations. This system applies to high-end refrigerator displays.

Text from [here](https://docs.openharmony.cn/pages/v4.1/en/OpenHarmony-Overview.md)  
>**Note:** need verify the words used in this text like 'OpenHarmony' since we want to emphasize Oniro


Source from `OpenHarmony docs` used LICENSE [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/legalcode)  
You can find legal notice about such info [here](https://gitee.com/openharmony/docs/blob/master/en/Legal-Notices.md#https://gitee.com/link?target=https%3A%2F%2Fcreativecommons.org%2Flicenses%2Fby%2F4.0%2Flegalcode)

