Vagrant.configure("2") do |config|

  (1..2).each do |i|
    config.vm.define "node-#{i}" do |node|
      node.vm.box = "bento/ubuntu-22.04"
      node.ssh.username = "vagrant"
      config.ssh.insert_key = false
      node.vm.provider "virtualbox" do |vb|
        vb.cpus = 1
        vb.memory = 1024
      end
      node.vm.network "forwarded_port", guest: "80", host: "6544", auto_correct: true
      node.vm.network "private_network", ip: "192.168.57.1#{i}"
      node.vm.hostname = "webserver-#{i}"
      node.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "playbook.yml"
      end
    end
  end
end
