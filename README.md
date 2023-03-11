# vagrant-puppetdb
Bootstrap Puppetserver and PuppetDB with Puppet on Ubuntu Linux 20.04 LTS (Focal Fossa)

Setup
-----

*MacOS Requirements*
- [https://brew.sh](https://docs.brew.sh/Installation)
```
$ brew cask install virtualbox
$ brew cask install vagrant
```

*Other Operating Systems*
- You will need a hypervisor. Options are [https://www.virtualbox.org/](https://www.virtualbox.org/wiki/Downloads)
- [http://www.vagrantup.com/](https://developer.hashicorp.com/vagrant/downloads)

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
