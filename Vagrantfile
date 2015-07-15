# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
	config.vm.define "primary" do |primary|
		primary.vm.box = "ubuntu/trusty64"
		primary.vm.network "public_network", ip:"192.168.1.180"
		primary.vm.provider :virtualbox do |vb|
			vb.customize ["modifyvm", :id, "--memory", "512"]
		end
	end
	config.vm.define "secondary1" do |secondary1|
		secondary1.vm.box = "ubuntu/trusty64"
		secondary1.vm.network "public_network", ip:"192.168.1.181"
		secondary1.vm.provider :virtualbox do |vb|
			vb.customize ["modifyvm", :id, "--memory", "512"]
		end
	end
	config.vm.define "arbiter" do |arbiter|
		arbiter.vm.box = "ubuntu/trusty64"
		arbiter.vm.network "public_network", ip:"192.168.1.190"
		arbiter.vm.provider :virtualbox do |vb|
			vb.customize ["modifyvm", :id, "--memory", "512"]
		end
	end
end
