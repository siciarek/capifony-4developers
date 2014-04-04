Ustawienie odpowiednich praw dostępu do katalogów
=================================================

.. code-block:: ruby

    set :writable_dirs,       [ "app/cache", "app/logs" ]
    set :webserver_user,      "www-data"
    set :permission_method,   :acl
    set :use_set_permissions, true

Ustawienie ścieżek do których inny użytkownik ma mieć prawo dostępu typu ``rw``.

.. code-block:: ruby

    set :writable_dirs,       [ "app/cache", "app/logs", "web/uploads" ]

Podanie użytkownika, który ma mieć prawa dostępu typu ``rw`` do powyższych katalogów.

.. code-block:: ruby

    set :webserver_user,      "www-data"

Podanie sposobu w jaki mają być ustawiane prawa dostępu.

.. code-block:: ruby

    set :permission_method,   :acl

Dostępne wartości parametru:

    * ``:acl`` - korzysta z ``setfacl``
    * ``:chown`` - wymaga ustawienia ``set use_sudo:, true``
    * ``:chmod`` - korzysta z ``chmod +a``

Preferowana jest wartość ``:acl``

Flaga, czy należy ustawiać prawa dostępu, może być czasowo wyłączane bez potrzeby usuwania całej powyższej konfiguracji.

.. code-block:: ruby

    set :use_set_permissions, true