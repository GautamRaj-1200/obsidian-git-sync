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
3. We see that the buffers have currently 0 latency. In the next step, you will need the `NAME` and `PORT` of your output. In this example, these are `bluez_card.28_11_A5_84_B6_F9` and `headset-output`(it may be `speaker-output` if you have a speaker), respectively.
4. Set the buffer size (latency) of your card to a suitable value with this command pattern:
```bash
pactl set-port-latency-offset <NAME> <PORT> <BUFFER_SIZE_MICROSECONDS>
```
