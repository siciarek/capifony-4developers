Inicjalizacja środowiska produkcyjnego aplikacji
================================================

Przykładowa konfiguracja w ``Capfile``

.. code-block:: ruby

    set :application,   "myapp"
    set :user,          "dude"
    set :domain,        "target.server.com"
    set :repository,    "git@myscm.server.net:/home/git/repos/#{application}.git"
    set :deploy_to,     "/var/www/#{domain}"

    role :app,          :domain, :primary => true  # This may be the same as your ``Web`` server
    role :web,          :domain                    # Your HTTP server, Apache/etc

Przygotowanie środowiska produkcyjnego
--------------------------------------

.. code-block:: bash

    $ cap deploy:setup

.. code-block:: none

      * 2014-04-04 12:54:57 executing `deploy:setup'
      * executing multiple commands in parallel
        -> "else" :: "sudo -p 'sudo password: ' mkdir -p /var/www/target.server.com /var/www/target.server.com/releases /var/www/target.server.com/shared /var/www/target.server.com/shared/system /var/www/target.server.com/shared/log /var/www/target.server.com/shared/pids"
        -> "else" :: "sudo -p 'sudo password: ' mkdir -p /var/www/target.server.com /var/www/target.server.com/releases /var/www/target.server.com/shared /var/www/target.server.com/shared/system /var/www/target.server.com/shared/log /var/www/target.server.com/shared/pids"
        -> "else" :: "sudo -p 'sudo password: ' mkdir -p /var/www/target.server.com /var/www/target.server.com/releases /var/www/target.server.com/shared /var/www/target.server.com/shared/system /var/www/target.server.com/shared/log /var/www/target.server.com/shared/pids"
        -> "else" :: "sudo -p 'sudo password: ' mkdir -p /var/www/target.server.com /var/www/target.server.com/releases /var/www/target.server.com/shared /var/www/target.server.com/shared/system /var/www/target.server.com/shared/log /var/www/target.server.com/shared/pids"
        servers: ["new.ses-control.com", "platform.ses-support.com", "integration.sescom.pl", "hm.ses-control.com"]
        [integration.sescom.pl] executing command
        [hm.ses-control.com] executing command
        [platform.ses-support.com] executing command
        [new.ses-control.com] executing command
        command finished in 130ms
      * executing multiple commands in parallel
        -> "else" :: "sudo -p 'sudo password: ' chmod g+w /var/www/target.server.com /var/www/target.server.com/releases /var/www/target.server.com/shared /var/www/target.server.com/shared/system /var/www/target.server.com/shared/log /var/www/target.server.com/shared/pids"
        -> "else" :: "sudo -p 'sudo password: ' chmod g+w /var/www/target.server.com /var/www/target.server.com/releases /var/www/target.server.com/shared /var/www/target.server.com/shared/system /var/www/target.server.com/shared/log /var/www/target.server.com/shared/pids"
        -> "else" :: "sudo -p 'sudo password: ' chmod g+w /var/www/target.server.com /var/www/target.server.com/releases /var/www/target.server.com/shared /var/www/target.server.com/shared/system /var/www/target.server.com/shared/log /var/www/target.server.com/shared/pids"
        -> "else" :: "sudo -p 'sudo password: ' chmod g+w /var/www/target.server.com /var/www/target.server.com/releases /var/www/target.server.com/shared /var/www/target.server.com/shared/system /var/www/target.server.com/shared/log /var/www/target.server.com/shared/pids"
        servers: ["new.ses-control.com", "platform.ses-support.com", "integration.sescom.pl", "hm.ses-control.com"]
        [integration.sescom.pl] executing command
        [hm.ses-control.com] executing command
        [platform.ses-support.com] executing command
        [new.ses-control.com] executing command
        command finished in 98ms

Jeżeli wszystkie prawa dostępu będą ustawione prawidłowo na **serwerze produkcyjnym** zostanie utworzona poniższa
struktura katalogów:

.. code-block:: none

    /var/www/target.server.com
        |-- releases
        `-- shared


Sprawdzenie konfiguracji serwera produkcyjnego
----------------------------------------------

.. code-block:: bash

    cap deploy:check


Przykład zawartości katalogu aplikacji po kolejnym wdrożeniu
------------------------------------------------------------

.. code-block:: none

    `-- /var/www/target.server.com
    |-- current -> /var/www/target.server.com/releases/20100512131539
    |-- releases
    |   `-- 20100512131539
    |   `-- 20100509150741
    |   `-- 20100509145325
    `-- shared
       |-- web
       |    `-- uploads
       |-- logs
       |-- vendors
       `-- config
           `-- app
                `-- parameters.yml
