

Vagrant.configure(2) do |config|

    SWIFT_VERSION = "swift-2.2-SNAPSHOT-2016-01-06-a"

    config.vm.box = "ubuntu/wily64"
    config.vm.network :forwarded_port, guest: 8181, host: 8181
    config.vm.provision "shell", inline: <<-SHELL

    echo "*** Installing dependencies ***"
    # sudo apt-get update
    sudo apt-get install git cmake ninja-build clang uuid-dev libicu-dev icu-devtools libbsd-dev libedit-dev libxml2-dev swig libpython-dev libncurses5-dev pkg-config libssl-dev libevent-dev libsqlite3-dev

    echo "*** Installing Swift ***"
    cd /home/vagrant/
    wget https://swift.org/builds/ubuntu1510/#{SWIFT_VERSION}/#{SWIFT_VERSION}-ubuntu15.10.tar.gz
    tar -zxvf #{SWIFT_VERSION}-ubuntu15.10.tar.gz
    mv #{SWIFT_VERSION}-ubuntu15.10 swift
    echo "export PATH=/home/vagrant/swift/usr/bin:\"${PATH}\"" >> /home/vagrant/.bashrc
    sudo chown -R vagrant /home/vagrant/swift/

    echo "*** Installing Perfect ***"
    rm -rf /vagrant/Perfect
    cd /vagrant && git clone https://github.com/PerfectlySoft/Perfect.git
    cd /vagrant/Perfect/PerfectLib
    make
    sudo make install
    cd /vagrant/Perfect/PerfectServer
    make
    sudo rm -r /usr/local/bin/perfectserverfcgi 2> /dev/null
    sudo ln -s /vagrant/Perfect/PerfectServer/perfectserverfcgi /usr/local/bin/perfectserverfcgi
    sudo rm -r /usr/local/bin/perfectserverhttp 2> /dev/null
    sudo ln -s /vagrant/Perfect/PerfectServer/perfectserverhttp /usr/local/bin/perfectserverhttp
  SHELL
end
