=====================
A-musing-moose's blog
=====================

Installation
------------

`Jekyll`_ is required. Follow the install instructions at the `Jekyll wiki`_.
You can install this via RubyGems::

    sudo gem install jekyll

.. _`Jekyll`: https://github.com/mojombo/jekyll/
.. _`Jekyll wiki`: https://github.com/mojombo/jekyll/wiki/Install

OSX users might need to update RubyGems::

    sudo gem update --system

Building and viewing
--------------------

GitHub automatically builds Jekyll-based sites. If you want to make changes and
edit locally, you'll need to install Jekyll (see above).

Running a local server
----------------------

Change directory into the `django-oscar` directory, and build by::

    jekyll --server --base-url="" --auto
    
where ``--base-url`` is an option to override the baseurl setting in
``_config.yml``. This setting is used in the templates as the placeholder ``{{
site.baseurl }}``.  The ``--auto`` option ensures the server restarts when a 
change is made.

The generated site is available at http://localhost:4000/

Follow the instructions for setting up Jekyll.  You can view the site locally
by running the Jekyll server::

    jekyll --server

and visiting http://localhost:4000/
