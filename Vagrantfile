# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.ssh.extra_args = ["-o", "PubkeyAcceptedKeyTypes=+ssh-rsa", "-o", "HostKeyAlgorithms=+ssh-rsa"]
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 4
  end

config.vm.define "vm-local-1" do | me |
  #me.vm.box = 'rocky8-py3'
  me.vm.box = 'almalinux/8'
  me.vm.hostname = "vm-local-1"
  me.vm.network :forwarded_port, guest: 22, host: 65530, id: 'ssh'
  me.vm.network :forwarded_port, guest: 80, host: 8080, id: 'http'
  me.vm.network :forwarded_port, guest: 443, host: 8443, id: 'https'
  me.vm.network "private_network", ip: "10.0.0.110"
  me.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.inventory_path = "inventory"
      ansible.limit = "vm-local-1"
      ansible.compatibility_mode = "2.0"
      end

    end

end
