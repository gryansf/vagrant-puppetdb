# vagrant-puppetdb
Bootstrap Puppetserver and PuppetDB with Puppet on Ubuntu Linux 20.04 LTS (Focal Fossa)

Setup
-----

*MacOS Requirements*
- [https://brew.sh](https://docs.brew.sh/Installation)
```
$ brew cask install virtualbox
$ brew cask install vagrant
$ git clone https://github.com/gryansf/vagrant-puppetdb.git
```

*Other Operating Systems*
- [https://www.virtualbox.org/](https://www.virtualbox.org/wiki/Downloads)
- [http://www.vagrantup.com/](https://developer.hashicorp.com/vagrant/downloads)

Runtime
-------
```
$ cd vagrant-puppetdb
$ vagrant up
```

Post-installation
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
