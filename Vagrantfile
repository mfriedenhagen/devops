# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
BOX_NAME =  ENV['BOX_NAME'] || "debian/jessie64"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  #config.proxy.http     = "http://10.0.2.2:3128"
  #config.proxy.https    = "http://10.0.2.2:3128"
  #config.proxy.no_proxy = "localhost,127.0.0.1"
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = BOX_NAME
  config.vm.network :private_network, ip: "10.0.1.128"
  config.vm.hostname = 'docker.local'
  config.vm.provider "virtualbox" do |vb|
    # Don't boot with headless mode
    vb.gui = false 
    # Use VBoxManage to customize the VM. For example to change memory:
    vb.customize ["modifyvm", :id, "--memory", "2048"]
  end
  config.vm.provision "fix-no-tty", type: "shell" do |s|
    s.privileged = false
    s.inline = "sudo sed -i '/tty/!s/mesg n/tty -s \\&\\& mesg n/' /root/.profile"
  end
  config.vm.provision "shell",
    inline: 'echo "net.ipv6.conf.all.disable_ipv6 = 1" > /etc/sysctl.d/disable_ipv6.conf && sysctl -p --system'
end
