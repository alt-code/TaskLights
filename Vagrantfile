# -*- mode: ruby -*-
# vi: set ft=ruby :

# VBoxManage extpack install --replace Oracle_VM_VirtualBox_Extension_Pack-5.2.12.vbox-extpack

Vagrant.configure('2') do |config|

  config.vm.box = 'ubuntu/xenial64'

  config.vm.provider :virtualbox do |vb|
    # Better dns settings
    vb.customize [ 'modifyvm', :id, '--natdnshostresolver1', 'on' ]

    # Usb settings
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ["modifyvm", :id, "--usbehci", "on"]
    vb.customize [
        "usbfilter", "add", "0", 
        "--target", :id, 
        "--name", "blink(1)",
        "--manufacturer", "ThingM",
        "--product", "blink(1) mk2"
      ]
    vb.customize [
        "modifyvm", :id,
        "--audio", "coreaudio",
        "--audiocontroller", "hda"
      ]
  end

  config.vm.define :tasklights do |machine|

    machine.vm.network 'private_network', ip: '192.168.44.4'


    machine.vm.provision "shell", inline: <<-SCRIPT
        sudo apt-get update

        sudo apt-get install -y \
            apt-transport-https \
            ca-certificates \
            curl \
            software-properties-common

        curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
        sudo apt-key fingerprint 0EBFCD88

        sudo add-apt-repository \
          "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
          $(lsb_release -cs) \
          stable"

        sudo apt-get update -q
        sudo apt-get install -y docker-ce

        # Audio 
        sudo add-apt-repository ppa:ubuntu-audio-dev/alsa-daily
        sudo apt-get update
        sudo apt-get install -y linux-headers-$(uname -r) oem-audio-hda-daily-dkms alsa alsa-utils pulseaudio pulseaudio-utils gconf2 paprefs
        sudo usermod -a -G audio vagrant

        echo 'options snd-hda-intel model=generic index=0' >> /etc/modprobe.d/alsa-base.conf
        echo 'snd' >> /etc/modules
        echo 'snd-hda-intel' >> /etc/modules
        modprobe snd
        modprobe snd-hda-intel
        alsa force-reload
    SCRIPT
  end

end
