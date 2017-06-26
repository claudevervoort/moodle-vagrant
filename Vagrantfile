# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty64"

  forward_port = ->(guest, host = guest) do
    config.vm.network :forwarded_port,
      guest: guest,
      host: host,
      auto_correct: true
  end
  
  # Sync between the web root of the VM and the 'sites' directory
  config.vm.synced_folder "/mindtap-code/sentinel/moodle", "/var/www/html", owner: "www-data", group: "www-data"
  config.vm.synced_folder "/mindtap-code/sentinel/moodledata", "/var/moodledata", owner: "www-data", group: "www-data"

  forward_port[1080]      # mailcatcher
  forward_port[3306,33306]      # mailcatcher

  # Getting rid of older PHP5 version
  
  config.vm.provision :shell, :inline => "sudo apt-get -y purge `dpkg -l | grep php | awk '{print $2}' |tr \"\\n\" \" \"`"
  config.vm.provision :shell, :inline => "sudo add-apt-repository -y ppa:ondrej/php"
  config.vm.provision :shell, :inline => "sudo apt-get -y update"

  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "manifests"
    puppet.manifest_file = "default.pp"
  end
  
  # did not get this to run as part of Puppet so for now it's here...
  config.vm.provision :shell, :inline => "echo \"SET GLOBAL innodb_file_format=Barracuda;\" | /usr/bin/mysql -uroot -proot"
  config.vm.provision :shell, :inline => "echo \"SET GLOBAL innodb_large_prefix=ON;\" | /usr/bin/mysql -uroot -proot"
  config.vm.provision :shell, :inline => "echo \"SET GLOBAL innodb_file_per_table=ON;\" | /usr/bin/mysql -uroot -proot"
  config.vm.provision :shell, :inline => "echo \"*/1 * * * * /usr/bin/php5.6  /var/www/html/admin/cli/cron.php >/dev/null\" | sudo crontab -u www-data -"
  config.vm.provision :shell, :inline => "rm /var/wwww/html/index.html"
  

  config.vm.network :private_network, ip: "192.168.10.10"
end
