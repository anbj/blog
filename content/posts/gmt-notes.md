---
title: "GMT notes"
date: 2026-04-13T13:57:25+02:00
draft: false
---

## grdmath

* Her normaliserer vi et grid med to ulike kommandoer.
  Dette gir **samme resultat**:

  ```
  $ gmt grdmath -RSJ  @earth_faa_01m  -116.625 SUB 231.725006104 -116.625 SUB DIV = norm.nc

  $ gmt grdmath -RSJ  @earth_faa_01m NORM = norm2.nc
  ```

* Her bruker vi **feature scaling**.
  Først, **default**, hvor verdien blir mellom 0 - 1, deretter skalert etter eget ønske, -5000 - 5000:

  ```
  $ gmt grdmath -RSJ @earth_faa_01m.tif -116.625 SUB 231.725006104 -116.625 SUB DIV = norm_0_1.nc

  $ gmt grdmath -RSJ -1 @earth_faa_01m.tif -116.625 SUB 231.725006104 -116.625 SUB DIV 1 -1 SUB MUL ADD = norm_-1_1.nc

  $ gmt grdmath -RSJ -5000 @earth_faa_01m.tif -116.625 SUB 231.725006104 -116.625 SUB DIV 5000 -5000 SUB MUL ADD = norm_5000.nc
  ```

  Merk at man her kan justere min og max, utfira hvilke verdier man er på jakt etter, tror jeg.

  Les mer:

  * [Rescaling (min-max normalization)](https://en.wikipedia.org/wiki/Feature_scaling#Rescaling_(min-max_normalization))

## grdcut
* Test [-D[+t]](https://docs.generic-mapping-tools.org/dev/grdcut.html#d) for **dry run**.
* Test [-Slon/lat/radius[+n]](https://docs.generic-mapping-tools.org/dev/grdcut.html#s) for å angi **origin og radius**.
