Włączanie i wyłączanie aplikacji
================================

Podstawowe komendy
------------------

.. code-block:: bash

    cap deploy:web:disable
    cap deploy:web:enable


Zmiana wyświetlanego powodu wyłączenia ``REASON`` i czasu ponownego uruchomienia ``UNTIL``

.. code-block:: bash

    cap deploy:web:disable REASON="database migration" UNTIL="2014-04-08"


Szablon strony z powiadomieniem
-------------------------------

Szablon domyślny ``/usr/lib/ruby/vendor_ruby/capistrano/recipes/deploy/templates/maintenance.rhtml``

.. literalinclude:: ../samples/maintenance.rhtml
    :language: rhtml

Szablon zmodyfikowany ``./maintenance.pl.rhtml``

.. literalinclude:: ../samples/maintenance.pl.rhtml
    :language: rhtml


Aby ``capistrano`` korzystał ze zmodyfikowanego szablonu należy dodać do ``Capfile``

.. code-block:: ruby

    set :maintenance_template_path, "maintenance.pl.rhtml"


.. code-block:: bash

    cap deploy:web:disable REASON="migracji baz danych na nowy serwer" UNTIL="8 kwietnia 2014 o 9:30"


Konfiguracja serwerów www
-------------------------

Apache

.. code-block:: apacheconf

	RewriteCond %{DOCUMENT_ROOT}/maintenance.html -f
	RewriteRule .? maintenance.html [L]

NginX

.. code-block:: nginx

    if (-f /maintenance.html)
    {
        rewrite .? maintenance.html last;
    }