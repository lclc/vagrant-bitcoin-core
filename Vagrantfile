Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.network "forwarded_port", guest: 8333, host: 8333, protocol: 'tcp'
  config.vm.network "forwarded_port", guest: 8332, host: 8332, protocol: 'tcp'
  
  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    #v.cpus = 2
  end

  config.vm.provision "shell", privileged: false, inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y git
    sudo apt-get install -y build-essential
    sudo apt-get install -y libtool
    sudo apt-get install -y autotools-dev
    sudo apt-get install -y autoconf
    sudo apt-get install -y pkg-config
    sudo apt-get install -y libssl-dev
    sudo apt-get install -y libevent-dev
    sudo apt-get install -y libboost-all-dev

    git clone https://github.com/bitcoin/bitcoin.git
    cd bitcoin
    ./autogen.sh
    ./configure --disable-tests --disable-wallet
    make
    sudo make install
    
    mkdir /home/vagrant/.bitcoin
    ln -s /vagrant/bitcoin /home/vagrant/.bitcoin
    chown -R vagrant:vagrant /home/vagrant/.bitcoin
    
    su vagrant
    bitcoind -daemon
  SHELL
end
