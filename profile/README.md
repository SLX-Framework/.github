# SRX Framework
> Slang Role eXtended – Ein modernes FiveM Framework

## Über uns
SRX ist ein performance-orientiertes FiveM Framework.

## Ressourcen
- [SLX-Core](https://github.com/SLX-Framework/SLX-Core)
- [slang-core](https://github.com/SLX-Framework/slang_core)

## Template
```yaml
name: SLX Framework
version: v1.0.0
author: SLX-Framework
description: SLX Framework - Slang Extended. A modern FiveM Crimelife framework with an ESX Bridge.
requires: 4.0.0
tasks:
  # ============================================================
  # Database Setup
  # ============================================================
  - action: connect_database
  # ============================================================
  # oxmysql
  # ============================================================
  - action: download_file
    path: ./tmp/files/oxmysql.zip
    url: https://github.com/overextended/oxmysql/releases/latest/download/oxmysql.zip
  - action: unzip
    src: ./tmp/files/oxmysql.zip
    dest: ./resources/[standalone]
  - action: waste_time
    seconds: 10
  # ============================================================
  # SLX Core Framework
  # ============================================================
  - action: download_github
    src: https://github.com/SLX-Framework/slx-core
    ref: main
    dest: ./resources/[slx]/slx-core
  - action: waste_time
    seconds: 10
  # ============================================================
  # Slang Core
  # ============================================================
  - action: download_github
    src: https://github.com/SLX-Framework/slang_core
    ref: main
    dest: ./resources/[slx]/slang_core
  - action: waste_time
    seconds: 10
  # ============================================================
  # server.cfg + Logo aus dem Recipe-Repo holen
  # ============================================================
  - action: download_github
    src: https://github.com/SLX-Framework/txAdminRecipe
    ref: main
    dest: ./tmp/recipe
  - action: move_path
    src: ./tmp/recipe/server.cfg
    dest: ./server.cfg
  - action: move_path
    src: ./tmp/recipe/SLX.png
    dest: ./SLX.png
  # ============================================================
  # Cleanup
  # ============================================================
  - action: remove_path
    path: ./tmp
```
