1. Find necessary info about the bluetooth device (while it is connected!)
```bash
pactl list | grep -Pzo '.*bluez_card(.*\n)*'
```