# LIRC controls for an RGB bonsai

*WIP: Vagrant not working yet*

Quick noodling on a project to create a 'build bonsai' showing build status using a bonsai of RGB LEDs. It has an IR control, so the goal here is to develop a LIRC config.

TODO: link model

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