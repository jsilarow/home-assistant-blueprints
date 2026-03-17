# 💡 Motion Light + Sun Conditions

**Advanced motion-activated lighting with sun and optional ambient light (IKEA VALLHORN).**

This blueprint turns on lights on motion, with flexible sunset/sunrise conditions and an optional ambient light sensor so that lights only turn on when it actually feels dark.

## 🎛️ Configuration Options

| Input | Description | Default |
|-------|-------------|---------|
| `motion_entity` | Motion/occupancy sensor | Required |
| `light_target` | Light or light group | Required |
| `no_motion_wait` | Seconds after last motion | `120s` |
| `enable_sunset_condition` | Only after sunset | `false` |
| `sunset_offset` | Sunset offset (±60 min) | `0 min` |
| `enable_sunrise_condition` | Only before sunrise | `false` |
| `sunrise_offset` | Sunrise offset (±60 min) | `0 min` |
| `enable_ambient_light` | Enable ambient light (lux) condition | `false` |
| `ambient_light_sensor` | Illuminance sensor, e.g. IKEA VALLHORN | Optional |
| `ambient_light_threshold` | Lux threshold for “dark” | `50 lx` |

## 🌤️ Sun conditions

- If both sun options are **disabled** → automation is always active.  
- If only **sunset** is enabled → active after sunset (plus optional offset).  
- If only **sunrise** is enabled → active before sunrise (minus optional offset).  
- If **both** are enabled → active when any sun condition is met.  

The sun conditions are evaluated using the built‑in `sun` integration in Home Assistant.

## 💡 Ambient Light (IKEA VALLHORN)

When `enable_ambient_light` is turned on and an ambient light sensor is configured:

- The ambient condition is used **only when the sun is above the horizon** (daytime).  
- If current lux is **below** `ambient_light_threshold`, the room is treated as *dark* and the light can turn on even if sun conditions would normally block it.  
- After sunset (sun below horizon) the ambient sensor is **ignored** – motion + sun conditions are enough.

Typical values for **IKEA VALLHORN** in a small hallway:

- Dark room: `0–20 lx`  
- Dim / overcast: `20–80 lx`  
- Lights on in the room: `80–160 lx`  

Recommended threshold:

- `30–60 lx` for “turn on when it feels dark”  
- You can increase it (e.g. `100–150 lx`) if you want lights to turn on more aggressively.

If ambient light is enabled but the sensor is not set or returns invalid values, the blueprint falls back to **not blocking** the automation.

## 💡 Example Setup

- Motion Sensor: `binary_sensor.hall_pir`  
- Light: `light.hall_main` + `light.hall_stairs`  
- Sunset: ✅ `+00:30:00` (30 min after sunset)  
- Sunrise: ❌ disabled  
- Ambient light: ✅ enabled  
- Ambient sensor: `sensor.hall_vallhorn_illuminance`  
- Ambient threshold: `50 lx`  
- No Motion Wait: `300s` (5 minutes)

## ✨ Key Features

- **Restart mode** – new motion resets the off timer.  
- **Dual sun conditions** – sunset OR sunrise, independently configurable.  
- **Configurable offsets** – ±60 minutes precision.  
- **Ambient light aware** – optional lux threshold using IKEA VALLHORN or similar.  
- **Multiple lights** – supports light groups and multiple entities.  
- **Production tested** – used in real setups before release.  
- **HA YAML editor** – 100% graphical editor compatible.

## 🔧 Logic Flow

Motion ON → [Sun / Ambient OK?] → Light ON  
↓  
Motion OFF → Wait X seconds → Light OFF

## ✅ Requirements

- Home Assistant `2024.12` or newer.  
- `sun` integration enabled (default in most setups).  
- Optional: ambient illuminance sensor (e.g. IKEA VALLHORN).

## 🚀 Import Blueprint

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fjsilarow%2Fhome-assistant-blueprints%2Fblob%2Fmain%2Fblueprints%2Fmotion_light_sun%2Fmotion_light_sun.yaml)

## 🧾 Changelog

- `1.0.0` – initial public release (motion + sun + ambient light).

---

© 2026 **Cool Apps**
