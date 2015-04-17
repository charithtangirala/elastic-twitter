# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  config.vm.box = "chef/centos-7.0"

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    sudo yum update
    sudo yum install -y java

    rpm --import https://packages.elasticsearch.org/GPG-KEY-elasticsearch
    sudo echo '[elasticsearch-1.5]\nname=Elasticsearch repository for 1.5.x packages\nbaseurl=http://packages.elasticsearch.org/elasticsearch/1.5/centos\ngpgcheck=1\ngpgkey=http://packages.elasticsearch.org/GPG-KEY-elasticsearch\nenabled=1' > /etc/yum.repos.d/elastic.repo
    yum install -y elasticsearch
    sudo /bin/systemctl daemon-reload
    sudo /bin/systemctl enable elasticsearch.service
    
    sudo /usr/share/elasticsearch/bin/plugin install elasticsearch/elasticsearch-river-twitter/2.5.0
  SHELL
  
  config.vm.network "forwarded_port", guest: 9200, host: 9200, protocol: 'tcp'
  config.vm.network "forwarded_port", guest: 9200, host: 9200, protocol: 'udp'
  config.vm.network "forwarded_port", guest: 9300, host: 9300, protocol: 'tcp'
  config.vm.network "forwarded_port", guest: 9300, host: 9300, protocol: 'udp'
end
