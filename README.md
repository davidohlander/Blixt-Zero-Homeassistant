# Blixt-Zero-Homeassistant

This is a documentation of the homeassistant setup for blixtzero. All sensors named zero1 can be duplicated to create an input for multiple blixt-zeros.
 
## Files:

Add-ons.md contain the required add-ons from homeassistant which can be downloaded directly on the website.

HACS.md contain the required add-ons from the HACS (Home assistant community store) which in and of itself is a add-on.

Configuration.yaml is the yaml file which contains all the configurations made. It should be pasted into the configuration.yaml file already present in homeassistant.

Dashboard.yaml contains the code for the dashboard. It should be pasted into the raw configuration editor (top right) on the dashboard.


## MQTT Sensors:

- Sensors:

sensor.zero1_current - measures the raw current from the zero1 broker in mA.

sensor.zero1_voltage - measures the raw voltage from the zero1 broker in mV.

sensor.zero1_frequency - measures the raw frequency from the zero1 broker in mHz.


- Binary sensors:

zero1_state - displays the current state (open/closed) of zero1.

## Downloaded sensors:

sensor.nordpool_kwh_se1_sek_3_10_025 - measures current energyprices in zone 3 of Sweden in SEK/kWh.
  
## Helpers:

Helpers are tools that help convert the raw data to presentable values by doing calculations. Here, they are used to change the unit correctly and calculate power and energy consumption.


- Template sensors:

sensor.zero1_current_2 - measures current from zero1_current and displays it in A.  
State template: {{ states('sensor.zero1_current') | float * 0.001}}


sensor.zero1_voltage_2 - measures voltage from zero1_current and displays it in V.  
State template: {{ states('sensor.zero1_voltage') | float * 0.001 }}
  

sensor.zero1_frequency_2 - measures frequency from zero1_current and displays it in Hz.  
State template: {{ states('sensor.zero1_frequency') | float * 0.001 }}
  

sensor.zero1_power - measures power consumption in W of zero1 by multiplying data from zero1_current and zero1_voltage.  
State template: {{ states('sensor.zero1_current') | float * states('sensor.zero1_voltage')| float * 0.001*0.001 }}
  

sensor.zero1_price - measures the cost of zero1 since set-up in SEK by multiplying data from zero1_energy and nordpool.  
State template: {{ (states('sensor.zero1_energy') | float * states('sensor.nordpool_kwh_se1_sek_3_10_025')| float) |round(3) }}

- Integral sensors:

sensor.zero1_energy - measures energy consumption of zero1 in kWh by taking the integral of zero1_power.

- Utility meters:

sensor.zero1_elkostnad_manad - displays the energy price of zero1 monthly by taking zero1_price and resetting on monthly cycle.

sensor.zero1_energi_manad - displays the energy consumption of zero1 monthly by taking zero1_energy and resetting on a monthly cycle.

## Automations:

zero1_closed notification - Sends a notification to a device when zero1_state changes to closed

zero1_open notification - Sends a notification to a device when zero1_state changes to open.
