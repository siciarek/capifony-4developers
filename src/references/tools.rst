Narzędzia dodatkowe ``ant``
===========================

Plik konfiguracyjny ``build.xml`` dla ``ant``

.. literalinclude:: ../samples/build.xml
    :language: xml

Przykład użycia
---------------

Wdrożenie zakończone czyszczeniem cache i wgraniem ``assets``

.. code-block:: bash

    $ ant

Reset bazy danych połączony z wgraniem fixtures.

.. code-block:: bash

    $ ant db

Czyszczenie cache i wgranie ``assets``.

.. code-block:: bash

    $ ant cc

Przywrócenie poprzedniej wersji.

.. code-block:: bash

    $ ant rb
