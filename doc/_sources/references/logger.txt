Zakres informacji zwracany przez ``cap``
========================================

Capistrano umożliwia wyświetlanie informacji o wykonywanych komendach w różnych zakresach.

Typy zakresu
------------

.. code-block:: ruby

    logger.level = Logger::IMPORTANT # -->
    logger.level = Logger::INFO      # **
    logger.level = Logger::DEBUG     #  *
    logger.level = Logger::TRACE     #
    logger.level = Logger::MAX_LEVEL # Logger::TRACE = Logger::MAX_LEVEL


Fragment kodu ``logger.rb``

.. code-block:: ruby

    module Capistrano
      class Logger #:nodoc:
        attr_accessor :level
        attr_reader   :device

        IMPORTANT = 0
        INFO      = 1
        DEBUG     = 2
        TRACE     = 3

        MAX_LEVEL = 3


Przykładowy wynik ustawień
--------------------------

.. code-block:: ruby

    logger.level = Logger::IMPORTANT

.. code-block:: none

	--> Updating code base with copy strategy
	--> Creating cache directory................................V
	--> Creating symlinks for shared directories................V
	--> Creating symlinks for shared files......................V
	--> Normalizing asset timestamps............................V
	--> Downloading Composer....................................V

.. code-block:: ruby

    logger.level = Logger::INFO`

.. code-block:: none

	 ** sftp upload parameters.yml -> /d0/www/platform-integration/shared/app/config/parameters.yml
	 ** transaction: start
	--> Updating code base with copy strategy
	 ** sftp upload /tmp/20140319145926.tar.gz -> /tmp/20140319145926.tar.gz
	--> Creating cache directory
	--> Creating symlinks for shared directories
	--> Creating symlinks for shared files
	--> Normalizing asset timestamps
	--> Downloading Composer
	 ** [out :: myspec.pl] #!/usr/bin/env php
	 ** [out :: myspec.pl] Some settings on your machine may cause stability issues with Composer.
	 ** [out :: myspec.pl] If you encounter issues, try to change the following:
	 ** [out :: myspec.pl]
	 ** [out :: myspec.pl] Your PHP (5.3.3-7+squeeze14) is quite old, upgrading to PHP 5.3.4 or higher is recommended.
	 ** [out :: myspec.pl] Composer works with 5.3.2+ for most people, but there might be edge case issues.
	 ** [out :: myspec.pl]
	 ** [out :: myspec.pl] Downloading...
	 ** [out :: myspec.pl]
	 ** [out :: myspec.pl] Composer successfully installed to: /d0/www/platform-integration/releases/20140319145926/composer.phar
	 ** [out :: myspec.pl]
	 ** [out :: myspec.pl] Use it: php composer.phar
	--> Updating Composer dependencies
	 ** [out :: myspec.pl] Loading composer repositories with package information
	 ** [out :: myspec.pl] Updating dependencies



.. code-block:: ruby

    logger.level = Logger::DEBUG

.. code-block:: none

	  * 2014-03-19 16:00:41 executing `deploy'
	  * 2014-03-19 16:00:41 executing `upload_parameters'
	  * executing "mkdir -p /d0/www/platform-integration/shared/app/config"
	 ** sftp upload parameters.yml -> /d0/www/platform-integration/shared/app/config/parameters.yml
	  * sftp upload complete
	  * 2014-03-19 16:00:41 executing `deploy:update'
	 ** transaction: start
	  * 2014-03-19 16:00:41 executing `deploy:update_code'
	--> Updating code base with copy strategy
	  * getting (via checkout) revision cc301318ff9b560edd494a57db6c66ea95c878c7 to /tmp/20140319150041
	  * processing exclusions...
	  * Compressing /tmp/20140319150041 to /tmp/20140319150041.tar.gz
	 ** sftp upload /tmp/20140319150041.tar.gz -> /tmp/20140319150041.tar.gz
	  * sftp upload complete
	  * executing "cd /d0/www/platform-integration/releases && tar xzf /tmp/20140319150041.tar.gz && rm /tmp/20140319150041.tar.gz"
	  * 2014-03-19 16:00:44 executing `deploy:finalize_update'
	  * executing "chmod -R g+w /d0/www/platform-integration/releases/20140319150041"
	--> Creating cache directory
	  * executing "sh -c 'if [ -d /d0/www/platform-integration/releases/20140319150041/app/cache ] ; then rm -rf /d0/www/platform-integration/releases/20140319150041/app/cache; fi'"
	  * executing "sh -c 'mkdir -p /d0/www/platform-integration/releases/20140319150041/app/cache && chmod -R 0777 /d0/www/platform-integration/releases/20140319150041/app/cache'"
	  * executing "chmod -R g+w /d0/www/platform-integration/releases/20140319150041/app/cache"
	  * 2014-03-19 16:00:44 executing `deploy:share_childs'
	--> Creating symlinks for shared directories
	  * executing "mkdir -p /d0/www/platform-integration/shared/app/logs"
	  * executing "sh -c 'if [ -d /d0/www/platform-integration/releases/20140319150041/app/logs ] ; then rm -rf /d0/www/platform-integration/releases/20140319150041/app/logs; fi'"
	  * executing "ln -nfs /d0/www/platform-integration/shared/app/logs /d0/www/platform-integration/releases/20140319150041/app/logs"
	  * executing "mkdir -p /d0/www/platform-integration/shared/web/uploads"
	  * executing "sh -c 'if [ -d /d0/www/platform-integration/releases/20140319150041/web/uploads ] ; then rm -rf /d0/www/platform-integration/releases/20140319150041/web/uploads; fi'"
	  * executing "ln -nfs /d0/www/platform-integration/shared/web/uploads /d0/www/platform-integration/releases/20140319150041/web/uploads"
	  * executing "mkdir -p /d0/www/platform-integration/shared/vendor"
	  * executing "sh -c 'if [ -d /d0/www/platform-integration/releases/20140319150041/vendor ] ; then rm -rf /d0/www/platform-integration/releases/20140319150041/vendor; fi'"
	  * executing "ln -nfs /d0/www/platform-integration/shared/vendor /d0/www/platform-integration/releases/20140319150041/vendor"
	--> Creating symlinks for shared files
	  * executing "mkdir -p /d0/www/platform-integration/shared/app/config"
	  * executing "touch /d0/www/platform-integration/shared/app/config/parameters.yml"
	  * executing "ln -nfs /d0/www/platform-integration/shared/app/config/parameters.yml /d0/www/platform-integration/releases/20140319150041/app/config/parameters.yml"
	--> Normalizing asset timestamps
	  * executing "find /d0/www/platform-integration/releases/20140319150041/web/css /d0/www/platform-integration/releases/20140319150041/web/images /d0/www/platform-integration/releases/20140319150041/web/js -exec touch -t 201403191500.45 {} ';' &> /dev/null || true"
	  * 2014-03-19 16:00:45 executing `symfony:composer:update'
	  * 2014-03-19 16:00:45 executing `symfony:composer:get'
	  * executing "if [ -e /d0/www/platform-integration/releases/20140319150041/composer.phar ]; then echo 'true'; fi"
	--> Downloading Composer
	  * executing "sh -c 'cd /d0/www/platform-integration/releases/20140319150041 && curl -s http://getcomposer.org/installer | php'"
	 ** [out :: myspec.pl] #!/usr/bin/env php
	 ** [out :: myspec.pl] Some settings on your machine may cause stability issues with Composer.
	 ** [out :: myspec.pl] If you encounter issues, try to change the following:
	 ** [out :: myspec.pl]
	 ** [out :: myspec.pl] Your PHP (5.3.3-7+squeeze14) is quite old, upgrading to PHP 5.3.4 or higher is recommended.
	 ** [out :: myspec.pl] Composer works with 5.3.2+ for most people, but there might be edge case issues.
	 ** [out :: myspec.pl]
	 ** [out :: myspec.pl] Downloading...
	 ** [out :: myspec.pl]
	 ** [out :: myspec.pl] Composer successfully installed to: /d0/www

.. code-block:: ruby

    logger.level = Logger::TRACE
    logger.level = Logger::MAX_LEVEL # Logger::TRACE jest równy Logger::MAX_LEVEL

.. code-block:: none

	  * 2014-03-19 16:02:46 executing `deploy'
		triggering before callbacks for `deploy'
	  * 2014-03-19 16:02:46 executing `upload_parameters'
	  * executing "mkdir -p /d0/www/platform-integration/shared/app/config"
		servers: ["myspec.pl"]
		[myspec.pl] executing command
		command finished in 24ms
		servers: ["myspec.pl"]
	 ** sftp upload parameters.yml -> /d0/www/platform-integration/shared/app/config/parameters.yml
		[myspec.pl] /d0/www/platform-integration/shared/app/config/parameters.yml
		[myspec.pl] done
	  * sftp upload complete
	  * 2014-03-19 16:02:46 executing `deploy:update'
	 ** transaction: start
	  * 2014-03-19 16:02:46 executing `deploy:update_code'
		triggering before callbacks for `deploy:update_code'
	--> Updating code base with copy strategy
		executing locally: "git ls-remote git@ses-support.net:/home/git/repos/platform-integration.git HEAD"
		command finished in 91ms
	  * getting (via checkout) revision cc301318ff9b560edd494a57db6c66ea95c878c7 to /tmp/20140319150246
		executing locally: git clone -q git@ses-support.net:/home/git/repos/platform-integration.git /tmp/20140319150246 && cd /tmp/20140319150246 && git checkout -q -b deploy cc301318ff9b560edd494a57db6c66ea95c878c7 && git submodule -q init && git submodule -q sync && export GIT_RECURSIVE=$([ ! "`git --version`" \< "git version 1.6.5" ] && echo --recursive) && git submodule -q update --init $GIT_RECURSIVE
		command finished in 2742ms
	  * processing exclusions...
	  * Compressing /tmp/20140319150246 to /tmp/20140319150246.tar.gz
		executing locally: tar czf 20140319150246.tar.gz 20140319150246
		command finished in 38ms
		servers: ["myspec.pl"]
	 ** sftp upload /tmp/20140319150246.tar.gz -> /tmp/20140319150246.tar.gz
		[myspec.pl] /tmp/20140319150246.tar.gz
		[myspec.pl] done
	  * sftp upload complete
	  * executing "cd /d0/www/platform-integration/releases && tar xzf /tmp/20140319150246.tar.gz && rm /tmp/20140319150246.tar.gz"
		servers: ["myspec.pl"]
		[myspec.pl] executing command
		command finished in 52ms
	  * 2014-03-19 16:02:49 executing `deploy:finalize_update'
	  * executing "chmod -R g+w /d0/www/platform-integration/releases/20140319150246"
		servers: ["myspec.pl"]
		[myspec.pl] executing command
		command finished in 23ms


Zapis loga do pliku
-------------------

.. code-block:: ruby

    log_file = "deployment.log"
    self.logger = Logger.new(:output => log_file)

    logger.level = Logger::DEBUG
