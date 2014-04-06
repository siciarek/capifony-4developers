Elementy specyficzne dla Symfony 2
==================================

Nagłówek pliku konfiguracyjnego ``Capfile`` dla projektu ``Symfony 2``

.. code-block:: ruby

    load 'deploy' if respond_to?(:namespace) # cap2 differentiator

    require 'capifony_symfony2'

.. code-block:: bash

    $ cap -vT


Komendy ``capistrano``
----------------------

.. code-block:: none

    cap deploy                                  # Deploys your project.
    cap deploy:check                            # Test deployment dependencies.
    cap deploy:cleanup                          # Clean up old releases.
    cap deploy:cold                             # Deploys and starts a `cold' app...
    cap deploy:create_symlink                   # Updates the symlink to the most...
    cap deploy:drop                             # Drops :deploy_to directory
    cap deploy:finalize_update                  # Updates latest release source path
    cap deploy:migrate                          # Runs the Symfony2 migrations
    cap deploy:migrations                       # Deploy and run pending migrations.
    cap deploy:pending                          # Displays the commits since your...
    cap deploy:pending:diff                     # Displays the `diff' since your ...
    cap deploy:restart                          # Blank task exists as a hook int...
    cap deploy:rollback                         # Rolls back to a previous versio...
    cap deploy:rollback:cleanup                 # [internal] Removes the most rec...
    cap deploy:rollback:code                    # Rolls back to the previously de...
    cap deploy:rollback:revision                # [internal] Points the current s...
    cap deploy:set_permissions                  # Sets permissions for writable_d...
    cap deploy:setup                            # Prepares one or more servers fo...
    cap deploy:share_childs                     # Symlinks static directories and...
    cap deploy:start                            # Blank task exists as a hook int...
    cap deploy:stop                             # Blank task exists as a hook int...
    cap deploy:symlink                          # Deprecated API.
    cap deploy:test_all                         # Deploys the application and run...
    cap deploy:update                           # Copies your project and updates...
    cap deploy:update_code                      # Copies your project to the remo...
    cap deploy:upload                           # Copy files to the currently dep...
    cap deploy:web:disable                      # Present a maintenance page to v...
    cap deploy:web:enable                       # Makes the application web-acces...
    cap invoke                                  # Invoke a single command on the ...
    cap shared:folder:download                  # Downloads a backup of the share...
    cap shell                                   # Begin an interactive Capistrano...

Komendy dotyczące bazy danych
-----------------------------

.. code-block:: none

    cap database:dump:local                     # Dumps local database
    cap database:dump:remote                    # Dumps remote database
    cap database:move:to_local                  # Dumps remote database, download...
    cap database:move:to_remote                 # Dumps local database, loads it ...

Komendy ``composera``
---------------------

.. code-block:: none

    cap symfony:composer:copy_vendors           #
    cap symfony:composer:dump_autoload          # Dumps an optimized autoloader
    cap symfony:composer:dump_autoload_temp     # Dumps an optimized autoloader
    cap symfony:composer:get                    # Gets composer and installs it
    cap symfony:composer:install                # Runs composer to install vendor...
    cap symfony:composer:update                 # Runs composer to update vendors...

Komendy ``Symfony 2``
---------------------

.. code-block:: none

    cap symfony                                 # Runs custom symfony command

    cap symfony:assetic:dump                    # Dumps all assets to the filesystem
    cap symfony:assets:install                  # Installs bundle's assets
    cap symfony:assets:update_version           # Updates assets version (in conf...

    cap symfony:bootstrap:build                 # Runs the bin/build_bootstrap sc...
    cap symfony:cache:clear                     # Cache clear
    cap symfony:cache:warmup                    # Cache warmup

    cap symfony:project:clear_controllers       # Clears all non production envir...


Komendy ``Doctrine``
--------------------

.. code-block:: none

    cap symfony:doctrine:cache:clear_metadata   # Clears all metadata cache for a...
    cap symfony:doctrine:cache:clear_query      # Clears all query cache for a en...
    cap symfony:doctrine:cache:clear_result     # Clears result cache for a entit...
    cap symfony:doctrine:database:create        # Creates the configured databases
    cap symfony:doctrine:database:drop          # Drops the configured databases
    cap symfony:doctrine:init:acl               # Mounts ACL tables in the database
    cap symfony:doctrine:load_fixtures          # Load data fixtures
    cap symfony:doctrine:migrations:migrate     # Executes a migration to a speci...
    cap symfony:doctrine:migrations:status      # Views the status of a set of mi...

    cap symfony:doctrine:mongodb:indexes:create # Allows you to create indexes *o...
    cap symfony:doctrine:mongodb:indexes:drop   # Allows you to drop indexes *onl...
    cap symfony:doctrine:mongodb:schema:create  # Allows you to create databases,...
    cap symfony:doctrine:mongodb:schema:drop    # Allows you to drop databases, c...
    cap symfony:doctrine:mongodb:schema:update  # Allows you to update databases,...
    cap symfony:doctrine:schema:create          # Processes the schema and either...
    cap symfony:doctrine:schema:drop            # Drops the complete database sch...
    cap symfony:doctrine:schema:update          # Updates database schema of Enti...


Komendy ``Propel``
------------------

.. code-block:: none

    cap symfony:propel:build:acl                # Generates ACLs models
    cap symfony:propel:build:acl_load           # Inserts propel ACL tables
    cap symfony:propel:build:all_and_load       # Builds the Model classes, SQL s...
    cap symfony:propel:build:model              # Builds the Model classes
    cap symfony:propel:build:sql                # Builds SQL statements
    cap symfony:propel:build:sql_load           # Inserts SQL statements
    cap symfony:propel:database:create          # Creates the configured databases
    cap symfony:propel:database:drop            # Drops the configured databases

Komendy ``bin/vendors``
-----------------------

.. code-block:: none

    cap symfony:vendors:install                 # Runs the bin/vendors script to ...
    cap symfony:vendors:reinstall               # Runs the bin/vendors script to ...
    cap symfony:vendors:upgrade                 # Runs the bin/vendors script to ...


Komendy przeglądania logów
--------------------------

.. code-block:: none

    cap symfony:logs:tail                       # Tail prod.log
    cap symfony:logs:tail_dev                   # Tail dev.log

Uwagi
-----

Przy komendach ``symfony`` innych niż zdefiniowane np. ``fos:js-routing:dump`` pojawia się zapytanie

.. code-block:: none

    $ cap symfony
      * 2014-04-05 21:02:37 executing `symfony'
    task_arguments [cache:clear] :

aby tego uniknąć, kiedy np. chcemu użyć komendy w skrypcie, musimy przekierować komendę na ``STDIN``.

.. code-block:: bash

    $ echo fos:js-routing:dump | cap symfony

Zastosowanie w pliku konfiguracyjnym ``ant``

.. code-block:: xml

    <target name="fosjs">
        <exec executable="bash">
            <arg line="-c &quot;echo fos:js-routing:dump | cap symfony&quot;"/>
        </exec>
    </target>

Ustawienia konfiguracyjne ``composera``
---------------------------------------

.. code-block:: ruby

    set :use_composer,        true
    # set :composer_bin,       "/home/usync/bin/composer"
    set :interactive_mode,    false


Ustawienia konfiguracyjne specyficzne dla ``Symfony``
-----------------------------------------------------

.. code-block:: ruby

    set :model_manager,       "doctrine" # Or: "propel"
    set :shared_files,        [ "app/config/parameters.yml", "build.xml", "properties.cnf", "web/app.php" ]
    set :shared_children,     [ log_path, web_path + "/uploads", "vendor" ]

    set :update_vendors,      true
    set :dump_assetic_assets, true
    set :assets_symlinks,     true
