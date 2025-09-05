# Overview

The FFT_DataService provides a reliable and efficient way to access production and process data from the Industrial Information Hub (IIH). It acts as a backend service for the FFT_DataBridge and is available as a free application in the Industrial Edge Marketplace. Running directly on the Edge Device, the DataService ensures secure and standardized access to both real-time and historical data from IIH.

## Functionality

- Communicates with the Siemens IIH Essentials OpenAPI (minimum version 2.2.0 required)

- Provides a standardized gRPC/REST interface for downstream applications such as the FFT_DataBridge

- Supplies both real-time values and historical data on request

- Automatically generates a device_list.json file containing all available requestable variables (excluding variables with source type "Static")

- Allows optional configuration via config.toml for:

  - Defining IIH entry points (plc_name, root_asset_id)

  - Setting the gRPC server address (dataservice_host_address)

  - Customizing logging (log level, console output, file path, log rotation)

- Designed for scalability and flexibility, enabling efficient integration with Edge devices and applications

## Security

The FFT_DataService is built with security and reliability in mind:

- Operates only on the local Edge Device

- Accesses data solely from the Siemens Industrial Information Hub (IIH)
  
- No external ports are openend
  
- Does not share or expose data to external networks

- Keeps all logs and configurations local to the device

**This ensures that production data remains protected within the factory environment and is only transferred to external systems if explicitly enabled through the FFT_DataBridge which covers all security aspects.**

## Usage

1. Set up the Siemens IIH according to the official Industrial Information Hub • Reader • Industrial Operations X Documentation.

   - Ensure the IIH Essentials OpenAPI is version 2.2.0 or higher.

   - Make sure the data model is defined and ready.

   - Variables with the source type "Static" cannot be read.

2. Deploy the FFT_DataService on the Edge Device.

   - Without a configuration file, the DataService connects to the local IIH instance and exposes the full data structure.

   - After startup, it generates a device_list.json file in the publish volume. This file lists all variables available for the FFT_DataBridge to request.

3. Optional: Provide a config.toml file to customize the setup.

Example config.toml:
```toml
[[iih.instances]]
plc_name = "PLC"
root_asset_id = "9b252fb1-b984-f677-ce9c-9562bbaff455"
dataservice_host_address = "[::]:53051"

[logging]
console_log = true
level = "INFO"
file_path = "/app/logs/app.log"
file_max_size_bytes = 10485760
file_backup_count = 3
```

- [[iih.instances]]

  - plc_name: Asset name of the root node

  - root_asset_id: Asset ID of the root node

  - dataservice_host_address: Host and port for the gRPC server (default: "[::]:53051")

- [logging]

  - console_log: Enable/disable console logging (default: true)

  - level: Log level (INFO, WARNING, ERROR)

  - file_path: Log file path (must remain "/app/logs/app.log" to ensure proper mounting)

  - file_max_size_bytes: Maximum log file size (default: 10485760 bytes = 10 MB)

  - file_backup_count: Number of rotated log files to keep (default: 3)

**Note: Providing a configuration file is optional and intended for advanced users. If no configuration is supplied, the DataService uses the local IIH instance and reads the full data model.**
