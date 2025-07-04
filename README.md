# Blixt-Zero-Homeassistant

This is a documentation of the homeassistant setup for blixtzero.
 
## Files:

Add-ons.md contain the required add-ons from homeassistant which can be downloaded directly on the website.

HACS.md contain the required add-ons from the HACS (Home assistant community store) which in and of itself is a add-on.

Configuration.yaml is the yaml file which contain all the configurations made.


## MQTT Sensors:

- Sensors:

sensor.zero1_current - measures the raw current from the zero1 broker in mA.

sensor.zero1_voltage - measures the raw voltage from the zero1 broker in mV.

sensor.zero1_frequency - measures the raw frequency from the zero1 broker in mHz.


- Binary sensors:

zero1_state - displays the current state (open/closed) of zero1.
  
## Helpers:
- Template sensors:

sensor.zero1_current_2 - measures current from zero1_current and displays it in A.
  
State template: {{ states('sensor.zero1_current') | float * 0.001}}


sensor.zero1_voltage_2 - measures voltage from zero1_current and displays it in V.
  
State template: {{ states('sensor.zero1_voltage') | float * 0.001 }}
  

sensor.zero1_frequency - measures frequency from zero1_current and displays it in Hz.
  
State template: {{ states('sensor.zero1_frequency') | float * 0.001 }}
  

sensor.zero1_power - measures energy consumption by multiplying data from zero1_current and zero1_voltage.
  
State template: {{ states('sensor.zero1_current') | float * states('sensor.zero1_voltage')| float * 0.001*0.001}}
  

sensor.zero1_price -

- Integral sensors:

sensor.zero1_energy -
