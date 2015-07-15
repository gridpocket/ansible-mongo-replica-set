# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
	config.vm.define "db0" do |db0|
		db0.vm.box = "ubuntu/trusty64"
		db0.vm.network "public_network", ip:"192.168.1.200"
		db0.vm.provider :virtualbox do |vb|
			vb.customize ["modifyvm", :id, "--memory", "512"]
		end
	end
	config.vm.define "db1" do |db1|
		db1.vm.box = "ubuntu/trusty64"
		db1.vm.network "public_network", ip:"192.168.1.201"
		db1.vm.provider :virtualbox do |vb|
			vb.customize ["modifyvm", :id, "--memory", "512"]
		end
	end
	config.vm.define "db2" do |db2|
		db2.vm.box = "ubuntu/trusty64"
		db2.vm.network "public_network", ip:"192.168.1.202"
		db2.vm.provider :virtualbox do |vb|
			vb.customize ["modifyvm", :id, "--memory", "512"]
		end
	end
end
