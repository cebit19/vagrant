# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!

Vagrant.configure(2) do |config|  
  config.vm.define "dhcpapache" do |dhcpapache|
    dhcpapache.vm.box = "ubuntu/trusty64"
    dhcpapache.vm.hostname = "dhcpapache"
    dhcpapache.vm.network "public_network", type:"dhcp"
    dhcpapache.vm.network "private_network", ip:"10.100.10.1", virtualbox__intnet:true
    
    dhcpapache.vm.provider "virtualbox" do |vb|
	  vb.memory = "2048" 
    end

    dhcpapache.vm.provision "shell", inline: <<-SHELL
		  sudo apt-get update
        
        sudo apt-get -y install apache2

        sudo rm /var/www/html/index.html
        echo "<html lang="de">"| sudo tee -a /var/www/html/index.html
        echo "<head>"sudo tee -a /var/www/html/index.html
		    echo "<title>Vorlage_Home</title>" | sudo tee -a /var/www/html/index.html
	      echo "</head>" | sudo tee -a /var/www/html/index.html
        echo "<body>" | sudo tee -a /var/www/html/index.html
		    echo "<header>" | sudo tee -a /var/www/html/index.html
				echo "<hgroup>" | sudo tee -a /var/www/html/index.html
				echo "<h1>Willkommen auf meiner Webseite</h1>" | sudo tee -a /var/www/html/index.html
				echo "</hgroup>" | sudo tee -a /var/www/html/index.html
			  echo "</header>" | sudo tee -a /var/www/html/index.html
        echo "</body>" | sudo tee -a /var/www/html/index.html    
        echo "</html>" | sudo tee -a /var/www/html/vagindex.html 
        
        # DHCP Server installieren
        sudo apt-get -y install isc-dhcp-server
        # DHCP Server konfigurieren
        sudo sed -i 's/example.org/LB1.local/g' /etc/dhcp/dhcpd.conf
        sudo sed -i 's/ns2.LB1.local/8.8.8.8/g' /etc/dhcp/dhcpd.conf
        sudo sed -i 's/#authoritative/authoritative/g' /etc/dhcp/dhcpd.conf
        sudo sed -i '$asubnet 10.100.10.0 netmask 255.255.255.0 {' /etc/dhcp/dhcpd.conf
        sudo sed -i '$arange 10.100.10.20 10.100.10.254;' /etc/dhcp/dhcpd.conf
        sudo sed -i '$aoption routers 10.100.10.1;' /etc/dhcp/dhcpd.conf
        sudo sed -i '$a}' /etc/dhcp/dhcpd.conf
        sudo sed -i 'interface enp0s9'
		    sudo service isc-dhcp-server restart
        
        # Eingabemethode⁄ ändern
        sudo apt-get -y install language-pack-de
        sudo sed -i 's/LANG=en_US.UTF-8/LANG=de_CH.UTF-8/g' /etc/default/locale
        sudo sed -i 's/XKBLAYOUT="us"/XKBLAYOUT="ch"/g' /etc/default/locale
        sudo reboot

    SHELL
  end

  config.vm.define "dhcpclient" do |dhcpclient|
    dhcpclient.vm.box = "ubuntu/trusty64"
    dhcpclient.vm.hostname = "dhcpclient"
    dhcpclient.vm.network "private_network", type:"dhcp", virtualbox__intnet:true

    dhcpclient.vm.provider "virtualbox" do |vb|
	  vb.memory = "2048" 
    end

  end

end
