# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "travis-ci/ci-minimal-trusty64"

  config.ssh.username = "travis"
  config.ssh.password = "travis"

  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider "vmware_fusion" do |v|
    v.memory = 1024
  end

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update -y
    sudo apt-get install -y \
      build-essential \
      libssl-dev \
      xvfb \
      firefox

    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash

    curl -o- https://raw.githubusercontent.com/travis-ci/travis-cookbooks/master/cookbooks/xserver/files/default/etc/init.d/xvfb.sh > /etc/init.d/xvfb
    chmod +x /etc/init.d/xvfb

    echo "export DISPLAY=:99.0" >> /home/travis/.bashrc
  SHELL
end
