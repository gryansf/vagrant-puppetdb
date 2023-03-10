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
Watch for the PuppetDB report status, which should look something like
```
    default: Debug: Processing report from ubuntu-focal.internal.salesforce.com with processor Puppet::Reports::Puppetdb
    default: Debug: Using cached connection for https://ubuntu-focal.internal.salesforce.com:8081
    default: Debug: HTTP POST https://ubuntu-focal.internal.salesforce.com:8081/pdb/cmd/v1?checksum=5cb8edcb0cd7fc9ebbd0cf7907f22eba3244f034&version=8&certname=ubuntu-focal.internal.salesforce.com&command=store_report&producer-timestamp=2023-03-10T04:57:25.841Z returned 200 OK
    default: Debug: Caching connection for https://ubuntu-focal.internal.salesforce.com:8081
    default: Info: 'store_report' command for ubuntu-focal.internal.salesforce.com submitted to PuppetDB with UUID b7023a70-3733-4d2a-8e10-c86b5908c923
    default: Debug: Closing connection for https://ubuntu-focal.internal.salesforce.com:8081
```
After vagrant brings up the VM, install and configure puppetdb-cli 
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
