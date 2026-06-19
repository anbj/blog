---
title: "Casiorama"
date: 2026-05-07T11:33:45+02:00
draft: false
---

*Sist oppdatert: 27.05.2026*

Intro
-----
I går, **6. mai 2026**, mottok jeg pakke i posten med mine **tre nye Casioklokker**.
De ble kjøpt etter inspirasjon av `Stop Buying the Casio F-91W (Get These Instead) <https://www.youtube.com/watch?v=TfFg_RifcQE>`__.
Fikk tak i følgende, men mangler ``w217h``, som jeg også tenke meg å teste:

* `f-91w <https://www.urverket.no/casio/youth/f-91w-1yeg/1169152>`__
* `f-105w <https://www.urverket.no/casio/collection/f-105w-1awyef/17637>`__
* `w-59 <https://www.urverket.no/casio/collection/w-59-1vqes/17980>`__
* `w-217h <https://www.urverket.no/casio/classic/w-217h-1avdf/885621>`__ - **ny**, 14.mai.

Den 14. mai endte jeg nå opp med å kjøpe ``w-217h``.
Da får jeg **alle** klokkene som jeg synes er relevante for meg fra videoen over.

Utpakking gikk fint.
I dag prøver jeg ``w-59``'en.

Samtlige av klokkene - inkludert min gamle ``f-91w`` og ``ae-1200``, fikk tiden stilt presist ca. kl. 23:30 den **6.mai**.
Dette gir **UNIX time**::

  $ date -d '2026-05-06 23:30' +'%s'
  1778103000

Sjekk driften på dem om et par ukers tid.
Mon tro om den *nye* ``f-91w`` har samme drift som den *gamle*..?

*Oppdatering 27. mai:*
Så er ``w-217h`` hentet på posten.
Jeg skal straks *unboxe*.

Denne ble stilt 23:45 den **27.mai**, **UNIX time** (dette går som **28. mai** i tabellen)::

  $ date -d '2026-05-27 23:45' +'%s'
  1779918300

----

Logg
----
Under følger oversikt over klokker jeg har testet.

.. list-table:: Testoversikt - klokker
  :header-rows: 1

  * - Klokke
    - Fra dato
    - Til dato
    - Dato stilt (UNIX time)
  * - ``w-59``
    - 7. mai
    - 13. mai
    - 1778103000
  * - ``f-105w``
    - 13. mai
    - 20. mai
    - 1778103000
  * - ``f-91w``
    - 20. mai
    - 27. mai
    - 1778103000
  * - ``w-217h``
    - 27. mai
    - 19. juni
    - 1779918300

----

Review
------
``w-59``
""""""""
Så har jeg hatt på meg ``w-59`` i én uke.
Det er egentlig veldig lite å si - på den gode måten.
Den likner veldig - og føles utrolig - lik, ``f-91w``.
Lite oppsiktsvekkende, på den gode måten.

Next up, ``f-105w``.

.. image:: w59.png

``f-105w``
""""""""""
Så har jeg gått med ``f-105w`` i én uke.
Det første jeg tenker, er at dette er en klokke som ser skikkelig tøff ut, med den blå farge, og *litt* kantete uttrykket.
Denne likte jeg veldig godt.
Next up er klassikeren... ``f-91w``.

**PS**: venter på at ``w-217h`` kommer i postkassen.

.. image:: f105w.png

``f-91w``
---------
Så har det vært klassikerens uke, nemlig ``f-91w``.
Som forventet var dette en følelse jeg hadde godt i minne.
Størrelsen er liten, den nærmest smelter bort på armen.
Det dårlige, dog sjarmerende, *backlighten*.
Som med de andre modellene jeg har prøvd så får jeg av og til på fornemmelsen at reimen er *litt mindre og trangere*, enn den var på min originale ``f-91w``.
Jeg vil tro at objektivt sett er reimen helt lik.
Reimen gir seg muligens litt over tid.

Next up er klokken det kanskje knytter seg mest spenning til, nemlig ``w-217h``.

.. image:: f91w.png

``w-217h``
----------
Så har jeg fått med ``w-217h`` er god stund.
Tatt forventningene i betraktning, synes jeg ikke klokken utmerket seg spesielt.
Isolert sett er den bra, men det står ikke i forhold til prisen.
Én av grunnene til at jeg var spent på klokken, var at den ifølge Youtube-videoen over skulle ha høy alarm-lyd.
Jeg synes ikke det var forskjell på alarmlyden på denne og e.g. ``f-91w``.
Det er en god klokke, men jeg kommer nok ikke til å kjøpe den igjen.
Av de nye klokkene er det denne som har gitt minst positivt inntrykk.

Nå har jeg testet alle de nye klokkene.
Spørsmålet nå er hvilken jeg vil bruke fremover..
Og etter å ha tenkt litt, har jeg nå tatt på meg ``f-105w``.

.. image:: w217h.png

Drift
-----
Her er driften for de ulike klokkene.
Utført 17. juni 2026::

  klokke	unix stilt [s]	unix sjekket [s]	testintervall [s]	testintervall [døgn]	Visningtid ved sjekk	drift [s]	drift [s/s]		drift [s/24h]		drift reciprocal [døgn/1]
  w-59		1778103000	1781648896		3545896			41.040462962963		1781648900		4		1.12806466969138E-06	0.0974647874613356	10.2601157407407
  f-105w	1778103000	1781648896		3545896			41.040462962963		1781648907		11		3.10217784165131E-06	0.268028165518673	3.73095117845118
  f-91w		1778103000	1781648896		3545896			41.040462962963		1781648900		4		1.12806466969138E-06	0.0974647874613356	10.2601157407407
  w-217h	1779918300	1781648940		1730640			20.0305555555556	1781648949		9		5.20038829565941E-06	0.449313548744973	2.22561728395062
  ae-1200	1778103000	1781648896		3545896			41.040462962963		1781648896		0		0			0			#DIV/0!
  f-91w (old)	1778103000	1781648896		3545896			41.040462962963		1781648924		28		7.89645268783969E-06	0.682253512229349	1.46573082010582
