Vagrant.configure("2") do |config|

  config.vm.define "db" do |db|
    db.vm.box = "ubuntu/bionic64" # os
    db.vm.network "forwarded_port", guest: 3306, host: 3306 # переадресація портів
    db.vm.network "private_network", ip: "192.168.32.21" # приватна мережа із такою ip
    db.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver2", "on"] # конфіг щоб був нет
      v.customize ["modifyvm", :id, "--memory", 1024] # оперативка, міняти тіку цифру
      v.customize ["modifyvm", :id, "--name", "db"] # ім'я віртуалки
    end
    db.vm.provision "shell", path: "provision/db_provider_2.sh" # провіжн файл
  end

  
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/bionic64"
    app.vm.network "forwarded_port", guest: 26112, host: 26110
    app.vm.network "private_network", ip: "192.168.32.31"
    app.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver2", "on"]
      v.customize ["modifyvm", :id, "--memory", 4096]
      v.customize ["modifyvm", :id, "--name", "app"]
    end
    app.vm.provision "shell", path: "provision/app_vm_provision.sh"

  end

 # config.vm.define "proxy" do |proxy|
  #  proxy.vm.box = "centos/7"
 #   proxy.vm.network "public_network"
 #   proxy.vm.network "forwarded_port", guest: 80, host: 8080
 #   proxy.vm.network "forwarded_port", guest: 443, host: 8888
 #   proxy.vm.network "private_network", ip: "192.168.32.11"
 #   proxy.vm.provider :virtualbox do |v|
 #     v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
 #     v.customize ["modifyvm", :id, "--memory", 2048]
 #     v.customize ["modifyvm", :id, "--name", "proxy"]
 #   end
 #   proxy.vm.provision "shell", path: #"provision/proxy_vm_provision.sh"
 # end


end
