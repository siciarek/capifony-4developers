Sprawdzanie ustawień na serwerze lokalnym i zdalnym
===================================================

Aby umożliwić sprawdzenie ustawień na lokalnym i zdalnym serwerze ``Capistrano`` udostępnia polecenie

.. code-block:: bash

    $ cap deploy:check

W wersji podstawowej sprawdza obecność i prawa dostępu do katalogów utworzonych poleceniem

.. code-block:: bash

    $ cap deploy:setup

Dostępność komendy ``tar`` na zdalnym serwerze oraz ``programu do kontroli wersji`` na lokalnym.

Wyświetlane są tylko efekty działania komendy sprawdzającej na zdalnym serwerze, chyba, że pojawią
się błędy, wtedy wyświetlane są w postaci komunikatu np.:

.. code-block:: none

    The following dependencies failed. Please check them and try again:
    --> `git' could not be found in the path on the local host
    --> `setfacl' could not be found in the path (ekk.sescom.pl)

Jeżeli sprawdzanie zakończy się sukcesem pojawi się komunikat:

.. code-block:: none

    You appear to have all necessary dependencies installed


Aby umożliwić dodawanie sprawdzania zasobów ``Capistrano`` udostępnia metodę ``depend`` Przyjmującą 3 argumenty

**Pierwszy parametr** określa miejsce sprawdzania, może przyjmować poniższe wartości:

  * ``:local`` jeżeli chcemy sprawdzać serwer z którego przeprowadzamy wdrożenie
  * ``:remote`` jeżeli chcemy sprawdzić zdalne serwery.


**Drugi parametr** określa typ sprawdzanego zasobu i może przyjmować poniższe wartości:

  * ``:directory`` sprawdza czy istnieje katalog.
  * ``:file`` sprawdza czy istnieje plik.
  * ``:writable`` sprawdza czy katalog lub plik posiada prawa do zapisu.
  * ``:command`` sprawdza czy komenda jest dostępna.
  * ``:deb`` sprawdza czy pakiet jest zainstalowany.

**Trzeci parametr** to nazwa sprawdzanego zasobu w postaci ``łańcucha znaków``.


Przykłady użycia
----------------

.. code-block:: ruby

    depend :local,  :command, "convert"
    depend :remote, :command, "setfacl"

