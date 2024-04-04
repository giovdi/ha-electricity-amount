# Home Assistant Blueprint - Electricity cost per device

[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip) 80%
![Project stage: Beta](https://img.shields.io/badge/project%20stage-alpha-red.svg)

⚠️ THIS BLUEPRINT IS IN ALPHA STAGE. I started testing this Blueprint on my Home Assistant in early April 2024, and the tests will last for at least a few months. Feel free to test this on your own, but by using this Blueprint, you accept the risk of unexpected results and Utility Meters reset. Thanks for understanding!

# Setup

## 1. Basic configuration

Add the following code to the `configuration.yaml`

**Current tariff and output sensor**: we'll use the Current tariff sensor to store the actual cost for kWh and the Output sensor to track every charge for each device. Add one Output sensor for each device you wish to track
```
input_number:
  tariff_energy:
    name: Electricity Cost per kWh
    icon: mdi:cash
    min: 0
    max: 5
    step: 0.001
    mode: box
    unit_of_measurement: EUR/kWh
  cost_rack:
    name: Electricity cost Rack
    icon: mdi:cash
    min: 0
    max: 99999
    step: 0.0001
    mode: box
    unit_of_measurement: EUR
```

ℹ️ If you're in Italy, I strongly suggest using the [![giovdi - ha-prices](https://img.shields.io/static/v1?label=giovdi&message=ha-prices&color=blue&logo=github)](https://github.com/giovdi/ha-electricity-cost) Blueprint, to automate the sensor based on the current tariff band.

**Utility meter**: it will track all the charges and, if set, split them into tariff bands.
```
utility_meter:
  energy_rack:
    unique_id: energy_rack
    name: Counter Rack
    source: input_number.cost_rack
    cycle: monthly
#    tariffs:
#      - F1
#      - F2
#      - F3
    delta_values: true
    always_available: true
```

After changing the `configuration.yaml` file, restart Home Assistant.


### 2. Set up the integration

Add this integration to your Home Assistant using this button:

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fgiovdi%2Fha-electricity-cost%2Fedit%2Fmain%2Fhome_electricity_cost.yaml)

This integration will track all the delta changes in the input counters, calculate the amount spent for each delta and output the result into the Output sensor.

### 3. Add widget to a Dashboard

Finally, you can add any widget to the Dashboard to display the Output sensor result.

I suggest using ApexCharts Card by RomRider, available in [HACS](https://hacs.xyz/). Here's the documentation: [![giovdi - ha-prices](https://img.shields.io/static/v1?label=RomRider&message=apexcharts-card&color=blue&logo=github)](https://github.com/RomRider/apexcharts-card).

Add it to your Home Assistant with this shortcut:

[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=RomRider&repository=apexcharts-card&category=plugin)

--WIP

## Issues or suggestions?

Feel free to open an Issue of fork this Blueprint to improve it!
