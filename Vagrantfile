Vagrant.configure(2) do |config|
  config.disksize.size = '400GB' # must do `vagrant plugin install vagrant-disksize`
  config.vm.box = "ubuntu/bionic64"

  config.vm.network "forwarded_port", guest: 8333, host: 8333 #mainnet
  #config.vm.network "forwarded_port", guest: 18333, host: 18333 #testnet

  config.vm.network "forwarded_port", guest: 8332, host: 8332 #mainnet RPC
  #config.vm.network "forwarded_port", guest: 18332, host: 18332 #testnet RPC

  #config.vm.network "public_network", ip: 192.168.1.201

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    sudo apt update && sudo apt -y upgrade
    sudo apt install -y snap
    sudo snap install bitcoin-core


    sudo apt-get install -y supervisor

    mkdir -p /home/vagrant/snap/bitcoin-core/common/.bitcoin/
    ln -s /vagrant/bitcoin.conf /home/vagrant/snap/bitcoin-core/common/.bitcoin/

    sudo ln -s /vagrant/bitcoin_supervisor.conf /etc/supervisor/conf.d
    sudo supervisorctl reread
    sudo supervisorctl update
  SHELL
end
