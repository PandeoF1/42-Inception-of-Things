Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.network "private_network", ip: "192.168.56.110"
  config.vm.define "server" do |server|
    server.vm.hostname = "tnardS"
    server.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = "1"
    end
    server.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y apt-transport-https curl
      curl -sfL https://get.k3s.io | K3S_NODE_NAME=server INSTALL_K3S_EXEC="server" sh -
    SHELL
  end
  config.vm.define "serverworker" do |serverworker|
    serverworker.vm.hostname = "tnardSW"
    serverworker.vm.network "private_network", ip: "192.168.56.111"
    serverworker.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
      vb.cpus = "1"
    end
    serverworker.vm.provision "shell", inline: <<-SHELL
      sudo apt-get update
      sudo apt-get install -y apt-transport-https curl
      curl -sfL https://get.k3s.io | K3S_NODE_NAME=serverworker K3S_URL=https://192.168.56.110:6443 K3S_TOKEN=changeme sh -
    SHELL
  end
end
