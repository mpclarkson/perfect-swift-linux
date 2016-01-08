#Swift and Perfect Server on Linux with Vagrant

##Introduction

This is `Vagrantfile` that builds a Ubuntu 15.10 virtual machine with open source [Swift](http://swift.org) and the Swift server [Perfect](https://github.com/PerfectlySoft/Perfect).

I'm far from a Vagrant specialist and welcome any PRs!

##Instructions

###Installation

1. Ensure you have [Vagrant](https://www.vagrantup.com) configured.
2. Clone this repository:
`git clone https://github.com/mpclarkson/perfect-swift-ubuntu`
3. Open the folder:
`cd perfect-swift-linux`
4. Install the virtual machine:
`vagrant up`
5. SSH into it:
`vagrant ssh`
6. Start the PerfectServer:
`cd /vagrant && perfectserverhttp`

###PerfectServer Examples

All of the [Examples](https://github.com/PerfectlySoft/Perfect/tree/master/Examples) are built and are accessible at http://127.0.0.1:8181/

###Swift REPL

You can access the swift REPL simply by typing `swift`

##Author

By [Matthew Clarkson](http://mpclarkson.github.io/) from [Hilenium](http://hilenium.com). Tweet me [@matt_clarkson](https://twitter.com/matt_clarkson)
