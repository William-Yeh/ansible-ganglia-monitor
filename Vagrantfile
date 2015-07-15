Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  #config.vm.box = "ubuntu/precise64"
  #config.vm.box = "debian/jessie64"
  #config.vm.box = "debian/wheezy64"
  #config.vm.box = "chef/centos-7.1"
  #config.vm.box = "chef/centos-6.6"



  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "test.yml"
#    #ansible.playbook = "example-playbook.yml"
    ansible.sudo = true
  end
end
