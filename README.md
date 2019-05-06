# LIRC controls for an RGB bonsai

*WIP: Vagrant not working yet*

Quick noodling on a project to create a 'build bonsai' showing build status using a bonsai of RGB LEDs. It has an IR control, so the goal here is to develop a LIRC config.

TODO: link model

## TODO breadcrumbs for maybe getting a working install
TODO install from source using full dependencies including libusb-dev; actually seeing ttyACM0
And then ln -s /usr/local/lib/liblirc.so.0.0.0 /usr/lib/liblirc.so.0 to fix some share object file issues (or set the prefix when compiling LIRC) - http://lirc.10951.n7.nabble.com/Re-error-while-loading-shared-libraries-liblirc-so-0-td10582.html)
Possibly follow some of http://dangerousprototypes.com/docs/USB_IR_Toy:_Configure_LIRC to configure

Stuck on:
Driver `irman' not found (wrong or missing -U/--plugindir?).

Try:
https://forums.opensuse.org/showthread.php/508988-LIRC-missing-irman-driver?s=116197b7578f78ee36dab23f36a1f041&p=2722648#post2722648z

## Vagrant
For the sake of ease of prototyping on a Mac (running LIRC should be possible but not OOTB), there's a Vagrantfile here that depends on using the VirtualBox provider and USB passthrough of an IRDroid. 

## Misc.
* Using IRDroid USB Transceiver; 

# See Also
* https://www.hackster.io/austin-stanton/creating-a-raspberry-pi-universal-remote-with-lirc-2fd581
* https://sonnguyen.ws/connect-usb-from-virtual-machine-using-vagrant-and-virtualbox/ 
* https://gist.github.com/bullshit/918d74db9473355d7181
* http://www.lirc.org/html/irtoy.html 
* https://www.irdroid.com/2016/12/infrared-task-automation-in-linux-using-the-irdroid-usb-infrared-transceiver/