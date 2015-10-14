# -*- mode: ruby -*-
# vi: set ft=ruby :

# Simple perl dev env that uses system perl with local::lib 

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  #config.vm.network "forwarded_port", guest: 80, host: 8080

  config.ssh.username = "vagrant"

# There are 3 inline scripts: config files script, ubuntu packages install script and CPAN distribution install script.

# I should probably move them to separate files.

  config.vm.provision "shell", :privileged => false, inline: <<-CONFIG
  mkdir -p ~/opt/bin
  echo PATH=~/opt/bin:$PATH >> ~/.profile
  echo '[ $SHLVL -eq 1 ] && eval "$(perl -I~/perl5/lib/perl5 -Mlocal::lib)"' >> ~/.profile
  echo 'eval "$( perl -I~/perl5/lib/perl5 -Mlocal::lib)"; cpanm $@' > ~/opt/bin/wcpanm && chmod 755 ~/opt/bin/wcpanm 
  CONFIG

  config.vm.provision "shell", inline: <<-INSTALL

   packages=(
	     build-essential
	     liblocal-lib-perl
	     cpanminus
	     perl-doc
	     git
#	     libssl-dev
	    )

   apt-get update
   apt-get install -y ${packages[@]} 

  INSTALL

  config.vm.provision "shell", :privileged => false, inline: <<-CPAN
   CPAN=(
#	    Dist::Zilla
#	    Zilla::Dist
#	    Module::Starter

#	    CPAN::Uploader

#	    Data::Dumper

#	    Perl::Tidy
#	    Perl::Critic
#	    Perl::Version

#	    Devel::NYTProf
#	    Devel::REPL
#	    Devel::Cover
	
#            App::Ack

#	    Pod::Readme
	    Software::License
	 )

   # This may take a while.
   if [ -x ~/opt/bin/wcpanm ]
   then
	~/opt/bin/wcpanm ${CPAN[@]}
   else
	echo "Unable to install CPAN distributions!"
   fi

  CPAN
end
