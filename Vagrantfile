# - set ft=ruby - 

Vagrant.configure("2") do |config|
	config.vm.box = "debian/jessie64"

	##
	# Criacao da maquina DevOps, responsavel pelo ambiente
	# de desenvolvimento e orquestracao
	config.vm.define "devops" do |devops|
		devops.vm.network "private_network", ip: '192.168.200.50'

		devops.vm.network "forwarded_port", guest: 8080, host: 8080
		devops.vm.network "forwarded_port", guest: 8090, host: 8090
		devops.vm.network "forwarded_port", guest: 22, host: 2201

		devops.vm.provider "virtualbox" do |vb|
			vb.cpus = "1"
			vb.memory = "2048"
			vb.name = "devops"
		end

		devops.vm.provision "shell", path: "tools/install_tools"
	end

	##
	# criacao da maquina Docker, responsavel pelo ambiente
	# de container do curso
	config.vm.define "docker" do |docker|
		docker.vm.network "private_network", ip: '192.168.200.100'

		docker.vm.network "forwarded_port", guest: 22, host: 2202
		docker.vm.network "forwarded_port", guest: 80, host: 8000
		docker.vm.network "forwarded_port", guest: 443, host: 8443
		docker.vm.network "forwarded_port", guest: 8001, host: 8001
		docker.vm.network "forwarded_port", guest: 8002, host: 8002
		docker.vm.network "forwarded_port", guest: 8003, host: 8003

		docker.vm.provider "virtualbox" do |vb|
			vb.cpus = "1"
			vb.memory = "2048"
			vb.name = "docker"
		end

		docker.vm.provision "shell", path: "tools/install_tools"
	end
end
