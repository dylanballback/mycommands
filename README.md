


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

chmod 777 myip
```

Now you just need 'myip' to run the bash script 
```
myip
```

---
---
---
---
---
---
---
---
---
---

# Connecting to a Websocket through terminal

Paste this into your terminal window
```
wscat --connect ws://192.168.1.64:80/
```
 - '192.168.1.64' = ip address to connect to
 - '80' = port to connect to 
