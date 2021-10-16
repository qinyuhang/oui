Vagrant.configure("2") do |config|
  config.vm.box = "vladimir-babichev/openwrt-19.07"
  config.vm.hostname = "openwrt"
  config.vm.post_up_message = "Please login using username 'root' and password 'vagrant' at http://openwrt.lan"
  config.vm.network "forwarded_port", guest: 80, host: 9090
  #config.vm.network "private_network", ip: "10.10.10.10"

  config.vm.synced_folder ".", "/root", rsync_auto: true,
    rsync__exclude: [
        ".git/",
        "node_modules*",
        "tools",
        ".output*"
        ],
        rsync__verbose: true


  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--nic2", "nat"]
    v.customize ["modifyvm", :id, "--nic3", "bridged", "--bridgeadapter3", "en0"]
  end
  config.vm.provision "shell", inline: <<-SHELL
    opkg update 
    opkg install uhttpd-mod-ubus
    /etc/init.d/rpcd restart 
    /etc/init.d/uhttpd restart
  SHELL
end
