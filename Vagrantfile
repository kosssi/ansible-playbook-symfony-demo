$HOSTNAME = "symfony.dev"
$BOX = "ubuntu/trusty64"
$IP = "88.88.88.88"
$MEMORY = ENV.has_key?('EASYFUTURE_VM_MEMORY') ? ENV['EASYFUTURE_VM_MEMORY'] : "2048"
$CPUS = ENV.has_key?('EASYFUTURE_VM_CPUS') ? ENV['EASYFUTURE_VM_CPUS'] : "2"
$EXEC_CAP = ENV.has_key?('EASYFUTURE_VM_EXEC_CAP') ? ENV['EASYFUTURE_VM_EXEC_CAP'] : "100"

Vagrant.configure("2") do |config|
  config.vm.hostname = $HOSTNAME
  config.vm.box = $BOX
  config.vm.network :private_network, ip: $IP

  config.vm.synced_folder "symfony", "/var/www/symfony/current", type: "nfs"

  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--cpuexecutioncap", $EXEC_CAP]
    v.customize ["modifyvm", :id, "--memory", $MEMORY]
    v.customize ["modifyvm", :id, "--cpus", $CPUS]
  end

  config.ssh.forward_agent = true

  # Ansible
  config.vm.provision "ansible" do |ansible|
    ansible.sudo = true
    ansible.playbook = "provision/playbook.yml"
    ansible.limit = "vagrant"
    ansible.inventory_path = "provision/hosts/vagrant"
    ansible.verbose = "vvvv"
    #ansible.tags = "config"
  end
end
