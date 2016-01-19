Vagrant.configure("2") do |config|
    SWIFT_VERSION = "swift-2.2-SNAPSHOT-2016-01-06-a"

    # wget https://swift.org/builds/ubuntu1510/swift-2.2-SNAPSHOT-2016-01-06-a/swift-2.2-SNAPSHOT-2016-01-06-a-ubuntu15.10.tar.gz
# tar -zxvf swift-2.2-SNAPSHOT-2016-01-06-a-ubuntu15.10.tar.gz &> /dev/null
    config.vm.define :"perfect-swift-linux" do |config|
        config.vm.provider "virtualbox" do |v|
          v.name = "perfect-swift-linux"
        end

        config.vm.box = "ubuntu/wily64"
        config.vm.network :forwarded_port, guest: 8181, host: 8181
        config.vm.provision "shell", inline: <<-SHELL

        echo "*** Installing dependencies ***"
        sudo apt-get --assume-yes install git clang libicu-dev libssl-dev libevent-dev libsqlite3-dev

        echo "*** Installing Swift ***"
        cd /home/vagrant/
        echo "* Downloading "#{SWIFT_VERSION}"..."
        wget https://swift.org/builds/ubuntu1510/#{SWIFT_VERSION}/#{SWIFT_VERSION}-ubuntu15.10.tar.gz --progress=bar:force
        echo "* Unpacking swift..."
        tar -zxvf #{SWIFT_VERSION}-ubuntu15.10.tar.gz &> /dev/null
        rm -rf swift
        mv #{SWIFT_VERSION}-ubuntu15.10 swift

        echo "* Adding Swift to PATH"
        sudo chown -R vagrant:vagrant /home/vagrant/swift/
        [ -f /home/vagrant/.profile ] || touch /home/vagrant/.profile
        grep 'PATH=/home/vagrant/swift/usr/bin' /home/vagrant/.profile || echo 'export PATH=/home/vagrant/swift/usr/bin:$PATH' | tee -a /home/vagrant/.profile

        echo "*** Downloading Perfect ***"
        rm -rf /vagrant/Perfect
        cd /vagrant && git clone https://github.com/PerfectlySoft/Perfect.git

        echo "* Making PerfectLib... "
        cd /vagrant/Perfect/PerfectLib && make && sudo make install

        echo "* Making PerfectServer..."
        cd /vagrant/Perfect/PerfectServer && make

        echo "* Symlinking..."
        sudo rm -r /usr/local/bin/perfectserverfcgi 2> /dev/null
        sudo ln -s /vagrant/Perfect/PerfectServer/perfectserverfcgi /usr/local/bin/perfectserverfcgi
        sudo rm -r /usr/local/bin/perfectserverhttp 2> /dev/null
        sudo ln -s /vagrant/Perfect/PerfectServer/perfectserverhttp /usr/local/bin/perfectserverhttp

        echo "*** Building Perfect Examples ***"
        echo "* Making Authenticator..."
        cd /vagrant/Perfect/Examples/Authenticator && make
        echo "* Making Tap Tracker..."
        cd /vagrant/Perfect/Examples/Tap\\ Tracker && make
        echo "* Making Upload Enumerator..."
        cd /vagrant/Perfect/Examples/Upload\\ Enumerator && make
        echo "* Making Upload Websockets Server..."
        cd /vagrant/Perfect/Examples/Websockets\\ Server && make
        echo "* Making URL Routing..."
        cd /vagrant/Perfect/Examples/URL\\ Routing && make

        echo "* Moving Libraries and Templates... "
        mkdir -p /vagrant/PerfectLibraries/
        find /vagrant/Perfect/Examples/ -name "*.so" | xargs -i cp {} /vagrant/PerfectLibraries/
        find /vagrant/Perfect/Examples/ -name "*.mustache" | xargs -i cp {} /vagrant/webroot/

        echo "*** DONE ***"
        SHELL
    end
end
