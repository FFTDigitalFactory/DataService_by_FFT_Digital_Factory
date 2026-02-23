# Overview

The FFT DataService provides a reliable and efficient way to access production and process data from the Industrial Information Hub (IIH). It acts as a backend service for the FFT_DataBridge and is available as a free application in the Industrial Edge Marketplace. Running directly on the Edge Device, the DataService ensures secure and standardized access to both real-time and historical data from IIH.

## Functionality

- Communicates with the Siemens IIH Essentials OpenAPI (minimum version 2.2.0 required)

- Provides a standardized gRPC interface for downstream applications such as the FFT_DataBridge

- Supplies both real-time values and historical data on request

- Automatically generates a device_list.json file containing all available requestable variables (excluding variables with source type "Static")

- Designed for scalability and flexibility, enabling efficient integration with Edge devices and applications

## Security

The FFT DataService is built with security and reliability in mind:

- Operates only on the local Edge Device

- Accesses data solely from the Siemens Industrial Information Hub (IIH)
  
- No external ports are openend
  
- Does not share or expose data to external networks

- Keeps all logs and configurations local to the device

## Documentation
[User Manual – FFT DataService](UserManual_DataService_V002.pdf)
