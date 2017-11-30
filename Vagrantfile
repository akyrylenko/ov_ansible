Vagrant.configure(2) do |config|
  config.vm.define 'provisioner' do |pr|
    pr.vm.box = 'ubuntu/xenial64'

    pr.vm.provision 'shell', inline: <<-SHELL
      sudo apt-get update
      sudo apt-get -y install software-properties-common
      sudo apt-add-repository ppa:ansible/ansible
      sudo apt-get update
      sudo apt-get -y install ansible
      sudo apt-get -y install python-passlib
      sudo ansible-galaxy install rvm_io.ruby
    SHELL

    pr.vm.network 'private_network', ip: '192.168.33.10'
  end

  config.vm.define 'web' do |web|
    web.vm.box = 'ubuntu/xenial64'

    web.vm.provision 'shell', inline: <<-SHELL 
      sudo sed -i 's/^PermitRootLogin prohibit-password/PermitRootLogin yes/g' /etc/ssh/sshd_config
      sudo service sshd restart
    SHELL

    web.vm.network 'private_network', ip: '192.168.33.11'
  end
end
