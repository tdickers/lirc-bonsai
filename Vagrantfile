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

  # Based on https://gist.github.com/bullshit/918d74db9473355d7181
  config.vm.provision "shell", inline: <<-SHELL
    apt update
    apt install -y --no-install-recommends \
      build-essential \
      pkg-config \
      python-dev \
      xsltproc

    # TODO sha256sum
    wget https://sourceforge.net/projects/lirc/files/LIRC/0.10.0/lirc-0.10.0.tar.gz/download -O lirc-0.10.0.tgz
    tar -zxf lirc-0.10.0.tgz
    cd lirc-0.10.0
    ./configure


    exit 0 # disable for now
    set -e

    # enable deb-src
    sed -i '/^#\sdeb-src /s/^#//' "/etc/apt/sources.list"
    export DEBIAN_FRONTEND=noninteractive # avoid LIRC curses-style config
    apt update
    apt install -y --no-install-recommends \
      build-essential \
      packaging-dev \
      libusb-dev \
      libasound2-dev \
      libice-dev \
      libsm-dev \
      libx11-dev \
      libirman-dev \
      libftdi-dev \
      dh-autoreconf \
      portaudio19-dev \
      libxt-dev \
      setserial

    wget https://gist.githubusercontent.com/bullshit/918d74db9473355d7181/raw/568b75813d51c8aaa793a83f448a6184b0d4d5aa/USB-Infrared-Toy-driver.patch

    apt-get source lirc
    cd $(find . -maxdepth 1 -type d -name 'lirc*')
    quilt import ../USB-Infrared-Toy-driver.patch
    quilt push
    quilt refresh

    debuild -us -uc

    cd ..
    find . -name 'liblircclient0_*.deb' -o -name 'lirc_*.deb' | xargs dpkg -i

    apt-mark hold lirc

    # TODO select "Dangerous Prototypes USB Infrared Toy" from list
  SHELL
end
