# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "webvirtcloud"
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.provision "shell", inline: <<-SHELL
     sudo sed -i "s/http:\/\/archive\.ubuntu\.com/http:\/\/mirrors.163.com/" /etc/apt/sources.list
     sudo sh /vagrant/dev/libvirt-bootstrap.sh
     sudo sed -i 's/auth_tcp = \"sasl\"/auth_tcp = \"none\"/g' /etc/libvirt/libvirtd.conf
     sudo service libvirt-bin restart
     sudo adduser vagrant libvirtd
     sudo apt-get -y install python-virtualenv python-dev libxml2-dev libvirt-dev zlib1g-dev
     virtualenv /vagrant/venv
     source /vagrant/venv/bin/activate
     pip install -r /vagrant/dev/requirements.txt -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com
  SHELL
end
