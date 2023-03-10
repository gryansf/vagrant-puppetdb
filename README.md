# vagrant-puppetdb
Bootstrap Puppetserver with PuppetDB 
```
$ cd vagrant-puppetdb
$ vagrant up
```
Install puppetdb-cli 
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
```
