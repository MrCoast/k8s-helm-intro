WORKER_MACHINES_COUNT = 2

Vagrant.configure("2") do |config|
    config.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 2
    end

    config.vm.box = "bento/ubuntu-22.04"

    config.vm.define "k8s-master" do |machine|
        machine.vm.hostname = "k8smaster.example.net"

        machine.vm.provision "ansible_local" do |ansible|
            ansible.playbook = "playbook.yml"
            ansible.extra_vars = {
                machine_name: "k8s-master"
            }
        end
    end

    (1..WORKER_MACHINES_COUNT).each do |machine_id|
        config.vm.define "k8s-worker-#{machine_id}" do |machine|
            machine.vm.hostname = "k8sworker#{machine_id}.example.net"

            machine.vm.provision "ansible_local" do |ansible|
                ansible.playbook = "playbook.yml"
                ansible.extra_vars = {
                    machine_name: "k8s-worker-#{machine_id}"
                }
            end
        end
    end
end