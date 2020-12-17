gwopa.buildout
==============

This is a gwopa buildout configuration for installing GWOPA PMP project management.


Prerequisites
-------------
- Python 2.7
- Python Virtualenv
- Git

Translations
------------

This product has been translated into

- English
- Spanish
- Français

Install
-------

For the default configuration with the GWOPA PMP release::

    $ git clone git@github.com:UPCnet/gwopa.buildout.git
    $ cd gwopa.buildout
    $ ./bin/python bootstrap.py

If you want to install the development version:

    $ ./bin/buildout

Or if you want to use the producction version:

Install ZOPE configuration::

    $ git clone git@github.com:UPCnet/gwopa.buildout.git gwopa.zope
    $ cd gwopa.zope
    $ cp customizeme-zope.in.cfg customizeme.cfg --> edit values to fit your case
    $ ./bin/python bootstrap.py
    $ ./bin/buildout -c zope-only.cfg

Install ZEO configuration::

    $ git clone git@github.com:UPCnet/gwopa.buildout.git gwopa.zeo
    $ cd gwopa.zeo
    $ cp customizeme-zeo.in.cfg customizeme.cfg --> edit values to fit your case
    $ ./bin/python bootstrap.py   
    $ ./bin/buildout -c zeo-only.cfg


Fire up Zope and maybe the ZEO Server::

    $ ./bin/zeo1 start --> ZEO
    $ ./bin/zc1 start --> ZOPE
    $ ./bin/zc2 start --> ZOPE
    $ ./bin/zc3 start --> ZOPE
    $ ./bin/zc4 start --> ZOPE
    $ ./bin/zcdebug fg --> Debug ZOPE
    $ ./bin/instance start --> DEVELOPMENT

Point your webbrowser to http://localhost:8899 (username admin, password admin)
and install a Plone instance, and in portal_quickinstaller, install gwopa.core

Add in url site /@@setup_home, for create demo

That's all, folks.


Extend the config
-----------------

For your own projects, you might extend the configuration. Use a different
PORT, add some more eggs, like::

Development
-----------

    [instance] 
    recipe = plone.recipe.zope2instance
    http-address = 8899
    user = admin:admin
    effective-user = plone
    develop = 
    	gwopa.core
    	gwopa.theme


Production
----------

zeo-only.cfg

    [buildout]
    extends = deploy/zeo-default.cfg

    [zeoserver]
    zeo-address = 8001

zope-only.cfg

    [buildout]
    extends = deploy/zope-default.cfg

    [ports]
    zc1 = 11001
    zc2 = 11002
    zc3 = 11003
    zc4 = 11004
    zcdebug = 11901 

License
-------

The project is licensed under the GPLv2.