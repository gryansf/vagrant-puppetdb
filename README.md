# vagrant-puppetdb
Bootstrap Puppetserver and PuppetDB with Puppet on Ubuntu Linux 20.04 LTS (Focal Fossa)

Setup
-----

*MacOS Requirements*
- [https://brew.sh](https://docs.brew.sh/Installation)
- brew cask install virtualbox
- brew cask install vagrant

*Other Operating Systems*
- [https://www.virtualbox.org/](https://www.virtualbox.org/wiki/Downloads)
- [http://www.vagrantup.com/](https://developer.hashicorp.com/vagrant/downloads)

Runtime
-------
```
$ git clone https://github.com/gryansf/vagrant-puppetdb.git
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

Puppet modules
--------------
- theforeman-puppet (v16.5.0)
- puppet-extlib (v6.2.0)
- puppet-systemd (v4.0.1)
- puppetlabs-inifile (v5.4.0)
- puppetlabs-concat (v7.3.2)
- puppetlabs-stdlib (v8.5.0)
- puppetlabs-puppetdb (v7.12.0)
- puppetlabs-firewall (v3.6.0)
- puppetlabs-postgresql (v8.2.1)
- puppetlabs-apt (v9.0.1)
- puppetlabs-stdlib (v8.5.0)
- puppetlabs-host_core (v1.2.0)

More here
---------
- https://www.puppet.com/docs/puppetdb/6/pdb_client_tools.html
- https://github.com/puppetlabs/puppetdb-cli
- https://www.puppet.com/docs/puppetdb/6/api/query/tutorial.html
