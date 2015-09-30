# -*- mode: ruby -*-
# vi: set ft=ruby :

# Simple perl dev env that uses system perl with local::lib 

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"

  #config.vm.network "forwarded_port", guest: 80, host: 8080

  config.ssh.username = "vagrant"

  config.vm.provision "shell", :privileged => false, inline: <<-SHELL


   packages=(
	     build-essential
	     liblocal-lib-perl
	     cpanminus
	     perl-doc
	    )

   CPAN=(
	    Dist::Zilla
	    Module::Starter

	    Perl::Tidy
	    Perl::Critic

	    Devel::NYTProf
	    Devel::REPL
	    Devel::Cover
	 )

   sudo apt-get update
   sudo apt-get install -y ${packages[@]} 

   echo '[ $SHLVL -eq 1 ] && eval "$(perl -I$HOME/perl5/lib/perl5 -Mlocal::lib)"' >> $HOME/.profile
   echo 'eval "$( perl -I$HOME/perl5/lib/perl5 -Mlocal::lib)"; cpanm $@' > $HOME/wcpanm && chmod 755 $HOME/wcpanm 
   
   # This may take a while.
   if [ -x $HOME/wcpanm ]
   then
	$HOME/wcpanm ${CPAN[@]}
   else
	echo "Unable to install CPAN distributions!"
   fi


  SHELL

end
