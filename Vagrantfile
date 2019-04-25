# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  # USB info for IRDroid
  vendor_id  = '0x04d8'
  product_id = '0xfd08'
  
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI for USB settings if needed
    # vb.gui = true

    vb.memory = "256"

    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize [
      'usbfilter', 'add', '0', 
      '--target', :id, 
      '--name', 'ESP', 
      '--vendorid', vendor_id, 
      '--productid', product_id
    ]
  end

  config.vm.provision "shell", inline: <<-SHELL
    export DEBIAN_FRONTEND=noninteractive # avoid LIRC curses-style config
    apt update
    apt install -y --no-install-recommends unzip dialog build-essential

    rm -rf /tmp/lirc
    mkdir /tmp/lirc
    cd /tmp/lirc
    echo "4c580206e6c64b12a393dc1119a6ad26514d0637fb3d6ab41ab899cf81ad008d USB_transceiver_LIRC.zip" > lirc.sha256
    wget https://www.irdroid.com/wp-content/uploads/downloads/2017/02/USB_transceiver_LIRC.zip
    sha256sum --strict -c lirc.sha256
    unzip USB_transceiver_LIRC.zip
    
    cd irtoy
    chmod +x ./configure *.sh
    ./configure
    # Option 3 (TODO)
    make
    make install

    # update-rc.d lirc defaults
  SHELL
end
