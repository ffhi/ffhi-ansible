# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "debian/stretch64"
    config.vm.network :public_network, :bridge => 'br0', :dev => 'virbr1'

    config.vm.provision "ansible" do |ansible|
        ansible.verbose = "v"
        ansible.playbook = "playbook.yml"
        ansible.groups = {
            "WebServers" => ["web"],
            "Concentrators" => ["concentrator"],
            "Clients" => ["client"],
        }
    end

    config.vm.define "web", autostart: false do |web|
        web.vm.hostname = "web"
    end

    config.vm.define "concentrator" do |concentrator|
        concentrator.vm.hostname = "concentrator"
    end

    config.vm.define "client" do |client|
        client.vm.hostname = "client"
    end

    config.vm.provider "libvirt" do |libvirt|
        libvirt.memory = "1024"
    end

    config.vm.synced_folder './', '/vagrant', type: '9p', disabled: true, accessmode: "mapped", mount: false
end

