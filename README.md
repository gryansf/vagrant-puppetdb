# vagrant-puppetdb
Bootstrap Puppetserver and PuppetDB with Puppet on Ubuntu Linux 20.04 LTS (Focal Fossa) 

MacOS Requirements
- brew cask install virtualbox
- brew cask install vagrant

Others
- [https://www.virtualbox.org/](https://www.virtualbox.org/wiki/Downloads)
- [http://www.vagrantup.com/](https://developer.hashicorp.com/vagrant/downloads)

```
$ git clone https://github.com/gryansf/vagrant-puppetdb.git
$ cd vagrant-puppetdb
$ vagrant up
```
Once vagrant brings up the VM, install and configure puppetdb-cli 
```
$ vagrant ssh
$ # sudo su -
$ # apt-get install -y ruby
$ # gem install --bindir /opt/puppetlabs/bin puppetdb_cli
$ # mkdir -p $HOME/.puppetlabs/client-tools
$ # touch $HOME/.puppetlabs/client-tools/puppetdb.conf
```

Place the following into the puppetdb.conf file we created above:
```
  {
    "puppetdb" : {
      "server_urls" : [
        "https://ubuntu-focal.internal.salesforce.com:8081"
      ],
      "cacert" : "/etc/puppetlabs/puppet/ssl/certs/ca.pem",
      "cert" : "/etc/puppetlabs/puppet/ssl/certs/ubuntu-focal.internal.salesforce.com.pem",
      "key" : "/etc/puppetlabs/puppet/ssl/private_keys/ubuntu-focal.internal.salesforce.com.pem"
    }
  }
```
Finally, run:
```
$ # puppet-query 'nodes[certname]{}'
$ # puppet-db status
```
Check out more here: https://github.com/puppetlabs/puppetdb-cli
