$name_server1 = "server1"
$name_server2 = "server2"

$ip_server1 = "192.168.3.4"
$ip_server2 = "192.168.3.5"

Vagrant.configure("2") do |config|



    config.vm.provision "file", source: "id_rsa", destination: "/home/vagrant/.ssh/id_rsa"
    public_key = File.read("id_rsa.pub")
    config.vm.provision :shell, :inline =>"
     echo 'Copying public SSH Key to the VM'
     mkdir -p /home/vagrant/.ssh
     chmod 700 /home/vagrant/.ssh
     echo '#{public_key}' >> /home/vagrant/.ssh/authorized_keys
     chmod -R 600 /home/vagrant/.ssh/authorized_keys
     echo 'Host 192.168.3.*' >> /home/vagrant/.ssh/config
     echo 'StrictHostKeyChecking no' >> /home/vagrant/.ssh/config
     echo 'UserKnownHostsFile /dev/null' >> /home/vagrant/.ssh/config
     chmod -R 600 /home/vagrant/.ssh/config
     echo '#{$ip_server1}   #{$name_server1}' >> /etc/hosts
     echo '#{$ip_server2}   #{$name_server2}' >> /etc/hosts
     "
    
    config.vm.provider :virtualbox do |vb|
      vb.memory = 256
      vb.cpus = 1
    end
    
    config.vm.define $name_server1 do |srv1|
        srv1.vm.hostname = $name_server1
        srv1.vm.box = "centos/7"
        srv1.vm.network :private_network, ip: $ip_server1
        
    end
    
    config.vm.define $name_server2 do |srv2|
        srv2.vm.hostname = $name_server2
        srv2.vm.box = "centos/7"
        srv2.vm.network :private_network, ip: $ip_server2
    end
end