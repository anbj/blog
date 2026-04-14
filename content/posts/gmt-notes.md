---
title: "GMT notes"
date: 2026-04-13T13:57:25+02:00
draft: false
---

## grdmath

* Her bruker vi **feature scaling**.
  Først dropper vi å angi `a` og `b`, som normaliserer mellom 0 - 1.
  Deretter samme, men med **NORM**, som gir samme resultat.
  Deretter normaliserer vi med -1 - 1.
  Til sist skalert etter **eget ønske**, -5000 - 5000:

  ```
  $ gmt grdmath -RSJ @earth_faa_01m -116.625 SUB 231.725006104 -116.625 SUB DIV = norm_0_1.nc

  $ gmt grdmath -RSJ  @earth_faa_01m NORM = norm_NORM.nc

  $ gmt grdmath -RSJ -1 @earth_faa_01m.tif -116.625 SUB 231.725006104 -116.625 SUB DIV 1 -1 SUB MUL ADD = norm_-1_1.nc

  $ gmt grdmath -RSJ -5000 @earth_faa_01m.tif -116.625 SUB 231.725006104 -116.625 SUB DIV 5000 -5000 SUB MUL ADD = norm_5000.nc
  ```

  For **NORM**, se `gmt/src/grdmath.c` linje 4140.
  Den bruker følgende:

  ```
  a = (n == 0 || zmax == zmin) ? GMT->session.f_NaN : (1.0 / (zmax - zmin));^I/* Normalization scale */
  ```

  Les mer:

  * [Rescaling (min-max normalization)](https://en.wikipedia.org/wiki/Feature_scaling#Rescaling_(min-max_normalization))

## grdcut
* Test [-D[+t]](https://docs.generic-mapping-tools.org/dev/grdcut.html#d) for **dry run**.
* Test [-Slon/lat/radius[+n]](https://docs.generic-mapping-tools.org/dev/grdcut.html#s) for å angi **origin og radius**.
