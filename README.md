# Hass.io Plejd add-on
Hass.io add-on for Plejd home automation devices. Gives you the ability to control the Plejd home automation devices through Home Assistant.
It uses MQTT to communicate with Home Assistant and supports auto discovery of the devices in range.

It also supports notifications so that changed made in the Plejd app are propagated to Home Assistant.

Thanks to [ha-plejd](https://github.com/klali/ha-plejd) for inspiration.

Disclaimer:
I am in no way affiliated with Plejd and am solely doing this as a hobby project.

## Getting started
To get started, make sure that the following requirements are met:

### Requirements
* A Bluetooth device (BLE), for eg. the built-in device in Raspberry Pi 4.
* An MQTT broker (the Mosquitto Hass.io add-on works perfectly well).

### Tested on
The add-on has been tested on the following platforms:
* Mac OS Catalina 10.15.1 with Node v. 13.2.0
* Raspberry Pi 4 with Hass.io

#### Tested Plejd devices
* DIM-01
* DIM-02
* LED-10
* CTR-01
* REL-01
* REL-02

### Easy Installation
Browse to your Home Assistant installation in a web browser and click on `Hass.io` in the navigation bar to the left.
* Open the Home Assistant web console and click `Hass.io` in the menu on the left side.
* Click on `Add-on Store` in the top navigation bar of that page.
* Paste the URL to this repo https://github.com/icanos/hassio-plejd.git in the `Add new repository by URL` field and hit `Add`.
* Scroll down and you should find a Plejd add-on that can be installed. Open that and install.
* Enjoy!

### Manual Installation
Browse your Hass.io installation using a tool that allows you to manage files, for eg. SMB or an SFTP client etc.
* Open the `/addon` directory
* Create a new folder named `hassio-plejd`
* Copy all files from this repository into that newly created one.
* Open the Home Assistant web console and click `Hass.io` in the menu on the left side.
* Click on `Add-on Store` in the top navigation bar of that page.
* Click on the refresh button in the upper right corner.
* A new Local Add-on should appear named Plejd. Open that and install.
* Enjoy!

### Configuration
You need to add the following to your `configuration.yaml` file:
```
mqtt:
  broker: [point to your broker IP eg. 'mqtt://localhost']
  username: [username of mqtt broker]
  password: !secret mqtt_password
  client_id: mqtt
  discovery: true
  discovery_prefix: homeassistant
  birth_message: 
    topic: 'hass/status'
    payload: 'online'
  will_message: 
    topic: 'hass/status'
    payload: 'offline'
```
The above is used to notify the add-on when Home Assistant has started successfully and let the add-on send the discovery response (containing all devices).

The plugin needs you to configure some settings before working. You find these on the Add-on page after you've installed it.

Parameter | Value
--- | ---
site | Name of your Plejd site, the name is displayed in the Plejd app (top bar).
username | Username of your Plejd account, this is used to fetch the crypto key and devices from the Plejd API.
password | Password of your Plejd account, this is used to fetch the crypto key and devices from the Plejd API.
mqttBroker | URL of the MQTT Broker, eg. mqtt://localhost
mqttUsername | Username of the MQTT broker
mqttPassword | Password of the MQTT broker
includeRoomsAsLights | Adds all rooms as lights, making it possible to turn on/off lights by room instead. Setting this to false will ignore all rooms. *Added in v. 5*.

## I want voice control!
With the Google Home integration in Home Assistant, you can get voice control for your Plejd lights right away, check this out for more information:
https://www.home-assistant.io/integrations/google_assistant/

### I don't want voice, I want HomeKit!
Check this out for more information on how you can get your Plejd lights controlled using HomeKit:
https://www.home-assistant.io/integrations/homekit/

## Changelog
*v 0.1.0*:
* NEW: Rewrote the BLE integration for more stability
* FIX: discovery wasn't always sent

*previous*:
* FIX: bug preventing add-on from building
* NEW: Added support for Plejd devices with multiple outputs (such as DIM-02)

## License

```
Copyright 2019 Marcus Westin <marcus@sekurbit.se>

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
