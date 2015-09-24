# -*- mode: ruby -*-
# vi: set ft=ruby :

# Simple perl dev env that uses system perl with local::lib 

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  #config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provision "shell", inline: <<-SHELL

   apt-get update
   
   apt-get install -y build-essential
   apt-get install -y liblocal-lib-perl
   apt-get install -y cpanminus
   apt-get install -y perl-doc

   echo '[ $SHLVL -eq 1 ] && eval "$(perl -I$HOME/perl5/lib/perl5 -Mlocal::lib)"' >> /home/vagrant/.profile

  SHELL

end
