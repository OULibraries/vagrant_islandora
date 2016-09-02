# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_USER="lmc"
VAGRANT_COMMAND = ARGV[0]

Vagrant.configure(2) do |config|

  ### General Vagrant Configuration #######

  # Our starting point for CentOS is Jeff Geerling's ansible base box.
  # https://github.com/geerlingguy/packer-centos-7/
  config.vm.box = "geerlingguy/centos7"
  config.ssh.insert_key = false

  # Virtualbox-specific machine configuration
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 3000
    vb.cpus = 2
  end

  ### Application Specific Setup #########
  config.vm.network :forwarded_port, guest: 8080, host: 8080 # Tomcat
  config.vm.network :forwarded_port, guest: 3306, host: 3306 # MySQL
  config.vm.network :forwarded_port, guest: 8000, host: 8000 # Apache

  # Temorary workaround because Windows
  config.vm.provision "shell", path: "bootstrap.sh", keep_color: "True"

  # Use a "real" user for interactive logins
  if  ['ssh', 'scp'].include? VAGRANT_COMMAND
    # Maybe you want to set this to a real account
    config.ssh.username = VAGRANT_USER
  end

end
