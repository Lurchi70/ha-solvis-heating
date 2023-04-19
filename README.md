# HA Multiscrape

[![GitHub Release][releases-shield]][releases]
[![License][license-shield]](LICENSE)

[![pre-commit][pre-commit-shield]][pre-commit]
[![Black][black-shield]][black]

[![hacs][hacsbadge]][hacs]
[![Project Maintenance][maintenance-shield]][user_profile]

[![Discord][discord-shield]][discord]
[![Community Forum][forum-shield]][forum]

## Important note: troubleshooting

If you don't manage to get the data from your heating device, please [enable debug logging](#debug-logging) and `log_response`. This will provide you with a lot of information for continued investigation. `log_response` will write all responses to files. 

If all of this doesn't help, use the home assistant forum. I cannot give everyone personal assistance and please don't create github issues unless you are sure there is a bug.
Check the [wiki](https://github.com/Lurchi70/ha-solvis-heating/wiki) for help and other details on the functionality of this component.

# HA Solvis Heating custom component
The `solvis_heating` integration uses the XML datainterface of the solvis remote extension of the heating system. 
This allows you to get details from your Solvis Heating device and integrate these into your Home Assistant installation.

Before being able to use the integration, you have to own a solvis remote device and have it attached, configured and available in your network. 
The xml-file is public and can be retrieved via http://<your-device-ip>/sc2_val.xml

When quering this interface your will retrieve a coded string like: 
```
<xml>
  <data>
    AA5555AA056B0C31350600120076028A013A018[...]0000000000
  </data>
</xml>
```
the returned payload data has a length of 439 Bytes in an undocumented format. This data will be decoded and depending on the configuration option 
made available. 
  
![Sample Screenshot for integration into HA](screenshots/screenshot01.png)

## Installation

[![hacs][hacsbadge]][hacs]

- Install manually by copying the files in 'custom_components/solvis_heating' to a new 'custom_components/solvis_heating' directory in HA config directory.
- Restart HA 
- in HA Setting - use "Add Integration" and search for Solvis
- Configure the integration test (ui configuration)

## Sensors
The following sensors are available in the data:

| name                         | Unit   | Description   |
|------------------------------|--------|:-------------------------------------------|
| last_update                  |        | Time since latest data update.                |
| runtime_solar_pump           | h      | Total output runtime of the solar pump. |
| solar_power                  | W      | Current solarpower from the solar panels. |
| solar_pressure               | bar    | Current pressure in the solar pipes. |
| solar_yield                  | kWh    | Total yield of the solar panels to the heating system |
| temperature_buffer_reference | °C     | current refernce temperature in the buffer |
| temperature_H_buffer_top     | °C     | current temperature in the H buffer top |
| temperature_H_buffer_bottom  | °C     | current temperature in the H buffer bottom |
| temperature_circulation      | °C     | current temperature warm water circulation |
| temperature_heating_circuit_1_flow | °C     | current flow temperature heating circuit 1 |
| temperature_heating_circuit_2_flow | °C     | current flow temperature heating circuit 2 |
| temperature_outside          | °C     | current temperature out the building |
| temperature_solar_flow       | °C     | current flow temperature of solar heating  |
| temperature_solar_panel      | °C     | current temperature on the solar panel(s)  |
| temperature_solar_return     | °C     | current return temperature of solar heating  |
| volume_solar_pump            | l/h    | current volume of fluid stream in solar heating  |
| volume_warm_water            | l/min  | current volume of fluid stream in warm water station  |

## Binary Sensors
The following binary sensors are available in the data:

| name                         | Description   |
|------------------------------|:-------------------------------------------|
| burner                       | oil/gas buner started. |
| burner_s2                    | oil/gas s2 buner started |
| circulation_pump             | warm water circulation pump running |
| heating_circuit_1_mixer_open | indicates that the heating circuit 1 increases the flow temperture |
| heating_circuit_1_mixer_close| indicates that the heating circuit 1 decreases the flow temperture |
| heating_circuit_1_pump       | heating circuit 1 pump is running |
| heating_circuit_2_mixer_open | indicates that the heating circuit 2 increases the flow temperture |
| heating_circuit_2_mixer_close| indicates that the heating circuit 2 decreases the flow temperture |
| heating_circuit_2_pump       | heating circuit 2 pump is running |
| heating_circuit_3_pump       | heating circuit 3 pump is running |
| recovery                     | recovery is active |
| solar_pump                   | solar pump is active |
| solar_2_pump                 | second solar pump is active |
| warm_water_station_pump      | warm water station pump is started |
  
<div class='note'>
The solvis heating integration is using the requests pypi package to get the data from your device. 
</div>
