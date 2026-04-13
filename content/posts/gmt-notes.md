---
title: "GMT notes"
date: 2026-04-13T13:57:25+02:00
draft: false
---

## ``grdmath``

* Her normaliserer vi et grid med to ulike kommandoer

```
~ $ gmt grdmath -RSJ  @earth_faa_01m  -116.625 SUB 231.725006104 -116.625 SUB DIV = norm.nc

~ $ gmt grdmath -RSJ  @earth_faa_01m NORM = norm2.nc
```
