---
layout: default
title: CLBoss
parent: + Lightning
grand_parent: Bonus Section
nav_exclude: true
has_toc: false
---
<!-- markdownlint-disable MD014 MD022 MD025 MD033 MD040 -->

# Bonus guide: CLBoss

{: .no_toc }

---

[CLBoss](https://github.com/ZmnSCPxj/clboss){:target="_blank"} is an automated manager for CLN nodes. It's capable of automatically opening channels to useful nodes, acquiring inbound capacity through boltz swaps, rebalancing existing channels and setting competitive forwarding fees.
Read more about it [here](https://zmnscpxj.github.io/clboss/index.html){:target="_blank"}.

Difficulty: Easy
{: .label .label-green }

Status: Not tested MiniBolt
{: .label .label-red }

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Introduction

CLBoss - an automated CLN node management tool. This guide shows how to install and setup an existing CLN node with CLBoss plugin.

---

## Requirements

* CLN

---

## Installation

We will download, install and setup CLBoss on your RaspiBolt CLN node. CLBoss is a plugin that we will place into `/data/lightningd-plugins-available/` and load via CLN's configuration file.

## Dependencies

* As "admin", install required dependencies to compile CLBoss's source code.

  ```sh
  $ sudo apt install -y build-essential pkg-config libev-dev \
                      libcurl4-gnutls-dev libsqlite3-dev dnsutils
  ```

* Switch back to user "lightningd".

  ```sh
  $ sudo su - lightningd
  ```

* Download latest version and untar it to CLN's plugin folder `/data/lightningd-plugins-available`.

  ```sh
  $ cd /data/lightningd-plugins-available
  $ wget https://github.com/ZmnSCPxj/clboss/releases/download/v0.12/clboss-0.12.tar.gz
  $ tar xfv clboss-0.12.tar.gz
  $ cd clboss-0.12
  ```

## Compilation

* Compile it.

    ```sh
  $ ./configure
  $ make
  ```

## Configuration

* Add the plugin to CLN config.

  ```sh
  $ nano /data/lightningd/config
  ```

* Append this line to end of file:

  ```ini
  plugin=/data/lightningd-plugins-available/clboss-0.12/clboss
  ```

## Restart Service

* As "admin", reload CLN configuration by restarting the service:

  ```sh
  $ sudo systemctl restart lightningd.service
  ```

* Check if it's running.

  ```sh
  $ sudo tail -f /data/lightningd/cl.log
  ```

* It should output log entry infos like these:

  ```
  INFO    plugin-clboss: clboss 0.12
  INFO    plugin-clboss: ChannelFeeManager: zerobasefee: allow
  INFO    plugin-clboss: New block at xxxxxx
  INFO    plugin-clboss: Started.
  ```

<br /><br />

---

<< Back: [+ Lightning](index.md)
