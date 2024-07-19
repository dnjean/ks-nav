# GETTING STARTED WITH KS-NAV - A BASIC TUTORIAL

## Table of Contents

- [GETTING STARTED WITH KS-NAV - A BASIC TUTORIAL](#getting-started-with-ks-nav---a-basic-tutorial)
  - [Table of Contents](#table-of-contents)
  - [1 Overview](#1-overview)
  - [2 A short tutorial](#2-a-short-tutorial)
    - [2.1 Build Linux for ks-nav](#21-build-linux-for-ks-nav)
    - [2.2 Run ks-nav on the built image](#22-run-ks-nav-on-the-built-image)
  - [3 What happens behind the scene](#3-what-happens-behind-the-scene)
    - [3.1 Configuring Linux to generate a debug build in Linux or Yocto](#31-configuring-linux-to-generate-a-debug-build-in-linux-or-yocto)
    - [3.2 Configuring kern\_bin\_db and the local database](#32-configuring-kern_bin_db-and-the-local-database)
    - [3.3 Configuring an external database](#33-configuring-an-external-database)
    - [3.4 Configuring nav and navweb for caller graph generation](#34-configuring-nav-and-navweb-for-caller-graph-generation)

## 1 Overview

To start using ks-nav, a Linux (or Yocto) build with debug symbols enabled is required. The tool then extracts symbols, functions and any useful data into a PostgreSQL database. 

In this tutorial, you will:

- Build a default branch from Linux - tag v6.6 is used in this tutorial
- Extract symbols into a local database using ksnav-kdb
- Run the navigator using ks-nav

## 2 A short tutorial

### 2.1 Build Linux for ks-nav

Skip this step if you already have a valid Linux build.
The **demo/linux_app** folder includes a pre-configured Linux Configuration file and a Dockerfile.
Use the commands below to create the container that will build the Linux image as defined in the configuration file **linux_config**.

```bash 

    # Move to the demo folder (should be the current directory) 
    cd ./demo
    # delete the ksbuild folder if you want to start with a new environment
    rm -rf ksbuild
    # Run script setup_linux_app to build a vmlinux image for ks-nav
    # The built image should be available under ./demo/ksbuild/app
    ./setup_linux_app
```

At the end of this step, the **ksbuild/app** folder should be populated with the Linux source and build artifacts. 

### 2.2 Run ks-nav on the built image

This step assumes that the **ksbuild/app** folder contains both Linux source and build artifacts.
The artifacts generated from the Linux build in the previous step are now passed to another container - the ksnav container.

```bash

    # Move to the demo folder (should be the current directory)
    cd demo
    # Run the run_ksnav script to build a ks-nav container
    ./run_ksnav
    # Access the container's shell (assuming $LINUX_CONT='linux-cont' in setup_linux_app)
    podman exec -it ksnav-cont sh
    # From the interractive shell, run the following command to:
    # - Extract symbols into a local database using kern_bin_db - the Kernel Source Symbols Extractor and DB Builder
    # - This takes a little while
    cd /app
    nav-db-filler /build/ksnav_kdb.json    
    # - Run the Source code Navigator using nav - which generates call tree graphs. 
    # The graphs are generated via script in the ksbuild/out_img folder
    nav -f /build/ksnav_nav.json > /out_img/run_init_process

```

At the end of this step, folder **./demo/ksbuild/out_img** should be populated with at least one image file of a call tree graph.

## 3 What happens behind the scene

Coming soon

### 3.1 Configuring Linux to generate a debug build in Linux or Yocto

### 3.2 Configuring kern_bin_db and the local database

### 3.3 Configuring an external database

### 3.4 Configuring nav and navweb for caller graph generation
