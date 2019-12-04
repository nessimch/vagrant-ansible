# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

    config.vm.provider "virtualbox" do |vb|
       vb.memory = "1024"
       vb.customize ["modifyvm", :id, "--audio", "none"]
     end

     config.vm.define "front-server" do |c|
         c.vm.hostname = "front-server"
         c.vm.network "private_network", ip: "172.16.1.5"
       end

     config.vm.define "back-server" do |c|
          c.vm.hostname = "back-server"
          c.vm.network "private_network", ip: "172.16.1.6"
       end

      config.vm.define "db-server" do |c|
         c.vm.hostname = "db-server"
         c.vm.network "private_network", ip: "172.16.1.7"
       end

      config.vm.provision "ansible" do |ansible|
          ansible.playbook = "./ansible/main.yml"
              ansible.groups = {
                "front" => ["front-server"],
                "back" => ["back-server"],
                "db" => ["db-server"],
                "front-back" => ["front-server","back-server"]
              }
        end
end
