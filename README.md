# node-red-contrib-esphome

[![platform](https://img.shields.io/badge/platform-Node--RED-red?logo=nodered)](https://flows.nodered.org/node/node-red-contrib-esphome)
[![Min Node Version](https://img.shields.io/node/v/node-red-contrib-esphome.svg)](https://nodejs.org/en/)
[![GitHub version](https://img.shields.io/github/package-json/v/twocolors/node-red-contrib-esphome?logo=npm)](https://www.npmjs.com/package/node-red-contrib-esphome)
[![GitHub stars](https://img.shields.io/github/stars/twocolors/node-red-contrib-esphome)](https://github.com/twocolors/node-red-contrib-esphome/stargazers)
[![Package Quality](https://packagequality.com/shield/node-red-contrib-esphome.svg)](https://packagequality.com/#?package=node-red-contrib-esphome)

[![issues](https://img.shields.io/github/issues/twocolors/node-red-contrib-esphome?logo=github)](https://github.com/twocolors/node-red-contrib-esphome/issues)
![GitHub last commit](https://img.shields.io/github/last-commit/twocolors/node-red-contrib-esphome)
![NPM Total Downloads](https://img.shields.io/npm/dt/node-red-contrib-esphome.svg)
![NPM Downloads per month](https://img.shields.io/npm/dm/node-red-contrib-esphome)
![Repo size](https://img.shields.io/github/repo-size/twocolors/node-red-contrib-esphome)

## About

### !!! Alpha, Alpha, Alpha release. Very. And yes also very cool.


## Changelog

#### 0.2.7
  - fix status [issues/36](https://github.com/twocolors/node-red-contrib-esphome/issues/36)
#### 0.2.5
  - change status algorithm [issues/30](https://github.com/twocolors/node-red-contrib-esphome/issues/30)
  - support Reconnect interval (Default: 15 sec) [issues/29](https://github.com/twocolors/node-red-contrib-esphome/issues/29)
#### 0.2.3
  - support Text
#### 0.2.1
  - support Status in node


## What is node-red-contrib-esphome?

This node provides a simple way to have API access to ESP-Home devices. This enables you to enjoy the rapid prototyping that ESP-Home provides without having to install HomeAssistant; most Node-Red users do their automation in Node-Red anyway.

In addition to the normal basic functions you expect, the esphome-in node provides access to a host of unique information not otherwise easily exposed in HomeAssistant. This may provide exciting new triggers not previously envisioned, and/or awareness of previously unenvisioned dystopian horrors.

## Installation

1. From Node-Red, click the hamburger menu in the top right, select and select Manage pallette, or press Alt-P. But like why would you let go of the mouse at that point? Surely you'd ohhhhhhhh right, assistive devices. I see you my cyborg people, what's up?

2. The User Settings window will appear, with a list of your installed nodes. Select the Install tab. I couldn't figure it out how you'd access it from keyboard, but it's probably like, Tab a lot.

3. In the search field, type "esphome". Something's bound to come up.

4. Select node-red-contrib-esphome, and click Install. Confirm at the prompt; there's also an option that brings you here, and if that's how you arrived, howzit.

5. That's it for installation. You're good to go.

Mind you, assistive device users probably just use the commandline anyway. In which case:

```bash
$ npm i node-red-contrib-esphome
```

This installs two nodes: esphome-in and esphome-out, which are pretty self explanatory. 


### Configuration

You will need to configure each of your esphome device once only; thereafter any esphome node you add can use it.

Configuring a device requires you to know:

 - the IP address of the device (hostname will not currently do, this is alpha software, chill out)
 - the encryption key and password for accessing the device remotely
 
You can get this data from the ESPHome Dashboard; encryption info from the YAML, IP from the log window.


## To configure both esphome-in and esphome-out nodes:

The Properties interface is identical for both nodes. A node can send commands (esphome-out) or receive status messages (esphome-in) for one Entity in a device only.

For example, if a device has two relays that you want to switch, you will need to configure an esphome-out node for each relay. Likewise, to receive state change messages when a relay triggers, you'll need an esphome-in node for each relay too.

1. Whether input or output, add an esphome node.

2. Double click to open the Properties window, and name it.

3. If this is the first time you are interacting with a particular device, you'll need configure it now. It'll be a list selection thereafter.

4. Select Add New Device (the option will be at the bottom if you've already got a lot of devices).

3. In the Properties window, give the device a usefully descriptive name. All esphome nodes will use this name, so this is when you get to rename the old ones that you regret. Mind you, "geysus" was still fun; kept that.

4. Fill in the IP, and paste the encryption stuff; you copied it earlier from the ESPHome panel. You can leave this blank if you're dealing with an older device that doesn't use encryption. Then click Add.

5. Back in the previous Properties window, you'll notice that the Entities dropdown doesn't work yet, so you can't select anything. This is because the node needs to be deployed once in order to get a list of available Entities from the device. So click Done, Deploy, come back, and select the entity you want to control.

That's it. Use in your automations at will. 


## Sending commands

You need to format command payloads as JSON, which 99% of the time will simply be {"state":true} or {"state":false} if you're just turning stuff on and off. Refer below as needed.

Some more specific examples are:

```js
// to set a light on:
msg.payload = {'state': true}

// set a door lock to unlock:
msg.payload = {'command':0}

// to toggle a light to 42% brightness:
msg.payload = {'brightness': 42}

// to press a button:
msg.payload = true
```

If you're having trouble getting a device to behave the way you expect, you are passing it the wrong kind of variable, or you've formatted it wrong. Trust me, it's you; I know because it was me.

To fix this, add a debug node to an esphome-in node, and have a look at the payload. It's JSON, so the type will be defined. A list of variables and the expected type is below.

## Receiving data

An esphome-in node returns an object payload with a generous amount of useful data about a device whenever a state changes on it (sensor input, switch touched, light turned on, etc).

Below is an example of the kind of payload esphome-out returns.

Note that three objects are returned within the payload; one for the usual data you expect, and two others to do with the device itself and its capabilities. 

You will obviously need to parse out the fields you want to use, but if it's inside esphome, it's available here. 

```js
{"payload":{"state":true,"brightness":1,"colorMode":1,"colorBrightness":1,"red":1,"green":1,"blue":1,"white":1,"colorTemperature":0,"coldWhite":1,"warmWhite":1,"effect":""},"device":{"usesPassword":false,"name":"MyDeviceName","macAddress":"XX:XX:XX:XX","esphomeVersion":"2023.3.2","compilationTime":"Apr 25 2023, 21:33:34","model":"esp8285","hasDeepSleep":false,"projectName":"","projectVersion":"","webserverPort":0,"legacyBluetoothProxyVersion":0,"bluetoothProxyFeatureFlags":0,"manufacturer":"Espressif","friendlyName":"","voiceAssistantVersion":WhyIsThisHere,"suggestedArea":""},"entity":{"key":394606768,"type":"Light","name":"Light - Library 2","config":{"objectId":"light_-_library_2","key":394606768,"name":"Light - Library 2","uniqueId":"son029_ifanlib2lightlight_-_library_2","supportedColorModesList":[1],"legacySupportsBrightness":false,"legacySupportsRgb":false,"legacySupportsWhiteValue":false,"legacySupportsColorTemperature":false,"minMireds":0,"maxMireds":0,"effectsList":[],"disabledByDefault":false,"icon":"","entityCategory":0}},"_msgid":"b65536dcd2f8a15a","_event":"node:6b3f6bc02f499ebe","topic":"/your/choice/of/topic"}
```

You can use this data in whatever creative ways occur to you. Please share when they do; it's how we grow as humans, after the relevant royalties and taxes have been deducted.


## Known but non-breaking quirks (in 0.27):

- The eshome-in node doesn't support topics yet, but this is easy to solve by adding a change node after it, and setting the topic there.

- Random errors will output into the debug panel. It has zero effect on functionality, just don't freak out when you see it. 












#### Button

Button inputs may be triggered with any payload in the input message. Simply send a timestamp, `true`, or other payload to the button node. Button type nodes provide no messages into Node-RED.

#### Climate
  - `mode` - optional. 0 - OFF, 1 - AUTO, 2 - COOL, 3 - HEAT, 4 - FAN_ONLY, 5 - DRY.  See `supportedModesList` attr in config
  - `targetTemperature`- optional. float
  - `targetTemperatureLow`- optional. float
  - `targetTemperatureHigh`- optional. float
  - `legacyAway` - optional. Boolean. Deprecated: use `preset` with AWAY
  - `fanMode` - optional. 0 - ON, 1 - OFF, 2 - AUTO, 3 - LOW, 4 - MEDIUM, 5 - HIGH, 6 - MIDDLE, 7 - FOCUS, 8 - DIFFUSE, 9 - QUIET. See `supportedFanModesList` attr in config
  - `swingMode` - optional. 0 - OFF, 1 - BOTH, 2 - VERTICAL, 3 - HORIZONTAL. See `supportedSwingModesList` attr in config
  - `customFanMode` - optional. string. See `supportedCustomFanModesList` attr in config
  - `preset` - optional. 0 - NONE, 1 - HOME, 2 - AWAY, 3 - BOOST, 4 - COMFORT, 5 - ECO, 6 - SLEEP, 7 - ACTIVITY. See `supportedPresetsList` attr in config
  - `customPreset` - optional. string. See `supportedCustomPresetsList` attr in config
#### Cover
  - `legacyCommand` - optional. 0 - OPEN, 1 - CLOSE, 2 - STOP. Deprecated: use `position`
  - `position` - optional. float. 0.0 - CLOSED, 1.0 - OPEN. See `supportsPosition` attr in config
  - `tilt` - optional. float. 0.0 - CLOSED, 1.0 - OPEN. See `supportsTilt` attr in config
  - `stop` - optional. boolean
#### Fan
  - `state` - optional. boolean
  - `speed` - optional. 0 - LOW, 1 - MEDIUM, 2 - HIGH
  - `oscillating` - optional. boolean
  - `direction` - optional. 0 - FORWARD, 1 - REVERSE
  - `speedLevel` - optional. integer. See `supportedSpeedLevels` attr in config
#### Light
  - `state` - optional. boolean
  - `brightness` - optional. float
  - `red` - optional. integer 0-255
  - `green` - optional. integer 0-255
  - `blue` - optional. integer 0-255
  - `colorMode` - optional. integer. See `supportedColorModesList` attr in config
  - `colorBrightness` - optional. float
  - `white` - optional. integer 0-255
  - `colorTemperature` - optional. integer
  - `coldWhite` - optional. float
  - `warmWhite` - optional. float
  - `flashLength` - optional. integer
  - `effect` - optional. string. effect from effects array in config list
#### Lock
  - `command` - REQUIRED. 0 - UNLOCK, 1 - LOCK, 2 - OPEN
  - `code` - optional. string. See `requiresCode` attr in config
#### MediaPlayer
  - `command` - REQUIRED. 0 - MEDIA_PLAYER_COMMAND_PLAY, 1 - MEDIA_PLAYER_COMMAND_PAUSE, 2 - MEDIA_PLAYER_COMMAND_STOP, 3 - MEDIA_PLAYER_COMMAND_MUTE, 4 - MEDIA_PLAYER_COMMAND_UNMUTE
  - `volume` - optional. float
  - `mediaUrl` - optional. string
#### Number
  - `state` - REQUIRED. float. See `minValue`, `maxValue`, and `step` attrs in config
#### Select
  - `state` - REQUIRED. string. See `optionsList` attr in config
#### Siren
  - `state` - REQUIRED. boolean
  - `tone` - optional. string. See `tonesList` attr in config
  - `duration` - optional. integer. See `supportsDuration` attr in config
  - `volume` - optional. integer. See `supportsVolume` attr in config
#### Switch
  - `state` - REQUIRED. boolean
#### Text
  - `state` - REQUIRED. string. See `minLength`, `maxLength` attrs in config

## Pictures

<img src="https://github.com/twocolors/node-red-contrib-esphome/raw/main/readme/device.png">
<img src="https://github.com/twocolors/node-red-contrib-esphome/raw/main/readme/flow.png">
