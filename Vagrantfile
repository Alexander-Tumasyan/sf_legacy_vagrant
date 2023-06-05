Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "pg"
    vb.memory = "1024"
    vb.cpus = "2"
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update && sudo apt-get install -y wget make gcc libreadline6 libreadline6-dev zlibc zlib1g-dev bison
    wget -q https://ftp.postgresql.org/pub/source/v8.4.22/postgresql-8.4.22.tar.gz
    tar xzf postgresql-8.4.22.tar.gz
    cd postgresql-8.4.22
    ./configure
    make
    su
    make install
    useradd postgres
    mkdir /usr/local/pgsql/data
    chown -R postgres:postgres /usr/local/pgsql
    su postgres -c "/usr/local/pgsql/bin/initdb -D /usr/local/pgsql/data/"
    su postgres -c "/usr/local/pgsql/bin/postgres -D /usr/local/pgsql/data/ -l logfile start"
  SHELL
end