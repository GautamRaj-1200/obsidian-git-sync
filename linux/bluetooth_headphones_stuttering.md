1. Find necessary info about the bluetooth device (while it is connected!)
```bash
pactl list | grep -Pzo '.*bluez_card(.*\n)*'
```
2. The output will be something like this:
```bash
device.name = "bluez_card.8B_A0_0F_41_71_74"                  
device.product.id = "0x000a"
device.string = "8B:A0:0F:41:71:74"
device.vendor.id = "bluetooth:05d6"
Ports:
	headset-output: Headset (type: Headset, priority: 0, available)
Active Port: headset-output
Formats:
	pcm
	.......
```
3. We need the following data : `bluez_card.8B_A0_0F_41_71_74` and `headset-output`. If you have 