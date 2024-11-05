<h1> Vagrant </h1>

Configuração do Ambiente com Vagrant

Este projeto utiliza o Vagrant para criar e configurar um ambiente de desenvolvimento com máquinas virtuais CentOS 8 e Ubuntu Bionic 64. Abaixo estão as descrições das configurações para cada máquina.
Arquivo Vagrantfile

O arquivo Vagrantfile define as máquinas virtuais, as boxes utilizadas, redes e configurações de provisionamento. O código está organizado para configurar uma máquina CentOS e uma máquina Ubuntu, com as seguintes especificações:


#ruby

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

<h2>Explicação das Configurações</h2>
<h3>Configuração Geral</h3>

   Versão de Configuração: "2" - Define a versão do Vagrantfile para compatibilidade com versões mais recentes do Vagrant.
   Define: Cada máquina virtual é configurada individualmente usando o método config.vm.define, que permite nomear e configurar cada VM separadamente.

<h3>Máquina Virtual CentOS</h3>

   Nome: "centos" - Nome da máquina virtual, usado para identificá-la.
   Box: generic/centos8 - A box do CentOS 8 é usada para criar o ambiente CentOS.

<h3>Máquina Virtual Ubuntu </h3>

    Nome: "ubuntu" - Nome da máquina virtual, usado para identificá-la.
    Box: hashicorp/bionic64 - A box do Ubuntu Bionic 64 (Ubuntu 18.04) é usada para criar o ambiente Ubuntu.
    Redirecionamento de Porta:
        guest: 80, host: 8080 - Redireciona a porta 80 da máquina virtual para a porta 8080 do host, permitindo o acesso ao servidor web do guest (Ubuntu) via localhost:8080 no host.
    Configuração de Rede Pública:
        public_network e ip: "192.168.1.55" - Define um IP fixo (192.168.1.55) para a máquina Ubuntu, acessível pela rede pública.
    Provisionamento de Script:
        ubuntu.vm.provision "shell", path: "./scripts_provision/script.sh" - Executa um script shell (localizado em ./scripts_provision/script.sh) para configurar automaticamente o ambiente dentro da VM Ubuntu durante a criação. Esse script pode instalar pacotes, configurar serviços, etc.
    Sincronização de Pasta:
        ubuntu.vm.synced_folder "site/", "/var/www/html" - Sincroniza o diretório site/ do host com o diretório /var/www/html no guest, permitindo o compartilhamento de arquivos entre o host e a máquina virtual.

Essas configurações automatizam a criação e o provisionamento do ambiente, garantindo que ambas as máquinas estejam prontas para o desenvolvimento ou testes assim que iniciadas com o comando vagrant up.
