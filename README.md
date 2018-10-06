janusgw-vagrant
===============

This project spins up a virtual machine with a preconfigured instance of the
`meetecho/janus-gateway` WebRTC signaling server. This VM can be used to develop
applications requiring WebRTC functionality.

There are many plugins available to try! [Please check out the docs!](https://janus.conf.meetecho.com/docs/)

## Usage

### Quick Start
To get started using this VM, please install Vagrant and VirtualBox first to
the host. After you have verified everything is working as intended, clone this
repository and run `vagrant up` in the cloned directory.

### Step by Step
1. Download and install VirtualBox for your development platform:
   [Download VirtualBox](https://www.virtualbox.org/wiki/Downloads)

2. Download and install Vagrant:
   [Download Vagrant](https://www.vagrantup.com/downloads.html)

3. Clone this repository to a well known directory:
   `git clone https://github.com/shadoxx/janusgw-vagrant`

4. `cd janusgw-vagrant/` and run `vagrant up`

5. Wait a little while. Depending on your internet connection, bringing up the
   VM could take as long as 15 minutes. Get up. Stretch your legs. How long have
   you been sitting at your computer?

6. Once completed, a basic web management interface with API demos will be available
   at http://localhost:8080/index.html. The password for the Admin API is: `janusoverlord`

7. To SSH into the newly created VM, just type `vagrant ssh`.

8. To start from scratch, run `vagrant destroy -f; vagrant up` in the cloned
   repository. YOUR VM WILL BE DESTROYED AND RECREATED!

## Appendix
### A. Ports
This VM has the following services listening on the corresponding ports:

| Guest Port | Host Port | Service |
| ----------:| ---------:|:-------:|
| 3478       | 3478      | coturn    |
| 7088       | 7088      | admin api |
| 8088       | 8088      | janus api |
|   80       | 8080      | nginx     |

### B. Customized Configurations
All files located in the `provision/conf/janus` directory in this repository
are copied to `/etc/janus` in the VM on first run. If you would like your own
configurations included (ie, for different transports), please drop your configs
into `provision/conf/janus`.

### C. SSL Certificate for `localhost`
The first time you run `vagrant up`, a unique SSL certificate generated for
localhost can be found in `/vagrant/cache/ssl`. This is meant to be used only
for development and is explicitly ignored in .gitignore.

By default, it is not used. SSL support via automated configuration is planned
in a later revision of this VM. For now, please find instructions for enabling
SSL support in the official `janus-gateway` docs. Configuration files are also
heavily commented.

### D. Build Caching
To save on bandwidth, all cloned repos and most generated files are downloaded to `/vagrant/cache` on first run, and then pulled from that location on each
subsequent run. This directory is explicitly ignored in the Git repo, so it's
safe to put things there that you don't want to be deleted between `vagrant destroy`
and `vagrant up`.

### E. Networking
Earlier revisions of this VM used host->port mapping on the host for networking
services. This complicated things in ways that don't make sense, especially in the
context of STUN/TURN. This VM is now configured to pull an IP via DHCP from the host
'public network' as configured in the Vagrantfile. More advanced network
configurations are possible, but they will not be covered in this project outside
of the preconfigured simple scenario. Refer to Appendix A for a list of open/listening
ports in this VM and work your development security strategy accordingly.
