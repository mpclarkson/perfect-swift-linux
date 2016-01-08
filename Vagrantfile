

Vagrant.configure(2) do |config|

    SWIFT_VERSION = "swift-2.2-SNAPSHOT-2016-01-06-a"

    config.vm.box = "ubuntu/wily64"
    config.vm.network :forwarded_port, guest: 8181, host: 8181
    config.vm.provision "shell", inline: <<-SHELL

    echo "*** Installing dependencies ***"
    sudo apt-get --assume-yes install git cmake ninja-build clang uuid-dev libicu-dev icu-devtools libbsd-dev libedit-dev libxml2-dev swig libpython-dev libncurses5-dev pkg-config libssl-dev libevent-dev libsqlite3-dev

    echo "*** Installing Swift ***"
    cd /home/vagrant/
    echo "* Downloading "#{SWIFT_VERSION}"..."
    wget https://swift.org/builds/ubuntu1510/#{SWIFT_VERSION}/#{SWIFT_VERSION}-ubuntu15.10.tar.gz --progress=bar:force
    echo "* Unpacking swift..."
    tar -zxvf #{SWIFT_VERSION}-ubuntu15.10.tar.gz &> /dev/null
    rm -rf swift
    mv #{SWIFT_VERSION}-ubuntu15.10 swift
    echo "* Adding swift to PATH..."
    echo "export PATH=/home/vagrant/swift/usr/bin:\"${PATH}\"" >> /home/vagrant/.bashrc
    sudo chown -R vagrant /home/vagrant/swift/

    echo "*** Downloading Perfect ***"
    rm -rf /vagrant/Perfect
    cd /vagrant && git clone https://github.com/PerfectlySoft/Perfect.git &> /dev/null

    echo "* Making PerfectLib... "
    cd /vagrant/Perfect/PerfectLib
    make &> /dev/null
    sudo make install &> /dev/null

    echo "* Making PerfectServer..."
    cd /vagrant/Perfect/PerfectServer
    make &> /dev/null

    echo "* Symlinking... ***"
    sudo rm -r /usr/local/bin/perfectserverfcgi 2> /dev/null
    sudo ln -s /vagrant/Perfect/PerfectServer/perfectserverfcgi /usr/local/bin/perfectserverfcgi
    sudo rm -r /usr/local/bin/perfectserverhttp 2> /dev/null
    sudo ln -s /vagrant/Perfect/PerfectServer/perfectserverhttp /usr/local/bin/perfectserverhttp

    echo "*** Building Perfect Examples ***"
    echo "* Making Authenticator..."
    cd /vagrant/Perfect/Examples/Authenticator && make &> /dev/null
    echo "* Making Tap Tracker..."
    cd /vagrant/Perfect/Examples/Tap\\ Tracker && make &> /dev/null
    echo "* Making Upload Enumerator..."
    cd /vagrant/Perfect/Examples/Upload\\ Enumerator && make &> /dev/null
    echo "* Making Upload Websockets Server..."
    cd /vagrant/Perfect/Examples/Websockets\\ Server && make &> /dev/null
    echo "* URL Routing..."
    cd /vagrant/Perfect/Examples/URL\\ Routing && make &> /dev/null

    echo "* Moving Libraries and Templates... "
    find /vagrant/Perfect/Examples/ -name "*.so" | xargs -i cp {} /vagrant/PerfectLibraries/
    find /vagrant/Perfect/Examples/ -name "*.mustache" | xargs -i cp {} /vagrant/webroot/

    echo "*** DONE ***"
  SHELL
end
