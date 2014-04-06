Zdefiniowane zadania ``tasks`` i wyzwalacze ``triggers``
========================================================

Zdefiniowane zadania są sposobem na rozszerzenie podstawowych funkcjonalności
udostępnianych przez ``cap``.

Najprostszy ``task`` prezentujący jednynie strukturę

.. code-block:: ruby

    desc 'To jest task testowy.'
    task :dummy do
        # do nothing.
    end

Wersja z bogatszym opisem

.. code-block:: ruby

    desc <<-DESC
        To jest task testowy. Task testowy "dummy" \
        służy wyłącznie do prezentacji sposobu budowania tasków \
        i nie powinien zawierać żadnych istotnych elementów.
    DESC
    task :dummy do
        # do nothing.
    end

Użycie zdefiniowanego zadania

.. code-block:: bash

    $ cap dummy


Bardziej użyteczny task wgrywający ``parameters.yml`` do katalogu aplikacji.

.. code-block:: ruby

    desc <<-DESC
        Kopiuje plik konfiguracyjny aplikacji. Plik konfiguracyjny \
        nie powinien być częścią repozytorium, ponieważ zawiera dane niejawne \
        jak np. hasło dostępowe do serwera bazy danych.
    DESC
    task :upload_parameters do
        origin_file = "parameters.yml"
        destination_file = shared_path + "/app/config/#{origin_file}" # Notice the shared_path

        try_sudo "mkdir -p #{File.dirname(destination_file)}"
        top.upload(origin_file, destination_file)
    end

    before "deploy:share_childs", "upload_parameters"

Wgrywanie i usuwanie front controllera debugującego.

.. code-block:: ruby

    desc <<-DESC
        Wgraj front kontroler debugujący.
    DESC
    task :dbg do
        origin_file = "app_dev.php"
        destination_file = deploy_to + "/current/web/" + origin_file
        top.upload(origin_file, destination_file)
    end

.. code-block:: ruby

    desc <<-DESC
        Usuń front kontroler debugujący.
    DESC
    task :undbg do
        origin_file = "app_dev.php"
        destination_file = deploy_to + "/current/web/" + origin_file
        try_sudo "rm -rvf #{destination_file}"
    end

Działanie powyższego zbliżone jest do ``cap symfony:project:clear_controllers``.


Wyzwalacze (triggers)
---------------------

Wyzwalacze pozwalają na automatyczne uruchamianie zadań wbudowanych lub zdefiniowanych
w przypadku zaistnienia odpowiedniego zdarzenia ``event``.

Składnia

.. code-block:: ruby

    cut_point, "zadanie_docelowe", "zadanie_do_wykonania_w_kontekscie", "kolejne_zadanie_do_wykonania_w_kontekscie", ...

Obecnie ``capistrano`` obsługuje poniższe punkty wcięcia ``cut_point`` (aspect programming domain):

.. code-block:: ruby

    # * :before, uruchamia podane zadanie/zadania przed wywołaniem danego zdarzenia docelowego
    # * :after, po wywołaniu danego zdarzenia docelowego
    # * :start, przed uruchomieniem głównego zadania
    # * :finish, po zakończeniu głównego zadania
    # * :load, po załadowaniu wszystkich zadań
    # * :exit, po wykonaniu wszystkich zadań


Są jeszcze bardziej wymyślne konstrukcje, do zobaczenia w dokumentacji (w kodzie) ``capistrano/callback``.
