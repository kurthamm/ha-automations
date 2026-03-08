# Home Assistant Automations

Hamm household HA automations, version-controlled for sanity.

## Categories

### HVAC
- **den-dual-heater-control** — Main downstairs climate control (V7). 4-layer variable architecture.
- **hvac-fan-circulation** — Periodic fan circulation
- **upstairs-climate-control** — Upstairs thermostat management
- **energy-hvac-extended-heating-alert** — Alert if HVAC runs too long
- **energy-daily-hvac-summary** — Daily energy summary

### Garage
- **garage-lights-on-with-motion-when-dark** — TriSensor 8 motion → Hue lights
- **garage-lights-auto-off-15-min-after-on** — Auto-off timer
- **garage-morning-vent-open** — Open to 20% for the cat
- **garage-auto-close-to-vent-after-timeout** — Close back to vent position
- **garage-sync-hue-light-with-door-opener-led** — Visual sync
- **notify-kurt-garage-door-opened** — Push notification

### Walmart Delivery
- **walmart-delivery-open-garage-when-driver-en-route**
- **walmart-delivery-close-garage-to-vent-10-min-after-delivered**
- **walmart-delivery-reset-override-when-garage-closed**
- **walmart-delivery-safety-timeout-45-min-max**

### Lighting
- **outdoor-lighting-sunset-on-dim-late-off-at-sunrise**
- **decorative-plugs-on-at-sunset-off-at-midnight**
- **master-bedroom-motion-lighting-with-auto-off-and-dnd**
- **master-bedroom-auto-off-after-manual-light-on**
- **half-bath-motion-light-3-min-auto-off**
- **smooth-sunrise-simulation-all-hue-ambiance-lamps** (off)

### Office
- **office-blink-lights-for-calendar-meetings**
- **turn-off-office-lights-when-kurts-phone-leaves-home** (off)
- **office-smart-humidifier-auto-control** (off)

### Kitchen
- **kitchen-door-auto-unlock-when-garage-opens**
- **microwave-done-tts-alert-all-speakers**
- **kitchen-tovala-oven-done-tts-alert**

### Safety
- **smokeco-emergency-alert-system**

### Network Monitoring (Syslog)
- **syslog-wan-outage-alert**
- **syslog-count-wifi-deauths**
- **syslog-deauth-storm-alert**
- **syslog-reset-deauth-counter**
- **syslog-aimesh-problem**
- **syslog-dfs-radar-alert**
- **syslog-router-reboot**

### Other
- **litter-box-notifications** (off)
- **litter-robot-full-waste-drawer-evening-tts-alert** (off)
- **frigate-person-detected-in-garage**

## Architecture Notes

### Den Dual-Heater Control (V7)
The main HVAC automation uses **4 sequential variable layers** to avoid Home Assistant's
simultaneous variable evaluation limitation:

1. **Layer 1**: Constants + direct state reads (41 vars)
2. **Layer 2**: Time period calculations, weather (15 vars)
3. **Layer 3**: Schedule targets, computed states (9 vars)
4. **Layer 4**: Final action decisions (13 vars)

Each layer can reference variables from previous layers but not its own.
