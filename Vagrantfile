$samplescript = <<SCRIPT
echo "192.168.56.102    web" >> /etc/hosts
yum install -y git
git clone https://github.com/ausard/module2.git
cd module2
git checkout task2
cat test.txt
ping -c 6 web
SCRIPT

Vagrant.configure(2) do |config|

    config.vm.define "web" do |web|
        web.vm.box = "centos/7"
        web.vm.hostname = 'web'
    
        web.vm.network :private_network, ip: "192.168.56.102"

        web.vm.provider :virtualbox do |vb|
            vb.memory = "1024"
            vb.cpus = "2"
        end
    end

    config.vm.define "githost" do |githost|
        githost.vm.box = "centos/7"
        githost.vm.hostname = 'githost'
    
        githost.vm.network :private_network, ip: "192.168.56.101"
        githost.vm.provision "shell", inline: $samplescript

        githost.vm.provider :virtualbox do |vb|
            vb.memory = "1024"
            vb.cpus = "2"
        end
    end
end