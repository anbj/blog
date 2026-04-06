---
title: "Rst Test"
date: 2026-04-06T16:35:27+02:00
draft: false
---

Test for å se hvordan rst funker.


``ps(1)`` - *report a snapshot of the current processes*
========================================================
* ``ps(1)`` **displays information about a selection of the active processes**.
* Kort **info om ulike pid-klasser**.
  Det finnes fire ``pid``-klasser.
  Se også *Advanced Programming in the UNIX Environment: Week 07, Segment 4 - Signals* i [CS631]_.

  Fra ``wait(2)``::

    The value of pid can be:

    < -1   meaning wait for any child process whose process group ID is
           equal to the absolute value of pid.

    -1     meaning wait for any child process.

    0      meaning wait for any child process whose process group ID is
           equal to that of the calling process at the time of the call to
           waitpid().

    > 0    meaning wait for the child whose process ID is equal to the
           value of pid.

* ``ps(1)`` kan bruke flere måter å spesifisere argumenter på:

  * *UNIX options, which may be grouped and must be preceded by a dash*
  * *BSD options, which may be grouped and must not be used with a dash.*
  * *GNU long options, which are preceded by two dashes.*

* Den enkleste bruken er å **angi pid**.
  ``u`` gir mer info::

    $ ps 6520
        PID TTY      STAT   TIME COMMAND
       6520 pts/3    Ss     0:00 bash

  ::

    $ ps u 6520
    USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    anbj        6520  0.0  0.0   7540  4384 pts/3    Ss   21:51   0:00 bash

* Min **vanlige bruk** er å kjøre ``ps aux``, som gir **all processes, show user name og show processes som ikke har controlling terminal**.
  Legg på ``f`` for å få **tree view** og ``--headers`` for å få **repetert headerene** regelmessig.

  Merk at ``TTY`` her står som ``?``.
  Det betyr at prosessen **ikke er tilknyttet noen terminal**::

    $ ps aux
    USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root           1  0.0  0.0 169448 14088 ?        Ss   Oct10   0:05 /sbin/init
    root           2  0.0  0.0      0     0 ?        S    Oct10   0:00 [kthreadd]
    root           3  0.0  0.0      0     0 ?        I<   Oct10   0:00 [rcu_gp]
    [...]

  Alternativt kan man bruke ``ps cax``, som gir kortere **cmd-navn**::

    $ ps cax
        PID TTY      STAT   TIME COMMAND
          1 ?        Ss     0:02 systemd
          2 ?        S      0:00 kthreadd
          3 ?        S      0:00 pool_workqueue_release
    [...]

* Ved å endre argumentene, får man (som regel) forskjellig uttrekk av informasjon om prosessene.
  ``-f`` gir mye mer informasjon om hver prosess::

    $ ps -ef
    UID          PID    PPID  C STIME TTY          TIME CMD
    root           1       0  0 Oct10 ?        00:00:05 /sbin/init
    root           2       0  0 Oct10 ?        00:00:00 [kthreadd]
    root           3       2  0 Oct10 ?        00:00:00 [rcu_gp]
    [...]

  Eller ``-el``::

    $ ps -el
    F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
    4 S     0       1       0  0  80   0 - 42362 -      ?        00:00:05 systemd
    1 S     0       2       0  0  80   0 -     0 -      ?        00:00:00 kthreadd
    1 I     0       3       2  0  60 -20 -     0 -      ?        00:00:00 rcu_gp
    [...]

* Vis status for prosesser startet fra **dette terminalvinduet**.
  Legg på ``-l`` for å få mer informasjon om prosessene::

    $ ps
        PID TTY          TIME CMD
     396511 pts/6    00:00:00 bash
     396522 pts/6    00:00:00 ps

* For å liste alle prosessene tilknyttet brukeren med ``uid``, bruk følgende::

    $ ps -fu 1000
    UID          PID    PPID  C STIME TTY          TIME CMD
    anbj        2719       1  0 Oct10 ?        00:00:01 /lib/systemd/systemd --user
    anbj        2720    2719  0 Oct10 ?        00:00:00 (sd-pam)
    anbj        2795    2719  0 Oct10 ?        00:00:43 /usr/bin/pipewire
    [...]

* Outputten kan også defineres selv med ``-o``, som betyr **user-defined format** og ``-e`` er **all processes**, e.g.::

    $ ps -eo "[options]"

  Tre eksempler::

    $ ps -waxo pid,ppid,command
        PID    PPID COMMAND
          1       0 /sbin/init
          2       0 [kthreadd]
          3       2 [rcu_gp]

  ::

    $ ps -o pid,ppid,pgid,sid,comm
        PID    PPID    PGID     SID COMMAND
     424580  424541  424580  424580 bash
     424598  424580  424598  424580 ps

  ::

    $ ps -o pid,ppid,stat,comm
        PID    PPID STAT COMMAND
     764332  763656 Ss   bash
     764341  764332 R+   ps

* ``ps(1)`` markerer **login-shell** med en bindestrek foran navnet, e.g.::

    $ ps aux | grep bash
    anbj        3416  0.0  0.0  10148  5512 pts/1    Ss   Sep28   0:00 -bash
    anbj        3814  0.0  0.0  10296  3780 pts/1    S+   Sep28   0:00 socat -v -ddd EXEC:bash /var/tokt2023/7-output-nmea-every-sec.sh TCP-LISTEN:2948,reuseaddr,fork,bind=127.0.0.1
    anbj        3819  0.1  0.0   6932  2792 pts/1    S+   Sep28  10:28 bash /var/tokt2023/7-output-nmea-every-sec.sh
    anbj     1097773  0.0  0.0  10296   780 pts/1    S+   09:33   0:20 socat -v -ddd EXEC:bash /var/tokt2023/7-output-nmea-every-sec.sh TCP-LISTEN:2948,reuseaddr,fork,bind=127.0.0.1
    anbj     1186820  0.0  0.0   7576  4428 pts/0    Ss   15:22   0:00 bash

* **Cheat sheet**::

    | code | normal | header  |
    |------|--------|---------|
    | %C   | pcpu   | %CPU    |
    | %G   | group  | GROUP   |
    | %P   | ppid   | PPID    |
    | %U   | user   | USER    |
    | %a   | args   | COMMAND |
    | %c   | comm   | COMMAND |
    | %g   | rgroup | RGROUP  |
    | %n   | nice   | NI      |
    | %p   | pid    | PID     |
    | %r   | pgid   | PGID    |
    | %t   | etime  | ELAPSED |
    | %u   | ruser  | RUSER   |
    | %x   | time   | TIME    |
    | %y   | tty    | TTY     |
    | %z   | vsz    | VSZ     |

* Flere **eksempler**.

  * En grei kommando å bruke er::

      $ ps -eo "%U %G %p %a"

    Da får man i tillegg opp hvilke ``group`` som prosessen kjører med.

  * Dersom man vil se informasjon om *threads*, prøv::

      $ ps m

  * For å liste alle prosesser eid av *user*, bruk::

      $ ps -u user

  * Enda et eksempel::

      $ ps -o pid,ppid,pgid,sid,comm

  * Og enda ett::

      $ ps -eo user,pid,nice,cmd
      USER         PID  NI CMD
      root           1   0 /sbin/init
      root           2   0 [kthreadd]
      root           3   0 [pool_workqueue_release]
      [...]

* For mer hjelp, prøv::

    $ ps --help

    Usage:
     ps [options]

     Try 'ps --help <simple|list|output|threads|misc|all>'
      or 'ps --help <s|l|o|t|m|a>'
     for additional help text.

    For more details see ps(1).

Les mer:

* ``ps(1)``
