# -*- mode: ruby -*-
# vi: set ft=ruby :
APP_NAME=File.basename(File.expand_path(".", Dir.pwd))
APP_HOME=File.join(File.dirname(__FILE__), './')

Vagrant.configure("2") do |config|
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.verbose = "v"
  end

  config.vm.define "vm" do |c|
    c.vm.hostname = "#{APP_NAME}"
    c.vm.box = "centos/7"
    c.ssh.insert_key = false
    c.vm.network "private_network", type: "dhcp"
    c.vm.synced_folder APP_HOME, "/opt/#{APP_NAME}"

    c.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--audio", "none"] #needed for proper suspend mode to avoid high CPU usage.
      vb.cpus = 1
      vb.memory = "1024"
      vb.name = "#{APP_NAME}"
    end
  end
end
