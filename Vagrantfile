Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-7.6"

  config.vm.hostname = "devbox.lan"
  config.vm.network :private_network, ip: "10.10.0.20"
  config.ssh.forward_agent = true

  config.vm.network "forwarded_port", guest: 80, host: 8200
  # config.vm.network "forwarded_port", guest: 80, host: 8000

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--memory", ENV['MEMORY'] ? ENV['MEMORY'] : 1024]
    v.customize ["modifyvm", :id, "--cpus", ENV['CPU'] ? ENV['CPU'] : 4]
  end

  ############################################################################
  # Shared folders
  config.vm.synced_folder ".",  "/vagrant", id: "vagrant-root", disabled: true
  config.vm.synced_folder "./provision", "/opt/provision", nfs: true
  config.vm.synced_folder "./webroot", "/opt/webroot", nfs: true

  # other projects
  #config.vm.synced_folder "../../path-to-some-project", "/opt/some-project"
  #config.vm.synced_folder "../../../pixi", "/opt/pixi"
  #config.vm.synced_folder "/mnt/r2d2/web/ineo.biz/dev/test", "/opt/r2d2"

  ############################################################################
  # Provisioning
  config.vm.provision "shell" do |s|
    s.name = "install common"
    s.path = "provision/common.sh"
  end

  config.vm.provision "shell" do |s|
    s.name = "install mysql"
    s.path = "provision/mysql.sh"
  end

  config.vm.provision "shell" do |s|
    s.name = "install php"
    s.path = "provision/php.sh"
  end

  config.vm.provision "shell" do |s|
    s.name = "install httpd"
    s.path = "provision/httpd.sh"
  end

  config.vm.provision "shell" do |s|
    s.name = "install phpmyadmin"
    s.path = "provision/phpmyadmin.sh"
  end

  # config.vm.provision "shell" do |s|
  #   s.name = "install craftcms"
  #   s.path = "provision/craftcms.sh"
  # end

  # config.vm.provision "shell" do |s|
  #   s.name = "install django"
  #   s.path = "provision/django.sh"
  # end

end