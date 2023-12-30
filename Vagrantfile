MASTER_NUM = 1
MASTER_CPU = 1
MASTER_MEM = 3072

GROUP1_NUM=2
GROUP1_CPU=2
GROUP1_MEM=3072

GROUP2_NUM=1
GROUP2_CPU=1
GROUP2_MEM=2048


# NODE_NUM = 2
# NODE_CPU = 2
# NODE_MEM = 2048

IP_BASE = "192.168.56."


Vagrant.configure("2") do |config|
    config.ssh.insert_key = false
    config.vm.define "k3sMaster" do |master|
        master.vm.box = "hashicorp/bionic64"
        master.vm.network "private_network", ip: "192.168.56.11"
        master.vm.hostname = "k3sMaster"
        master.vm.provider "virtualbox" do |v|
            v.memory = MASTER_MEM
            v.cpus = MASTER_CPU
        end
        
        # master.vm.provision "ansible" do |ansible|
        #     ansible.playbook = "roles/k8s.yml"
        #     #Redefine defaults
        #     ansible.extra_vars = {
        #         k8s_master_admin_user:  "vagrant",
        #         k8s_master_admin_group: "vagrant",
        #         k8s_master_apiserver_advertise_address: "192.168.56.11",
        #         k8s_master_node_name: "k8s-m-1",
        #         k8s_node_public_ip: "192.168.56.11"
        #     }                
        # end
    end

    # (1..NODE_NUM).each do |j|
    #     config.vm.define "k3sNode#{j}" do |node|
    #         node.vm.box = "hashicorp/bionic64"
    #         node.vm.network "private_network", ip: "#{IP_BASE}#{j + 10 + MASTER_NUM}"
    #         node.vm.hostname = "k3sNode#{j}"
    #         node.vm.provider "virtualbox" do |v|
    #             v.memory = NODE_MEM
    #             v.cpus = NODE_CPU
    #         end
    #     end
    # end

    (1..GROUP1_NUM).each do |j|
        config.vm.define "k3sG1Node#{j}" do |node|
            node.vm.box = "hashicorp/bionic64"
            node.vm.network "private_network", ip: "#{IP_BASE}#{j + 10 + MASTER_NUM}"
            node.vm.hostname = "k3sG1Node#{j}"
            node.vm.provider "virtualbox" do |v|
                v.memory = GROUP1_MEM
                v.cpus = GROUP1_CPU
            end
        
            # node.vm.provision "ansible" do |ansible|
            #     ansible.playbook = "roles/k8s.yml"                   
            #     #Redefine defaults
            #     ansible.extra_vars = {
            #         k8s_node_admin_user:  "vagrant",
            #         k8s_node_admin_group: "vagrant",
            #         k8s_node_public_ip: "#{IP_BASE}#{j + 10 + MASTER_NUM}"
            #     }
            # end
        end
    end

    (1..GROUP2_NUM).each do |j|
        config.vm.define "k3sG2Node#{j}" do |node|
            node.vm.box = "hashicorp/bionic64"
            node.vm.network "private_network", ip: "#{IP_BASE}#{j + 10 + MASTER_NUM + GROUP1_NUM}"
            node.vm.hostname = "k3sG2Node#{j}"
            node.vm.provider "virtualbox" do |v|
                v.memory = GROUP2_MEM
                v.cpus = GROUP2_CPU
            end
        
            # node.vm.provision "ansible" do |ansible|
            #     ansible.playbook = "roles/k8s.yml"                   
            #     #Redefine defaults
            #     ansible.extra_vars = {
            #         k8s_node_admin_user:  "vagrant",
            #         k8s_node_admin_group: "vagrant",
            #         k8s_node_public_ip: "#{IP_BASE}#{j + 10 + MASTER_NUM + GROUP1_NUM}"
            #     }
            # end
        end
    end
end
