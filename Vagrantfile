Vagrant.configure("2") do |config|
  config.vm.box = "generic/centos9s"

  config.vm.network "forwarded_port", guest: 80, host: 8888

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 2
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo yum install -y epel-release
    sudo yum install -y nginx
    sudo setenforce 0
    sudo sed -ie 's/^SELINUX=.*$/SELINUX=disabled/' /etc/selinux/config
    cat /etc/selinux/config
    sudo systemctl start nginx
    sudo systemctl enable nginx
    sudo systemctl disable firewalld
    sudo systemctl stop firewalld
  SHELL
end