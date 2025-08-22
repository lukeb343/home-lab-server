# Zabbix Frontend Configuration

### 1. Establishing a Discovery Rule
this scans my specific IP range to identify devices on my network
- Data Collection>Discovery>Create Discovery Rule
  - Name: Local Network
  - Discovery by: Server
  - IP range: 192.168.0.1-254
  - Update Interval: 1h
  - Checks: ICMP Ping

 This will use an ICMP ping every hour sent to any device within the subnet. If the device is able to respond to these pings, it will show back as a device on the network
 - This rule will only discover devices, NOT add them as hosts
 - In order to acheive that it neds a discovery action

### 2. Creating a Discovery Action
This is neded in order to add any device discovered as a host without me manually having to do it
- Alerts>Actions>Create Action
  - Enter Name:
  - New Condition
    - Condition type: Discovery Rule
    - Discovery rule: Local Network
  - Operations
    - Add to host groups: "Discovered Devices"
    - Link Template: ICMP Ping

  Together these will....
  - Periodically scan the network
  - Automatically add and monitor discovered devices
  
