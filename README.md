#Swift and Perfect on Linux using Vagrant!

##Introduction

This is `Vagrantfile` that builds a Ubuntu 15.10 virtual machine configured with open source [Swift](http://swift.org) and the Swift server [Perfect](https://github.com/PerfectlySoft/Perfect).

##Instructions

1. Ensure you have [Vagrant](https://www.vagrantup.com) configured.
2. Clone this repository:
`git clone https://github.com/mpclarkson/perfect-swift-ubuntu`
3. Open the folder:
`cd perfect-swift-linux`
4. Install the virtual machine:
`vagrant up`
5. SSH into it:
`vagrant ssh`:
6. Go to the directory that is shared with your local machine:
`cd /vagrant`
7. Start the Perfect server in the `vagrant` folder:
`perfectserverhttp`

##PerfectServer Example Applications

All of the [Examples](https://github.com/PerfectlySoft/Perfect/tree/master/Examples) are built and are accessible at http://127.0.0.1:8181/


##Author

By [Matthew Clarkson](http://mpclarkson.github.io/) [@matt_clarkson](https://twitter.com/matt_clarkson) from [Hilenium](http://hilenium.com). [@matt_clarkson](https://twitter.com/matt_clarkson)
