Source Control Management
=========================

Przykładowa konfiguracja w ``Capfile``

.. code-block:: ruby

    set :application,   "myapp"
    set :user,          "dude"
    set :domain,        "target.server.com"
    set :repository,    "git@myscm.server.net:/home/git/repos/#{application}.git"
    set :deploy_to,     "/var/www/#{domain}"

    role :app,          :domain, :primary => true  # This may be the same as your ``Web`` server
    role :web,          :domain                    # Your HTTP server, Apache/etc

    set :scm,        :git
    set :deploy_via, :copy

Wartości ``:scm``
-----------------

**:none**
    System kontroli wersji nie jest stosowany
**:scm**
    System kontroli wersji jest wykrywany automatycznie
**:git**
    GIT http://git-scm.com
**:accurev**
    AccuRev http://www.accurev.com
**:bzr**
    Bazaar http://bazaar.canonical.com
**:cvs**
    CVS http://www.nongnu.org/cvs/
**:darcs**
    Darcs http://darcs.net
**:subversion**
    SVN http://subversion.tigris.org, http://subversion.apache.org
**:mercurial**
    Mercurial http://mercurial.selenic.com
**:perforce**
    PERFORCE http://www.perforce.com

Wartości ``:deploy_via``
------------------------

**:copy**
    Na **serwerze źródłowym** wykonuje eksport wersji, domyślnie, do katalogu ``/tmp``, następnie kopiuje jego zawartość
    na **serwer produkcyjny**.

.. code-block:: ruby

    set :copy_dir, "./tmp" # optional

    set :copy_exclude,  [
        ".git",
        ".gitignore",
        "/app/config/config_test.yml",
        "/bin",
        "/src/Application/MainBundle/Tests",
        "/src/Application/MainBundle/Resources/doc",
        "/web/apple-touch-icon.png",
    ]

**:checkout**
    Wykonuje operację ``checkout`` na **serwerze produkcyjnym**, nie zalecany, ze względu na możliwość nieautoryzowanej
    modyfikacji zawartości repozytorium.
**:export**
    Wykonuje operację ``export`` na **serwerze produkcyjnym**.
**:remote_cache**
    Wykonuje ``git pull`` (lub odpowiednik tej komendy w innych ``SCM``) w katalogu ``shared/cached_copy``,
    zamiast zaciągania całego repozytorium. Ma znaczenie jeżeli zależy nam na przyśpieszeniu procesu wdrożenia.
    Jeżeli w czasie wdrożenia pojawią się problemy należy usunąć katalog ``shared/cached_copy``.
**:rsync_with_remote_cache**
    W tym przypadku ``rsync`` utworzy katalog na **serwerze produkcyjnym** i będzie go synchronizował ze zmianami w repozytorium.
    Wymaga instalacji dodatkowego ``gema``.

.. code-block:: bash
    $ gem install capistrano_rsync_with_remote_cache

Wartości specyficzne dla danego ``SCM``
---------------------------------------

Możemy dodać do konfiguracji dodatkowe parametry, specyficzne dla użytego ``SCM`` np.

.. code-block:: ruby

    set :git_enable_submodules, true
