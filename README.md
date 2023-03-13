# vagrant-puppetdb
Bootstrap Puppetserver and PuppetDB with Puppet on Ubuntu Linux 20.04 LTS (Focal Fossa)

Setup
-----
*General Requirements*
- You will need [Vagrant](https://developer.hashicorp.com/vagrant/docs/installation)
- Vagrant's out-of-box options for hypervisor support include [VirtualBox, Hyper-V, and Docker](https://developer.hashicorp.com/vagrant/docs/providers) 
- [VMware](https://developer.hashicorp.com/vagrant/docs/providers/vmware/vagrant-vmware-utility) support comes in the form of an installable plugin

*MacOS (Intel) Requirements*
- [https://brew.sh](https://docs.brew.sh/Installation)
```
$ brew cask install virtualbox
$ brew cask install vagrant
```
*Clone the repo to your local system*
```
$ git clone https://github.com/gryansf/vagrant-puppetdb.git
```

Build
-------
```
$ cd vagrant-puppetdb
$ vagrant up
```

Post-config
-----------------
```
$ vagrant ssh
$ # sudo su -
$ # puppet-query 'nodes[certname]{}'
$ # puppet-db status
```

More here
---------
- https://www.puppet.com/docs/puppetdb/6/pdb_client_tools.html
- https://github.com/puppetlabs/puppetdb-cli
- https://www.puppet.com/docs/puppetdb/6/api/query/tutorial.html
