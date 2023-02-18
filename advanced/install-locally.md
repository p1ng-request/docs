---
description: >-
  The following details are provided to aid developers to quickly install naas
  locally.
---

# Install Locally

## Naas Prerequisites

In order to set up Naas, docker is required. Set up Docker with the help of the [Docker official installation guides](https://docs.docker.com/engine/install/).

_**Note:**_ Setting up Naas locally only enables schedulers. In order to access all the features make use of Naas Cloud.

## Run locally

### **Runtime dependencies**

The following dependencies are necessary for Naas at runtime:

* Docker
* Make (not necessary if you choose to use docker-compose directly on Windows, Linux, or macOS).

### Run

**Linux / macOS**

```
make
```

Then you can go on [http://localhost:8888/lab?token=naas](http://localhost:8888/lab?token=naas)

**Windows**

Double click on the file `windows_start.bat`, this will open a terminal, start naas and open your browser on [http://localhost:8888/lab?token=naas](http://localhost:8888/lab?token=naas).

### Stop

**Linux / macOS**

`make stop`

```
make stop
```

or if you want to delete the container as well you can run

```
make down
```

**Windows**

Double click on `windows_stop.bat`

### Build

Unless you modified something relevant to the `Dockerfile.dev`, you don't need to run this. If it never happened before, the build process is done automatically when running naas (`make` or `make run`).

**Linux / macOS**

```
make build
```

#### Open a shell in the container (root)

**Linux / macOS**

```
make sh
```

### File structure for local development

When you land in your freshly started naas, on the left you should see a file structure like this:

```markup
.
├── awesome-notebooks
├── file_sharing
├── drivers
├── naas
└── Welcome_to_Naas.ipynb
```

When naas is starting, it will automatically mount `../drivers` and `../awesome-notebooks` in your home directory of your naas. This means that if these directories do not exist on your machine it will create them and `git clone` [naas drivers](https://github.com/jupyter-naas/drivers) in `../drivers` and [awesome-notebooks](https://github.com/jupyter-naas/awesome-notebooks) in `../awesome-notebooks`.

`naas` folder corespond to `.` directory on your machine (where naas project is cloned).

`file_sharing` directory is a folder created next to `./naas` to allow easy file sharing between your computer and naas container. Every file that you will drop in this directory, either from naas or from your computer will be accessible on both naas and your machine.

`Welcome_to_Naas.ipynb` is our welcoming notebook to get you a place to start your journey.

### API Documentation

We have a WIP documentation in swagger.

`http://127.0.0.1:5000/swagger/`

### Live reload

If you do change in naas code, the server will live to reload.

If you use naas in a notebook restart the kernel to get the changes.

### Naas Manager

Open Naas manager outside of jupyter context :

`http://localhost:5000/naas`

### Run test

Open Jupyterlab and click on `+` to open Launcher Open Shell Go to the right directory `cd naas` Run it in the shell `pytest -x` to test your code

Each Change you do from your IDE or from jupyter in the Naas folder is live reloaded If you test naas feature inside a notebook reload your kernel between changes. Same for the manager page you have to reload the page to see the changes. To go faster you can use `isolated Manager` to reload only manager and not full jupyterlab

### Check lint

`python -m black naas` format better `python -m flake8 naas` check if any left error

### Publish

You can commit from jupyter or from your local IDE, code of Naas is synced between docker-machine and your computer

This auto publish by GitHub action on the main branch
