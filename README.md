# Touch Screen Enabled Remote Control for Ground Rovers

Custom Lua telemetry widgets for the **RadioMaster TX16S MKII** transmitter running **EdgeTX**, built to give ground rover operators a flexible, customisable real-time telemetry display.

This is the code for my MSc Electronics Engineering dissertation at the University of Southampton (September 2024), supervised by Dr Klaus Peter Zeuner.

## Overview

Ground rover control systems are often rigid compared with those used for UAVs. This project adapts tools that are common in the UAV world (EdgeTX firmware, Lua scripting, and the ExpressLRS / Crossfire (CRSF) ecosystem) to give ground rovers a customisable telemetry interface.

The interface is made of two EdgeTX widgets.

### 1. Telemetry Display widget
Shows live numerical values:
- Battery percentage
- RSSI (dBm) and a signal strength bar indicator
- Speed and throttle percentage
- GPS position, temperature and humidity (placeholders)
- Alerts: low battery warning (threshold 20%) and weak signal sound alert

**Widget options:** `Interval`, `Decrement`, `AlertVolume`

### 2. Graphical Visualisation widget
Shows telemetry trends over time:
- Battery percentage gauge (red to green colour bands)
- RSSI graph
- Signal strength and link speed indicators
- Combined dashboard view

Graph data is held in a circular buffer so memory use stays low.

## Simulated data

No physical sensors or receiver were used, so values are simulated:

| Parameter | How it is simulated |
|---|---|
| Battery | Decrement timer (user sets interval and percentage step) |
| RSSI / signal strength | Random values, triggered by switch **SA** |
| Noise / interference | Switch **SB** degrades RSSI and signal strength |
| Throttle | Throttle stick position (0 to 100%) |
| Speed | Derived from the elevator (ELE) stick |
| Temperature / humidity / GPS | Random values within set ranges |

The structure is modular so real sensor inputs can replace the simulated ones.

## Requirements

- RadioMaster TX16S MKII (or the EdgeTX Companion simulator)
- EdgeTX firmware with Lua widget support
- EdgeTX Companion (for simulator testing)

## Installation

1. Copy the widget folders from `widgets/` to the `WIDGETS` folder on the radio's SD card (`/WIDGETS/<WidgetName>/main.lua`).
2. Restart the radio.
3. Long-press **PAGE** on the main screen, choose a layout, and add each widget from the widget list.
4. Open each widget's settings to adjust the options.

To test without hardware, load the SD card contents in **EdgeTX Companion** and start the simulator.

## Repository structure

```
.
├── widgets/
│   ├── TelemetryDisplay/
│   │   └── main.lua
│   └── GraphicalDisplay/
│       └── main.lua
├── docs/
│   └── screenshots/
├── README.md
└── .gitignore
```

*(Adjust folder and file names to match your actual project.)*

## Limitations

- All telemetry is currently simulated.
- Lua scripts on the TX16S run at fixed intervals, so heavy processing can reduce refresh rates.
- Customising the widgets needs some Lua knowledge.

## Future work

- Replace simulated data with real sensors (GPS, battery voltage, environmental)
- Add a dedicated GPS widget with location tracking and waypoints
- Optimise Lua code to reduce processing overhead

## Acknowledgements

Thanks to my supervisor Dr Klaus Peter Zeuner, the EdgeTX community, and everyone who helped with Lua and EdgeTX support during the project.

## Licence

Add a licence here (for example MIT), or state that the code is shared for viewing only.
