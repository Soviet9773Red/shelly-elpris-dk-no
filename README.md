# DK/NO Nord Pool spot price control for Shelly devices  
## **shelly-elpris-dk-no** (v3.1.5)

[![License: AGPL v3](https://img.shields.io/badge/License-AGPL%20v3-blue.svg)](https://www.gnu.org/licenses/agpl-3.0)

**shelly-elpris-dk-no** is a Shelly script for controlling outputs based on Nord Pool spot prices in Denmark (DK1-DK2) and Norway (NO1-NO5).

The project is a regional adaptation of shelly-elprisSE, which itself is based on shelly-porssisahko [v3.1.1](https://github.com/jisotalo/shelly-porssisahko-en/releases/tag/v.3.1.1) by Jussi Isotalo.  
Version 3.1.5 shares the same internal architecture and logic as the [SE](https://github.com/Soviet9773Red/shelly-elprisSE) release, but uses Danish and Norwegian price APIs and regional settings.



### **Version 3.1.5 primary supports Shelly platform Gen2**
```
| Device   | Gen 2 | Gen 3 | Gen 4 |
|----------|-------|-------|-------|
| Plus1    |  OK   |  --   |  --   |
| Plus1 PM |  OK   |  --   |  OK   |
| Plus2 PM |  OK   |  --   |  --   |
| Pro 2    |  OK   |  --   |  --   |
| Pro 3    |  OK   |  --   |  --   |
| Plug S   |  OK   |  SI   |  --   |
| Mini PM  |  --   |  SI   |  --   |

-- = Not tested , SI = Shows instability

Shelly Gen 3-4: - may work, - not fully tested
- memory constraints may cause instability
```



## Key features (3.1.5)

- **Unified DK + NO support**  
  Single build with automatic zone detection and correct API routing.
- **Improved UI**  
  Refined *Status*, *History*, *Setup* and integrated *Help* tab.
- **Grid fee model**  
  Clear weekday/weekend separation and time-of-day detection (where applicable).
- **Improved reliability**  
  Fixes for day rollover, VAT calculation, override persistence and spot price display.
- **Optional H&T temperature addon**  
  Dynamic adjustment of cheapest hours based on Shelly H&T sensor data.



## Price data sources

Prices are fetched via regional APIs and delivered in a compact, Shelly-friendly format:

- **[Denmark:](https://www.elprisenligenu.dk/)** `elprisenligenu.dk`
- **[Norway:](https://www.hvakosterstrommen.no/)** `hvakosterstrommen.no`

At the time of writing, both APIs provide hourly (24-interval) price data.  
The script parses and operates on this format directly, without any internal aggregation.

The current implementation will continue to work as long as the APIs keep delivering 24-hour data.  
If either API switches to *15-minute intervals* in the future, the script will stop working until a new version is released that is adapted to the updated API format.

No transition date for such a change is currently known.


## Getting started

1. Connect your Shelly device to the network.
2. Update firmware to latest **stable** (>= 1.7.x recommended).
     <img src="https://github.com/Soviet9773Red/shelly-elpris-dk-no/blob/main/img/console.jpg?raw=true" width="426"
  align="right"
     style="margin-right:15px; margin-bottom:10px;">
3. Set timezone:
   - **Europe/Copenhagen** (DK)
   - **Europe/Oslo** (NO)
4. Create a new script in Shelly Web UI.
5. Paste the latest **[shelly-elpris-dk-no.js](https://github.com/Soviet9773Red/shelly-elpris-dk-no/blob/main/shelly-elpris-dk-no.js) (ver. 3.1.5)**  build and save.
6. Start the script and open the console.

You will see output similar to:
```
elpris: v.3.1.5_12
elpris: URL http://192.168.8.119/script/1
```


7. Open the HTTP endpoint shown in the console.

> Note: `/script/N` depends on the script slot used on your device.

<br clear="all">

## Built-in web interface
<img src="https://github.com/Soviet9773Red/shelly-elpris-dk-no/blob/main/img/stat.jpg" width="400"
  align="left"
  style="margin-right:15px; margin-bottom:10px;">
  

The Shelly device exposes a lightweight HTTP UI with four tabs:

| Tab | Description |
|-----|-------------|
| **Status** | Current state, prices, outputs and active logic |
| **History** | Logged actions and state changes |
| **Setup** | Zone, VAT, tariffs, outputs and overrides |
| **Help** | Embedded documentation and usage notes |


<br clear="all">

## Important notes

- **KVS structure changed in 3.1.5**  
  Configuration slot **#3 was removed**.  Old KVS keys from earlier versions should be deleted before first start.
- The script assumes **hour-based control logic** though price input is 24-hour based.

<br>



## H&T temperature addon

An optional addon script can be loaded **after** the main script.  
It uses temperature data from a Shelly H&T sensor to dynamically adjust the number of cheapest hours.

Addon documentation and examples are located in the SE [`addons/`](https://github.com/Soviet9773Red/shelly-elprisSE/tree/main/addons) directory.



## Background and credits

Developed by **@Soviet9773Red**  
Based on **shelly-porssisahko** by **Jussi Isotalo**  
With additional ideas and JSON optimizations inspired by the community.



## Source code and build system

The public repository contains **ready-to-use builds** only.  
Internal build tooling, sources and npm-based environment are currently not public.

Forks, adaptations or collaboration can be discussed via GitHub Issues.

---

### Visual overview [shelly-device-map](https://github.com/Soviet9773Red/shelly-device-map) (optional)

When using this script on multiple Shelly devices, it can be convenient to add a simple visual overview.

The **[shelly-device-map](https://github.com/Soviet9773Red/shelly-device-map)** project provides a lightweight, static HTML page where devices can be placed on a floor plan and linked by their local IP addresses. This makes it easy to quickly access the Shelly Web UI, running scripts, and status endpoints from a single view.

Shelly Device Map ([demo](https://soviet9773red.github.io/shelly-device-map/)) is fully static, requires no backend, and can be opened locally or hosted on a small device such as a Raspberry Pi.   

---


## Support the project

Keeping the proxy infrastructure and APIs online costs time and money.  
If this project saves you electricity or hardware headaches, support is welcome.

[![Big Mac](https://img.shields.io/badge/Buy%20me%20a%20🍔-Big%20Mac-yellow?style=for-the-badge)](https://buymeacoffee.com/soviet9773red)

