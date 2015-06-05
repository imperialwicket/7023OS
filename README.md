# Elasticsearch Indexing

These are [Vagrant](https://www.vagrantup.com/downloads.html) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads) resources for the Elasticsearch Indexing text. Once both are installed, you can use `vagrant up` to launch an Ubuntu 14.04 virtual machine that will update and install openjdk-7-jre (and dependencies) to get up and running quickly and easily.

## Getting Started

After installation, we must start the virtual machine. On the first launch, Vagrant will attempt to provision the machine using a very simple script embedded in the Vagrantfile. Some useful commands to keep in mind:

    - `vagrant up` - launch the default virtual machine configured in the local Vagrantfile
    - `vagrant ssh` - connect to the default virtual machine via ssh
    - `vagrant provision` - run the provisioner script/utility again manually
    - `vagrant halt` - shutdown the default virtual machine

More commands and documentation are available at [Vagrantup.com](https://docs.vagrantup.com/v2/getting-started/).
