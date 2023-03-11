# vagrant-puppetdb
Bootstrap Puppetserver and PuppetDB with Puppet on Ubuntu Linux 20.04 LTS (Focal Fossa)

Setup
-----

*MacOS (Intel) Requirements*
- [https://brew.sh](https://docs.brew.sh/Installation)
```
$ brew cask install virtualbox
$ brew cask install vagrant
```

*Other Operating Systems*
- You will need a [hypervisor](https://developer.hashicorp.com/vagrant/docs/providers) to run Vagrant. [VirtualBox](https://www.virtualbox.org/wiki/Downloads) has options, as does [VMware](https://developer.hashicorp.com/vagrant/downloads/vmware).
- Ultimately, you will need to be able to run [vagrant up](http://www.vagrantup.com/).

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
