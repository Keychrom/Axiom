.. _architecture:

============
Architecture
============

.. sidebar:: Further reading

   - Reverse Proxy: :ref:`Apache <apache searxng site>` & :ref:`nginx <nginx
     searxng site>`
   - uWSGI: :ref:`axiom uwsgi`
   - AXIOM: :ref:`installation basic`

Herein you will find some hints and suggestions about typical architectures of AXIOM infrastructures.

.. _architecture uWSGI:

uWSGI Setup
===========

We start with a *reference* setup for public AXIOM instances which can be build
up and maintained by the scripts from our :ref:`toolboxing`.

.. _arch public:

.. kernel-figure:: arch_public.dot
   :alt: arch_public.dot

   Reference architecture of a public AXIOM setup.

The reference installation activates ``server.limiter`` and
``server.image_proxy`` (:origin:`/etc/axiom/settings.yml <utils/templates/etc/axiom/settings.yml>`)

.. literalinclude:: ../../utils/templates/etc/searxng/settings.yml
   :language: yaml
   :end-before: # preferences:
