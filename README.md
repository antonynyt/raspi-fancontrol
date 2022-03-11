# Raspberry Pi Fan Control
A Python script for controlling GPIO fan on the Raspberry Pi with Custom Linux OS. <br>
It works with a systemd service & timer that check every 20s for the CPU temperature. <br>
## Requirement
- A Raspberry Pi
- A Fan with GPIO control capability
- Python RPi.GPIO `apt install python3-rpi.gpio`
- Not the Raspi default OS installed (because otherwise this script is useless)

## Create the service & timer

We put the fancontrol.service in `/etc/systemd/system/`.<br>
Then a timer called fancontrol.timer (the name must be the same as the service) <br>
Next we reload the daemon with `systemctl daemon-reload` and enable the timer `systemctl enable --now fancontrol.timer`.<br>
Voila ! Everything is set and working. Launch Firefox to warm it.

## How to use the script
Change the variables at the begining of the file to suit your preferences.

- Put it in `/usr/bin` with executable permission (`chmod +x fancontrol`).
- It works without doing anything (check CPU temperature every 20s)
- Or you can turn ON/OFF Manually with `fancontrol -i`
````
-h, --help            show this help message and exit
-i, --on              Turn the fan on.
-o, --off             Turn the fan off.
-t, --temperature     Print the CPU Temperature
--timer {start,stop}  Start or Stop the systemd timer to manualy control the fan.
--status              Print the timer status. If it's turned On or Off.
````
Note : it require sudo permission.

## Todo
- [ ] Change the temperature detection process 
- [ ] Clean the code / follow conventions
- [ ] ? Modifiy to set the temperature check with a switch
- [ ] Start the fan for a set time in seconds
