# Midea AC LAN

# FORK from https://github.com/wuwentao/midea_ac_lan

## add support for 56000AG (Midea 120i BT)

## Installation

### Option 1: Install via HACS

> 1. make sure you have installed HACS to Home Assistant [HACS install guide](https://hacs.xyz/docs/setup/download)
> 2. open HACS, click [Custom repositories], Repository input: `https://github.com/wuwentao/midea_ac_lan`, Category select [Integration]
> 3. **Restart Home Assistant**.

### Option 2: Install with Script

> run this script in HA Terminal or SSH add-on

```shell
wget -O - https://github.com/ariellukowski/midea_ac_lan/raw/master/scripts/install.sh | ARCHIVE_TAG=latest bash -
```

### Option 3: Manual Install

1. Download `midea_ac_lan.zip` from [Latest Release](https://github.com/ariellukoeski/midea_ac_lan/releases/latest)
2. copy `midea_ac_lan.zip` to `/custom_components/midea_ac_lan` in Home Assistant.
3. **Restart Home Assistant**.

Once it done, open `[Settings]`, `[Device & services]`, `[Integrations]`, `[Midea AC Lan]`, do init config and add all your devices.

## Add device

**_❗Note: First, set a static IP address for your appliance in the router, in case the IP address of the appliance changes after set-up._**

After installation, search and add component `Midea AC LAN` in Home Assistant integrations page.

Or click [![Configuration](https://my.home-assistant.io/badges/config_flow_start.svg)](https://my.home-assistant.io/redirect/config_flow_start?domain=midea_ac_lan)

**_❗Note: During the configuration process, you may be asked to enter your Midea account and password. It's necessary to retrieve appliance information (Token and Key) from Midea cloud server. After all appliances configured, you can remove the Midea account configuration without affecting the use of the appliance._**

After the account is configured, Click 'ADD DEVICE' once more to add new device. You could repeat the above action to add multiple devices.

### Discover automatically

Using this option, the component could auto-discover and list Midea M-Smart appliances in network or specified IP address, select one and add it in.

You can also use an IP address to search within a specified network, such as `192.168.1.255`.

**_❗Note: Discovery automatically requires your appliances and your Home Assistant must be in the same sub-network. Otherwise, devices may not be auto-discovered. Check this by yourself._**

### Configure manually

If you already know following information, you could add the appliance manually.

- Appliance code
- Appliance type (one of [Supported appliances](README.md#supported-appliances))
- IP address
- Port (default 6444)
- Protocol version
- Token
- Key

### List all appliances only

Using this option, you can list all discoverable Midea M-Smart devices on the network, along with their IDs, types, SNs, and other information.

**_❗Note: For certain reasons, not all supported devices may be listed here._**

## Configure

Configure can be found in `Settings -> Devices & Services -> Midea AC LAN -> Devices -> CONFIGURE`.
You can re-set the IP address when device IP changed.
You can also add extra sensor and switch entities or customize your own device.

### IP address

Set the IP address of device. You can reset this when your device IP is changed.

### Refresh interval

Set the interval for actively refreshing the status of a single device (the unit is second) (30 by default and 0 means not refresh actively)
Mostly the status update of Midea devices relies on the active information notification of the device, \
in which condition the status update in HA still works normally even if the refresh interval is set to be "0". \
This component will also actively query the device status at regular intervals, and the default time is 30 seconds. \
Some devices do not have active information notifications when their status changed, so synchronization with the status in HA will be slower. \
If you are very concerned about the synchronization speed of the status, you can try to set a shorter status refresh interval.

**_❗Note: shorter refresh interval may mean more power consumption_**

### Extra sensor and switch entities

After configuration, one of few main entity (e.g. climate entity) may be generated . If you want to make the attributes to extra sensor and switch entities, click CONFIGURE in Midea AC LAN integration card to choose (your device MUST support this feature).

### Customize

Some types of device have their own configuration items, if your device does not work properly, you may need to customize it. Refer to the device documentation for specific information.

The format of customizations must be JSON.

If multiple customization items need to be configured, the settings must comply with the JSON format.

Example

```json
{ "refresh_interval": 15, "fan_speed": 100 }
```

## Debug and Test

please refer to [Debug and Test](doc/debug.md)
