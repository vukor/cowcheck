VAGRANTFILE_API_VERSION = "2"

$bootstrap=<<SCRIPT
curl https://releases.rancher.com/install-docker/18.06.sh | sh
apt install make -y
usermod -a -G docker vagrant
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision :shell, inline: $bootstrap

  # Uses the host keys for pulling repos from bitbucket
  config.ssh.forward_agent = true

  # Sync the repos that actually do the deploys
  config.vm.synced_folder ".", "/home/vagrant/cowcheck"
end