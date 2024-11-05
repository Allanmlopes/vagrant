    # Maquina CentOS
Vagrant.configure("2") do |config|
    config.vm.define "centos" do |centos|
      config.vm.box = "generic/centos8"
    end
  
    # Máquina Ubuntu
    config.vm.define "ubuntu" do |ubuntu|
      ubuntu.vm.box = "hashicorp/bionic64"
      ubuntu.vm.network "forwarded_port", guest: 80, host: 8080
      ubuntu.vm.network "public_network", ip: "192.168.1.55"
      ubuntu.vm.provision "shell", path: "./scripts_provision/script.sh"
      ubuntu.vm.synced_folder "site/", "/var/www/html"
    end
end
  
