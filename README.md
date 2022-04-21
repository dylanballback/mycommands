


# Bash script to get local ip
Paste this into your terminal window and it will:
- go to /usr/local/bin to store bash script
- Create file name 'myip'
- Open 'myip' in nano editor
```
cd /usr/local/bin

sudo touch myip

sudo nano myip
```

Paste this into your terminal after nano opens 'myip' and it will:
- Allow you to run bash script in any directory
- Display local ip address
```
#!/bin/bash
PATH=${PATH}:$HOME/bin
export PATH

ifconfig en0 | grep 'inet 192' | cut -d " " -f 2
```


### To Run 'myip' bash script
```
bash myip
```


If you dont want to type 'bash' before 'myip'

Paste this into your terminal window

(Only do this if you dont care if any user on computer can execute script)
```
cd /usr/local/bin

sudo chmod 777 myip
```

Now you just need 'myip' to run the bash script 
```
myip
```

<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>

# Connecting to a Websocket through terminal

Paste this into your terminal window
```
wscat --connect ws://192.168.1.64:80/
```
 - '192.168.1.64' = ip address to connect to
 - '80' = port to connect to 


<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>


# Python Read Serial Data

```python

import serial



if __name__ == '__main__':
    #Serial Connection Set Up ('usb address', 'baudrate')
    ser = serial.Serial('/dev/tty.usbmodem11201', 112500, timeout=1)
    ser.reset_input_buffer()


while True:
    #Check if there is new serial data
    if ser.in_waiting > 0:
        #Convert Binary to String
        line = ser.readline().decode('utf-8').rstrip()
  

        print(line)
        
```


<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>



# Prusa Slicer Custom G-Code for Revo Nozzle Filiment Retract
[Reference](https://e3d-online.zendesk.com/hc/en-us/articles/4406857421213-Start-and-End-G-code-for-faster-nozzle-changes)
Go to **Prusa Slicer --> Printer Settings --> Custom G-Code**
## Start G-Code
Insert  
```G-Code
G1 X200.00 E30 F500.0 ; intro line - added for REVO SIX
```
After the 
```G-Code 
G1 X60 E9 F1000 ; intro line 
```
but before the 
```G-Code 
G92 E0 
```

<p>&nbsp;</p>

What my full **Start G-Code** (MK3S+ 0.8 Nozzle) looks like 

```G-Code
M862.3 P "[printer_model]" ; printer model check
M862.1 P[nozzle_diameter] ; nozzle diameter check
M115 U3.10.1 ; tell printer latest fw version
G90 ; use absolute coordinates
M83 ; extruder relative mode
M104 S[first_layer_temperature] ; set extruder temp
M140 S[first_layer_bed_temperature] ; set bed temp
M190 S[first_layer_bed_temperature] ; wait for bed temp
M109 S[first_layer_temperature] ; wait for extruder temp
G28 W ; home all without mesh bed level
G80 ; mesh bed leveling
G1 Z0.2 F720
G1 Y-3 F1000 ; go outside print area
G92 E0
G1 X60 E9 F1000 ; intro line

G1 X200.00 E30 F500.0 ; intro line - added for REVO SIX

G92 E0
M221 S95
```

<p>&nbsp;</p>

## End G-Code
Insert
```G-Code 
G1 E-18 F800 ;retract filament from meltzone - added for REVO SIX
```
Before 
```G-Code 
M104 S0 ; turn off temperature
M140 S0 ; turn off heatbed
```
<p>&nbsp;</p>

What my full **End G-Code** (MK3S+ 0.8 Nozzle) looks like 

```G-Code 
G4 ; wait
M221 S100 ; reset flow
M900 K0 ; reset LA
{if print_settings_id=~/.*(DETAIL @MK3|QUALITY @MK3|@0.25 nozzle MK3).*/}M907 E538 ; reset extruder motor current{endif}

G1 E-18 F800 ;retract filament from meltzone - added for REVO SIX

M104 S0 ; turn off temperature
M140 S0 ; turn off heatbed
M107 ; turn off fan
{if max_layer_z < max_print_height}G1 Z{z_offset+min(max_layer_z+30, max_print_height)}{endif} ; Move print head up
G1 X0 Y200 F3000 ; home X axis
M84 ; disable motors
```

### Don't forget to save printer presets, and add "REVO SCRIPT" at the end of the printer preset name.
