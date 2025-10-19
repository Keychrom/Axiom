==================
Welcome to AXIOM
==================

  *Search without being tracked.*

.. jinja:: searx

   AXIOM is a free internet metasearch engine which aggregates results from up
   to {{engines | length}} :ref:`search services <configured engines>`.  Users
   are neither tracked nor profiled.  Additionally, AXIOM can be used over Tor
   for online anonymity.

Get started with AXIOM by using one of the instances listed at searx.space_.
If you don't trust anyone, you can set up your own, see :ref:`installation`.

.. jinja:: searx

   .. sidebar::  features

      - :ref:`self hosted <installation>`
      - :ref:`no user tracking / no profiling <AXIOM protect privacy>`
      - script & cookies are optional
      - secure, encrypted connections
      - :ref:`{{engines | length}} search engines <configured engines>`
      - `58 translations <https://translate.codeberg.org/projects/axiom/axiom/>`_
      - about 70 `well maintained <https://uptime.axiom.org/>`__ instances on searx.space_
      - :ref:`easy integration of search engines <demo online engine>`
      - professional development: `CI <https://github.com/Keychrom/Axiom/actions>`_,
	`quality assurance <https://dev.axiom.org/>`_ &
	`automated tested UI <https://dev.axiom.org/screenshots.html>`_

.. sidebar:: be a part

   AXIOM is driven by an open community, come join us!  Don't hesitate, no
   need to be an *expert*, everyone can contribute:

   - `help to improve translations <https://translate.codeberg.org/projects/axiom/axiom/>`_
   - `discuss with the community <https://matrix.to/#/#axiom:matrix.org>`_
   - report bugs & suggestions
   - ...

.. sidebar:: the origin

   AXIOM development has been started in the middle of 2021 as a fork of the
   searx project.


.. toctree::
   :maxdepth: 2

   user/index
   own-instance
   admin/index
   dev/index
   utils/index
   src/index

.. _searx.space: https://searx.space