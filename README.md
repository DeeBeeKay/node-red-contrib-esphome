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

### !!! Alpha, Alpha, Alpha release
### !!! Need help writing documentation

Node-RED nodes to ESPhome devices

## Changelog

#### 0.1.0
  - support logs in node
  - allow empty password

## Installation

```bash
$ npm i node-red-contrib-esphome
```

## Inputs

#### Button
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

## Pictures

<img src="https://github.com/twocolors/node-red-contrib-esphome/raw/main/readme/device.png">
<img src="https://github.com/twocolors/node-red-contrib-esphome/raw/main/readme/flow.png">
