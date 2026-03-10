# 💡 Motion Light + Sun Conditions

**Advanced motion-activated lighting with sunset/sunrise conditions**

## 🎛️ Configuration Options

| Input | Description | Default |
|-------|-------------|---------|
| `motion_entity` | Motion/Occupancy sensor | Required |
| `light_target` | Light or light group | Required |
| `no_motion_wait` | Seconds after last motion | 120s |
| `enable_sunset_condition` | Only after sunset | `false` |
| `sunset_offset` | Sunset offset (±60min) | 0 min |
| `enable_sunrise_condition` | Only before sunrise | `false` |
| `sunrise_offset` | Sunrise offset (±60min) | 0 min |

## 💡 Example Setup

Motion Sensor: binary_sensor.hall_pir
Light: light.hall_main + light.hall_stairs
Sunset: ✅ +30min (after sunset)
Sunrise: ❌ Disabled
No Motion Wait: 300s (5 minutes)


## ✨ Key Features

- **Restart Mode** - New motion resets timer
- **Dual Sun Conditions** - Sunset OR Sunrise (independent)
- **Configurable Offsets** - ±60 minutes precision
- **Multiple Lights** - Supports light groups
- **Production Tested** - Reliable in real-world use
- **HA YAML Editor** - 100% graphical editor compatible

## 🔧 Logic Flow

Motion ON → [Sun OK?] → Light ON
↓
Motion OFF → Wait X sec → Light OFF


[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fjsilarow%2Fhome-assistant-blueprints%2Fblob%2Fmain%2Fblueprints%2Fmotion_light_sun%2Fmotion_light_sun.yaml)

**© 2026 Cool Apps**

