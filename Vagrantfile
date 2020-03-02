require 'yaml'

config_file = YAML.load_file('config.yaml')
#puts "Config: #{config_file.inspect}\n\n"

# Node Image
IMAGE_NAME = "debian/buster64"

# Node configuration
NODE = Hash.new
NODE['count'] = config_file.fetch('node').fetch('count')
NODE['cpus'] = config_file.fetch('node').fetch('cpus')
NODE['memory'] = config_file.fetch('node').fetch('memory')

# Master configuration
MASTER = Hash.new
MASTER['cpus'] = config_file.fetch('master').fetch('cpus')
MASTER['memory'] = config_file.fetch('master').fetch('memory')

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.provider :virtualbox do |v|
          v.cpus = MASTER['cpus']
          v.memory = MASTER['memory']
        end
        master.vm.network "private_network", ip: "192.168.50.10"
        master.vm.hostname = "k8s-master"
        master.vm.provision "ansible" do |ansible|
            ansible.playbook = "kubernetes-setup/master-playbook.yml"
            ansible.extra_vars = {
                node_ip: "192.168.50.10",
            }
        end
    end

    (1..NODE['count']).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.provider :virtualbox do |v|
              v.cpus = NODE['cpus']
              v.memory = NODE['memory']
            end
            node.vm.network "private_network", ip: "192.168.50.#{i + 10}"
            node.vm.hostname = "node-#{i}"
            node.vm.provision "ansible" do |ansible|
                ansible.playbook = "kubernetes-setup/node-playbook.yml"
                ansible.extra_vars = {
                    node_ip: "192.168.50.#{i + 10}",
                }
           end
        end
    end
end
