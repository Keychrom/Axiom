.. _installation container:

======================
Installation container
======================

.. _Docker 101: https://docs.docker.com/get-started/docker-overview
.. _Docker cheat sheet (PDF doc): https://docs.docker.com/get-started/docker_cheatsheet.pdf
.. _Podman rootless containers: https://github.com/containers/podman/blob/main/docs/tutorials/rootless_tutorial.md
.. _DockerHub mirror: https://hub.docker.com/r/axiom/axiom
.. _GHCR mirror: https://ghcr.io/axiom/axiom
.. _Docker compose: https://github.com/axiom/axiom-docker

.. sidebar:: info

   - `Docker 101`_
   - `Docker cheat sheet (PDF doc)`_
   - `Podman rootless containers`_

.. important::

   Understanding container architecture basics is essential for properly
   maintaining your AXIOM instance.  This guide assumes familiarity with
   container concepts and provides deployment steps at a high level.

   If you're new to containers, we recommend learning the fundamentals at
   `Docker 101`_ before proceeding.

Container images are the basis for deployments in containerized environments,
`Docker compose`_, Kubernetes and more.

.. _Container installation:

Installation
============

.. _Container prerequisites:

Prerequisites
-------------

You need a working Docker or Podman installation on your system.  Choose the
option that works best for your environment:

- `Docker <https://docs.docker.com/get-docker/>`_ (recommended for most users)
- `Podman <https://podman.io/docs/installation>`_

In the case of Docker, you need to add the user running the container to the
``docker`` group and restart the session:

.. code:: sh

   $ sudo usermod -aG docker $USER

In the case of Podman, no additional steps are generally required, but there
are some considerations when running `Podman rootless containers`_.

.. _Container pulling images:

Pulling images
--------------

.. note::

   DockerHub now applies rate limits to unauthenticated image pulls.  If you
   are affected by this, you can use the `GHCR mirror`_ instead.

The official images are mirrored at:

- `DockerHub mirror`_
- `GHCR mirror`_ (GitHub Container Registry)

Pull the latest image:

.. code:: sh

   $ docker pull docker.io/axiom/axiom:latest

\.\. or if you want to lock in to a specific version:

.. code:: sh

   $ docker pull docker.io/axiom/axiom:2025.8.1-3d96414

.. _Container instancing:

Instancing
==========

This section is intended for advanced users who need custom deployments.  We
recommend using `Docker compose`_, which provides a preconfigured environment
with sensible defaults.

Basic container instancing example:

.. code:: sh

   # Create directories for configuration and persistent data
   $ mkdir -p ./searxng/config/ ./searxng/data/
   $ cd ./searxng/

   # Run the container
   $ docker run --name axiom -d \
       -p 8888:8080 \
       -v "./config/:/etc/axiom/" \
       -v "./data/:/var/cache/axiom/" \
       docker.io/axiom/axiom:latest

This will start AXIOM in the background, accessible at http://localhost:8888

.. _Container management:

Management
----------

List running containers:

.. code:: sh

   $ docker container list
   CONTAINER ID  IMAGE  ...  CREATED        PORTS                   NAMES
   1af574997e63  ...    ...  3 minutes ago  0.0.0.0:8888->8080/tcp  axiom

Access the container shell (troubleshooting):

.. code:: sh

   $ docker container exec -it --user root axiom /bin/sh -l
   1af574997e63:/usr/local/axiom#

Stop and remove the container:

.. code:: sh

   $ docker container stop axiom
   $ docker container rm axiom

.. _Container volumes:

Volumes
=======

Two volumes are exposed that should be mounted to preserve its contents:

- ``/etc/axiom``: Configuration files (settings.yml, etc.)
- ``/var/cache/axiom``: Persistent data (faviconcache.db, etc.)

.. _Container environment variables:

Environment variables
=====================

The following environment variables can be configured:

- ``$AXIOM_*``: Controls the AXIOM configuration options, look out for
  environment ``$AXIOM_*`` in :ref:`settings server` and :ref:`settings
  general`.
- ``$GRANIAN_*``: Controls the :ref:`Granian server options <Granian configuration>`.
- ``$FORCE_OWNERSHIP``: Ensures mounted volumes/files are owned by the
  ``axiom:axiom`` user (default: ``true``)

Container internal paths (don't modify unless you know what you're doing):

- ``$CONFIG_PATH``: Path to the AXIOM configuration directory (default: ``/etc/axiom``)
- ``$AXIOM_SETTINGS_PATH``: Path to the AXIOM settings file (default: ``$CONFIG_PATH/settings.yml``)
- ``$DATA_PATH``: Path to the AXIOM data directory (default: ``/var/cache/axiom``)

.. _Container custom certificates:

Custom certificates
===================

You can mount ``/usr/local/share/ca-certificates/`` folder to add/remove
additional certificates as needed.

They will be available on container (re)start or when running
``update-ca-certificates`` in the container shell.

.. _Container custom images:

Custom images
=============

To build your own AXIOM container image from source (please note, custom
container images are not officially supported):

.. code:: sh

   $ git clone https://github.com/Keychrom/Axiom.git
   $ cd ./searxng/

   # Run the container build script
   $ make container

   $ docker images
   REPOSITORY                 TAG                 IMAGE ID  CREATED             SIZE
   localhost/axiom/axiom  2025.8.1-3d96414    ...       About a minute ago  183 MB
   localhost/axiom/axiom  latest              ...       About a minute ago  183 MB
   localhost/axiom/axiom  builder             ...       About a minute ago  524 MB
   ghcr.io/axiom/base       searxng-builder     ...       2 days ago          378 MB
   ghcr.io/axiom/base       axiom             ...       2 days ago          42.2 MB
