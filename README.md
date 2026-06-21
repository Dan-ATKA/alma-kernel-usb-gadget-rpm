# alma-kernel-usb-gadget-rpm
Kernel with added back usb gadget to allow simulation of usb drive from disk image

## First, check if you already have the drivers, no use to install this if it's already working

Try to load the Dummy Host Controller Driver module 
```bash
# As root:
modprobe dummy_hcd
```
If there is no return, or something looking like this :
```
[   78.387962] dummy_hcd dummy_hcd.0: USB Host+Gadget Emulator, driver 02 May 2005
[   78.388050] dummy_hcd dummy_hcd.0: Dummy host controller
[   78.388488] dummy_hcd dummy_hcd.0: new USB bus registered, assigned bus number 3
[   78.388611] usb usb3: New USB device found, idVendor=1d6b, idProduct=0002, bcdDevice= 5.14
[   78.388637] usb usb3: New USB device strings: Mfr=3, Product=2, SerialNumber=1
[   78.388658] usb usb3: Product: Dummy host controller
[   78.388674] usb usb3: Manufacturer: Linux 5.14.0dan-usb-simul-1 dummy_hcd
[   78.388692] usb usb3: SerialNumber: dummy_hcd.0
[   78.389029] hub 3-0:1.0: USB hub found
[   78.389078] hub 3-0:1.0: 1 port detected
````
Then the virtual usb port have successfully loaded.

```bash
# As root:
modprobe g_mass_storage file=
```

Test
