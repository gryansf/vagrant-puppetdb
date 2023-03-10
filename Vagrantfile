# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "ubuntu/focal64"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
    vb.memory = "8192"
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-EOF
     export DEBIAN_FRONTEND=noninteractive
     test -f /tmp/puppet6-release-focal.deb 2>/dev/null || sudo curl -s -o /tmp/puppet6-release-focal.deb https://apt.puppetlabs.com/puppet6-release-focal.deb
     sudo dpkg -i /tmp/puppet6-release-focal.deb
     sudo apt-get update
     sudo dpkg -l puppet-agent 2>/dev/null || sudo apt-get install -y puppet-agent
     sudo /opt/puppetlabs/puppet/bin/puppet module install theforeman-puppet --version 16.5.0 --target-dir /tmp
     sudo /opt/puppetlabs/puppet/bin/puppet module install puppetlabs-puppetdb --version 7.12.0 --target-dir /tmp
     sudo /opt/puppetlabs/puppet/bin/puppet resource package puppetdb ensure=latest
     sudo /opt/puppetlabs/puppet/bin/puppet resource package puppetdb-termini ensure=latest
     sudo /opt/puppetlabs/puppet/bin/puppet resource package puppetserver ensure=latest
     sudo /opt/puppetlabs/puppet/bin/puppet resource package ruby ensure=latest
     sudo apt-get update
     sudo dpkg -l postgresql-contrib 2>/dev/null || sudo apt-get install -y postgresql postgresql-contrib
     sudo /opt/puppetlabs/puppet/bin/puppet apply -e "class { 'puppet': server_foreman => false, server => true, server_ca => true, server_crl_enable => true, server_ca_auth_required => true, server_ca_allow_sans => true, server_ca_enable_infra_crl => true, server_ca_allow_auth_extensions => true, server_ca_crl_sync => true, server_ca_client_whitelist => ['localhost'], dns_alt_names => ['puppet'], server_reports => store, server_jvm_extra_args => ['-Djava.net.preferIPv4Stack=true'], server_external_nodes => ''}" --modulepath /tmp
     sudo test -f /etc/puppetlabs/puppetdb/ssl/ca.pem 2>/dev/null || sudo /opt/puppetlabs/bin/puppetdb ssl-setup -f
     sudo /opt/puppetlabs/puppet/bin/puppet apply -e "class { 'puppetdb': listen_address => '0.0.0.0', ssl_set_cert_paths => true, ssl_deploy_certs => false, ssl_key => 'file:///etc/puppetlabs/puppet/ssl/private_keys/%{trusted.certname}.pem', ssl_cert => 'file:///etc/puppetlabs/puppet/ssl/certs/%{trusted.certname}.pem', ssl_ca_cert => 'file:///etc/puppetlabs/puppet/ssl/certs/ca.pem', manage_firewall => false, merge_default_java_args => true, java_args => {'-Djava.net.preferIPv4Stack' => '=true'}}" --modulepath /tmp
     ipaddress=$(/opt/puppetlabs/puppet/bin/facter ipaddress)
     fqdn=$(/opt/puppetlabs/puppet/bin/facter fqdn)
     sudo sed -i "/^127.0.1.1/d" /etc/hosts
     sudo echo -e "${ipaddress}\t${fqdn}\tpuppetdb\tpuppet" >> /etc/hosts
     sudo /opt/puppetlabs/puppet/bin/puppet agent -t
     sudo /opt/puppetlabs/puppet/bin/puppet apply -e "class { 'puppetdb::master::config': enable_reports => true, enable_storeconfigs => true, restart_puppet => true, manage_routes => true, manage_config => true, manage_storeconfigs => true, manage_report_processor => true}" --modulepath /tmp
     sudo mkdir -p /root/.puppetlabs/client-tools
     sudo gem install --bindir /opt/puppetlabs/bin puppetdb_cli
     sudo /opt/puppetlabs/puppet/bin/puppet apply -e '$puppetdb = { "puppetdb" => { "server_urls" => [ "https://${fqdn}:8081" ], "cacert" => "/etc/puppetlabs/puppet/ssl/certs/ca.pem", "cert" => "/etc/puppetlabs/puppet/ssl/certs/${fqdn}.pem", "key" => "/etc/puppetlabs/puppet/ssl/private_keys/${fqdn}.pem" } }; file { "/root/.puppetlabs/client-tools/puppetdb.conf": ensure => present, content => $puppetdb.to_json() }' --modulepath /tmp
     sudo /opt/puppetlabs/puppet/bin/puppet apply -e "notify { 'DEBUG puppetdb reports': }" --debug
     echo 'Type "vagrant ssh" to gain an interactive shell; then "sudo su -" to elevate privilege. As root, execute: "puppet-db status"'
  EOF
end
