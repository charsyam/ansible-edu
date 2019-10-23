$script = <<SCRIPT
sudo apt-get -y update
sudo apt-get -y install build-essential python3-pip 
sudo pip3 install --upgrade pip3
sudo pip3 install ansible
cd /vagrant
sudo mkdir -p /home/vagrant/.ssh
sudo cp /vagrant/id_rsa_vagrant /home/vagrant/.ssh/
sudo chown -R vagrant:vagrant /home/vagrant/.ssh
sudo useradd -d /home/charsyam charsyam
sudo groupmod -g 9999 input
sudo mkdir -p /home/charsyam/.ssh
sudo echo "charsyam ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
sudo chown -R charsyam:charsyam /home/charsyam/.ssh
sudo cat > /home/charsyam/.ssh/authorized_keys << EOF
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC0EwL4G49IG9yVa18hrgwfmWhI/o1+qE+2yyHOAxwNzFRIi2eA5yFVC1z7uQOnS9Y7s0Cx+F5ZMcIynYL/NZI1fWMaabffmeaJjJcrneBwhafO99g/NXDcxrzjJyhMfUJzAY6eAfi7Ep6AIir69j5e+Uyu9Y2aS+VcsW2TAzXbMKVX5LxY278yYczEYMpF6B2nYQTWxjF7jbuuiS0DSLdABdEQxiSCrWpSEPQG/oiXFhb7wZivMvyDxYETPiSyoZVK1TyCtD91KYFnzE0Se12NN4yA3X1jGMEHYoslkY6jLYP7otGMuZtCBaMoebEb4b2BwHXJC0sbW7SUfSij4YD4PyJHcqqlxsGSeNlMyrACWl1PeA+QyQ9zDz1/ANoT5lPAGOxHWoKD1SHZXXsNL6TiZZFbYnsF1i8f0eVB+hh3qgNmtj0ySnUoxawUEKJqIiSqwMSUyOQDYMTpEKU8Wbp7peOcLbKf/iKBN89jUYlF882rt8mAfB8HY8D5d6dYA17kZgFLvBWcToYczgbFrM6uxxhmzgoj0M7CoyZQZ5Txhh54igVovMC8su6lXDrq340XnkrxlkWrpzEP2ESBwBtLE+7SaHTh0bWEKszNnyhv8MJpGzoTPJRlg40fR7YkU/nvlTgJ8QCkCiif3j32O0pN1TBsIsIGFoaeUrri1t54ZQ== charsyam@charsyam
EOF
SCRIPT
 
Vagrant.configure(2) do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end
  config.vm.define "vm1" do |vm1|
    vm1.vm.box = "bento/ubuntu-18.04"
    vm1.vm.network :private_network, ip: "192.168.50.5"
    vm1.vm.provision "shell", inline: $script
  end
end
