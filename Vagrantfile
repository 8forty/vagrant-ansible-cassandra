# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|


    N = 3
    (1..N).each do |machine_id|

        config.vm.define "node#{machine_id}" do |machine|
            machine.vm.box = "ubuntu/trusty64"
            machine.vm.box_url = "https://atlas.hashicorp.com/ubuntu/boxes/trusty64"
            machine.vm.hostname = "node#{machine_id}"
            machine.vm.network "private_network", ip: "192.168.56.#{10+machine_id}"

            machine.vm.provider "virtualbox" do |vb|
                vb.memory = 8192
            end

            if machine_id == N
                machine.vm.provision :ansible do |ansible|
                  ansible.limit = "all"
                  ansible.playbook = "site.yml"
                end
            end
        end
    end

    config.vm.define "opscenter" do |opscenter|
        opscenter.vm.hostname = "opscenter"
        opscenter.vm.box = "ubuntu/trusty64"
        opscenter.vm.network  "private_network", ip: "192.168.56.14"

        opscenter.vm.provider "virtualbox" do |vb|
            vb.memory = 2048
        end

        config.vm.provision "ansible" do |ansible|
           ansible.playbook = "tasks/opscenter.yml"
       end
   end
end
