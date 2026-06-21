# alma-kernel-usb-gadget-rpm
Kernel with added back usb gadget to allow simulation of usb drive from disk image
***
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

Now try this
```bash
# As root:
modprobe g_mass_storage
```
It should load Mass Storage Gadget (MSG), which also load libcomposite and usb_f_mass_storage.
You may see nothing, or something like :
```
[  295.895316] Mass Storage Function, version: 2009/09/11
[  295.895977] LUN: removable file: (no medium)
[  295.896723] no file given for LUN0
[  295.897503] udc dummy_udc.0: failed to start g_mass_storage: -22
[  295.897830] g_mass_storage gadget.0: probe with driver g_mass_storage failed with error -22
[  295.898177] UDC core: g_mass_storage: couldn't find an available UDC
[  593.397745] Mass Storage Function, version: 2009/09/11
[  593.398478] LUN: removable file: (no medium)
[  593.399511] no file given for LUN0
[  593.400684] udc dummy_udc.0: failed to start g_mass_storage: -22
[  593.401097] g_mass_storage gadget.0: probe with driver g_mass_storage failed with error -22
[  593.401297] UDC core: g_mass_storage: couldn't find an available UDC
```
Then, you're ready to use.

Unload the empty gadget :
```bash
# As root:
modprobe -r g_mass_storage
```
Then use your file as a drive, see the [documentation](./documentation/mass-storage.rst) or follow this example :
```bash
# As root:
modprobe g_mass_storage file=path/to/your_image.raw removable=1
```
Enjoy.
-----
```bash
# As root:
rpm -ivh kernel-dan-usb-simul-*.rpm
```
rpm files are available on Vazypompe
