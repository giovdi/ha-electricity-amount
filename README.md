[![Project Status: WIP – Initial development is in progress, but there has not yet been a stable, usable release suitable for the public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip) 80%

# Setup

## 1. Basic configuration

Setup an Input Sensor with the following YAML:
```
cost_rack:
    name: Electricity cost Rack
    icon: mdi:cash
    min: 0
    max: 99999
    step: 0.0001
    mode: box
    unit_of_measurement: EUR
```

This will be the output of our calculus. Every point will be the actual consumption in the currency set.

## x. Setup the Utility meter

Now you can define the Utility meter that will handle the consumption, as the following YAML:
```
energy_rack:
  unique_id: energy_rack
  name: Counter Rack
  source: input_number.cost_rack
  cycle: monthly
  tariffs:
    - F1
    - F2
    - F3
  delta_values: true
  always_available: true
```

