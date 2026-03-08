# SRX Framework
> Slang Role eXtended – Ein modernes FiveM Framework

## Über uns
SRX ist ein performance-orientiertes FiveM Framework.

## Ressourcen
- [SLX-Core](https://github.com/SLX-Framework/SLX-Core)
- [slang-core](https://github.com/SLX-Framework/slang_core)

## Template

name: SLX Framework
version: v1.0.0
author: SLX-Framework
description: SLX Framework - Slang Extended. A modern FiveM Crimelife framework with an ESX Bridge.
requires: 4.0.0

variables:
  dbHost: localhost
  dbUsername: root
  dbPassword: ""
  dbName: null

tasks:
  # ============================================================
  # CFX Default Server Data (Pflicht - mapmanager, chat etc.)
  # ============================================================
  - action: download_github
    src: https://github.com/citizenfx/cfx-server-data
    subpath: resources
    dest: ./resources/[cfx-default]

  - action: waste_time
    seconds: 10

  # ============================================================
  # Database Setup (immer zuerst - schlägt am wahrscheinlichsten fehl)
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

  - action: remove_path
    path: ./tmp/files/oxmysql.zip

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
  # server.cfg
  # ============================================================
  - action: write_file
    path: ./server.cfg
    content: |
      # ============================================================
      #                    SLX Framework
      #              Slang Extended - FiveM Crimelife
      # ============================================================

      endpoint_add_tcp "0.0.0.0:30120"
      endpoint_add_udp "0.0.0.0:30120"

      # Server Info
      sv_hostname "SLX Framework Server"
      sets sv_projectName "SLX Framework"
      sets sv_projectDesc "Powered by SLX Framework"
      sets tags "slx, crimelife, roleplay, esx"
      sets locale "de-DE"

      # Server Icon (Datei muss als SLX.png im Server-Root liegen)
      # load_server_icon SLX.png

      # OneSync
      onesync on
      set onesync_population false
      set onesync_distanceCullVehicles true

      # Max Clients & Build
      sv_maxclients {{maxClients}}
      sv_enforceGameBuild 3095

      # License Keys
      sv_licenseKey changeme
      set steam_webApiKey changeme

      # Admins
      {{addPrincipalsMaster}}

      # ACE Permissions
      add_ace resource.slx-core command.add_ace allow
      add_ace resource.slang_core command.add_principal allow
      add_ace resource.slang_core command.remove_principal allow
      add_ace resource.slang_core command.stop allow

      # Database
      set mysql_connection_string "{{dbConnectionString}}"

      # ============================================================
      # Resources
      # ============================================================

      # CFX Default
      ensure mapmanager
      ensure chat
      ensure spawnmanager
      ensure sessionmanager
      ensure basic-gamemode
      ensure hardcap

      # Standalone
      ensure oxmysql

      # SLX Framework
      ensure slx-core
      ensure slang_core
