Narzędzie do synchronizacji katalogów ``rsync``
===============================================

Rsync jest aplikacją do synchronizacji katalogów na sewerze lokalnym i zdalnym, w obu kierunkach.

Strona projektu http://rsync.samba.org.

Szczegółowa dokumentacja http://rsync.samba.org/ftp/rsync/rsync.html.

Przykład sparametryzowanej komendy ``rsync``
--------------------------------------------

.. code-block:: bash

    SOURCE=.
    TARGET=dude@target.server.com:/var/www/target.server.com

    rsync \
    --itemize-changes \
    --verbose  \
    --human-readable \
    --omit-dir-times \
    --times \
    --perms \
    --progress \
    --stats \
    --compress \
    --recursive \
    --links \
    --delete \
    --exclude-from="config/rsync_exclude.txt" \
    --dry-run \
    $SOURCE $TARGET

Przykładowy wynik działania komendy ``rsync``
---------------------------------------------

.. code-block:: none

    sending incremental file list
    .L..t...... lib/doctrine/linked_schema.yml -> ../../data/linked_schema.yml
    *deleting   web/apc.php
    <f.st...... web/import.php

    Number of files: 10047
    Number of files transferred: 1
    Total file size: 150.32M bytes
    Total transferred file size: 2.76K bytes
    Literal data: 0 bytes
    Matched data: 0 bytes
    File list size: 210.08K
    File list generation time: 0.001 seconds
    File list transfer time: 0.000 seconds
    Total bytes sent: 211.97K
    Total bytes received: 1.49K

    sent 211.97K bytes  received 1.49K bytes  9.08K bytes/sec
    total size is 150.32M  speedup is 704.24 (DRY RUN)


Jak rozumieć format opisu zmiany
--------------------------------

.. code-block:: none

    *deleting   web/apc.php
    <f+++++++++ newfile.txt
    .L..t...... lib/doctrine/linked_schema.yml -> ../../data/linked_schema.yml
    <f.st...... web/import.php

Format opisu

.. code-block:: none

    YXcstpoguax

Gdzie

**Y**
    | **<** - plik został wysłany na **serwer zdalny**.
    | **>** - plik został pobrany ze **zdalnego serwera**.
    | **c** - element został lokalnie utworzony np. nowy katalog, lub link symboliczny.
    | **h** - oznacza, że dany element jest twardym linkiem (wymaga argumentu ``--hard-links``).
    | **.** - plik nie został zmieniony, ale zmieniły się inne parametry pliku.
    | ***** - prefiks dalszej informacji (np. "deleting").

**X**
    | **f** - plik
    | **d** - katalog
    | **L** - link symboliczny
    | **D** - urządzenie
    | **S** - plik specjalny (np. nazwane gniazdo (named socket) lub kolejka fifo).

Pozostałe znaki są literami opisującymi zmienione atrybuty pliku lub **"."**, jeżeli dany atrybut nie został zmieniony, poza trzema wyjątkami:

    * nowoutworzony plik zamienia każdą z liter na znak **"+"**
    * identyczny element zmienia kropki na spacje
    * nieznany atrybut zmieniany jest na znak **"?"** (to się może zdarzyć jeżeli na zdalnym serwerze jest starsza wersja ``rsync``)

**cstpoguax**
    | A c means either that a regular file has a different checksum (requires --checksum) or that a symlink, device, or special file has a changed value. Note that if you are sending files to an rsync prior to 3.0.1, this change flag will be present only for checksum-differing regular files.
    | A s means the size of a regular file is different and will be updated by the file transfer.
    | A t means the modification time is different and is being updated to the sender's value (requires --times). An alternate value of T means that the modification time will be set to the transfer time, which happens when a file/symlink/device is updated without --times and when a symlink is changed and the receiver can't set its time. (Note: when using an rsync 3.0.0 client, you might see the s flag combined with t instead of the proper T flag for this time-setting failure.)
    | A p means the permissions are different and are being updated to the sender's value (requires --perms).
    | An o means the owner is different and is being updated to the sender's value (requires --owner and super-user privileges).
    | A g means the group is different and is being updated to the sender's value (requires --group and the authority to set the group).
    | The u slot is reserved for future use.
    | The a means that the ACL information changed.
    | The x means that the extended attribute information changed.

Można użyć argumentu ``--out-format`` aby dostosować wyjście do swoich potrzeb.

