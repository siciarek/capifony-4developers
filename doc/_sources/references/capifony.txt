Capifony - Capistrano dla Symfony
=================================

``Capifony`` jest napisanym w języku ``ruby`` systemem zdalnego zarządzania zasobami serwerów,
dedykowanego do wdrożeń projektów ``Symfony``.

Instalacja
----------

``Capifony`` jest dostępny jako pakiet ``gem`` dla ``ruby``.

.. code-block:: bash

    $ gem -v
    1.8.23

Najniższa wymagana wersja to ``1.3.x``, jeżeli nie nie posiadasz takiej, należy przeprowadzić aktualizację a następnie wykonać komendę:

.. code-block:: bash

    $ gem install capifony

Po pomyślnie wykonanej instalacji powinno być możliwe wykonanie poniższej komendy:

.. code-block:: none

    $ capifony --help
    Usage: capifony [path]
        -h, --help                       Displays this help info
        -v, --version
        -s, --symfony VERSION            Capify specific symfony version (1|2)
        -p, --app NAME                   Specify app name (folder) to capify

