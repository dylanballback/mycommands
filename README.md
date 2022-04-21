


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
Go to **Prusa Slicer --> Printer Settings --> Custom G-Code**
## Start G-Code
Insert after the ``` G1 X60 E9 F1000 ; intro line ``` 
```G-Code
G1 X200.00 E30 F500.0 ; intro line
```
and before the ``` G92 E0 ```

## End G-Code
