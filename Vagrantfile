Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"

  # Servidor web 1
  config.vm.define "web1" do |web1|
    web1.vm.hostname = "web1"
    web1.vm.network "private_network", ip: "192.168.56.11"
    web1.vm.provider "virtualbox" do |vb|
      vb.memory = 512
      vb.cpus = 1
    end
    web1.vm.synced_folder "./www", "/var/www/html"
    web1.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
      echo "<h1 style='color: blue;'>Servidor Web 1</h1>" > /var/www/html/index.html
    SHELL
  end

  # Servidor web 2
  config.vm.define "web2" do |web2|
    web2.vm.hostname = "web2"
    web2.vm.network "private_network", ip: "192.168.56.12"
    web2.vm.provider "virtualbox" do |vb|
      vb.memory = 512
      vb.cpus = 1
    end
    #web2.vm.synced_folder "./www", "/var/www/html"
    web2.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
      echo "<h1 style='color: blue;'>Servidor Web 2</h1>" > /var/www/html/index.html
    SHELL
  end

  # Servidor de balanceo con Nginx
  config.vm.define "loadbalancer" do |lb|
    lb.vm.hostname = "loadbalancer"
    lb.vm.network "private_network", ip: "192.168.56.13"
    lb.vm.provider "virtualbox" do |vb|
      vb.memory = 512
      vb.cpus = 1
    end
    lb.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y nginx
      cat > /etc/nginx/sites-available/default <<EOF
server {
    listen 80;

    location / {
        proxy_pass http://backend;
    }
}

upstream backend {
    server 192.168.56.11;
    server 192.168.56.12;
}
EOF
      systemctl restart nginx
    SHELL
  end
end
