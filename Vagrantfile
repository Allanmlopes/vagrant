# Maquina CentOS
Vagrant.configure("2") do |config|
  config.vm.define "centos" do |centos|
    centos.vm.box = "generic/centos8"
    centos.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.customize ["createhd", "--filename", "centos_disk.vdi", "--size", 40960]
      vb.customize ["storageattach", :id, "--storagectl", "SATA Controller", "--port", 1, "--device", 0, "--type", "hdd", "--medium", "centos_disk.vdi"]
    end
  end

  # Máquina Ubuntu
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "hashicorp/bionic64"
    ubuntu.vm.network "forwarded_port", guest: 80, host: 8080
    ubuntu.vm.network "public_network", ip: "192.168.1.55"
    ubuntu.vm.provision "shell", path: "./scripts_provision/script.sh"
    ubuntu.vm.synced_folder "site/", "/var/www/html"
    ubuntu.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.customize ["createhd", "--filename", "ubuntu_disk.vdi", "--size", 40960]
      vb.customize ["storageattach", :id, "--storagectl", "SATA Controller", "--port", 1, "--device", 0, "--type", "hdd", "--medium", "ubuntu_disk.vdi"]
    end
  end
  
  # Maquina Windows
  config.vm.define "windows" do |windows|
    windows.vm.box = "gusztavvargadr/windows-10"
    windows.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.customize ["createhd", "--filename", "windows_disk.vdi", "--size", 40960]
      vb.customize ["storageattach", :id, "--storagectl", "SATA Controller", "--port", 1, "--device", 0, "--type", "hdd", "--medium", "windows_disk.vdi"]
    end
  end
end
