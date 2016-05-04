.. _installation:

Installation
============
The easiest method is to install directly from pypi using `pip`_ by
running the command below, which will also install the required
dependencies mentioned above::

    $ pip install mezzanine-auth-pages

If you prefer, you can download mezzanine-auth-pages and install it directly from
source::

    $ python setup.py install

Add ``mezzanine_page_auth`` to your ``INSTALLED_APPS`` setting before all
mezzanine apps::

    INSTALLED_APPS = (
        # ...
        'mezzanine_page_auth',
        'mezzanine.boot',
        'mezzanine.conf',
        'mezzanine.core',
        # ...
    )

You will then want to create the necessary tables. If you are using `South`_
for schema migrations, you'll want to::

    $ python manage.py migrate mezzanine_page_auth


Middleware
~~~~~~~~~~
Enable ``PageAuthMiddleware`` middleware in your settings module as follows::

    MIDDLEWARE_CLASSES = (
        # ...
        "mezzanine.core.middleware..."
        "mezzanine.pages.middleware..."
        "mezzanine_page_auth.middleware.PageAuthMiddleware",
        # ...
    )

The order of ``MIDDLEWARE_CLASSES`` is important. You should include the
``PageAuthMiddleware`` middleware after other Mezzanine middlewares in the list.

.. _template-context-processors:

Template Context Processors
~~~~~~~~~~~~~~~~~~~~~~~~~~~
Enable ``page_auth`` template context processors in your settings module as follows::

    TEMPLATE_CONTEXT_PROCESSORS = (
        # ...
        'mezzanine_page_auth.context_processors.page_auth',
    )

The order of ``MIDDLEWARE_CLASSES`` is important. You should include the
``PageAuthMiddleware`` middleware after other Mezzanine middlewares in the list.

Mezzanine Settings
~~~~~~~~~~~~~~~~~~
Configure ``EXTRA_MODEL_FIELDS`` Mezzanine setting in your settings module as
follows::

    EXTRA_MODEL_FIELDS = (
        # ...
        (
            "mezzanine.pages.models.Page.groups",
            "ManyToManyField",
            ("auth.Group",),
            {"blank": True, "verbose_name": 'groups',
             'symmetrical': False, 'through': "mezzanine_page_auth.PageAuthGroup"},
        ),
        # ...
    )

for inject field ``groups`` into Mezzanine’s models (reference to `Field Injection`_ Mezzanine documantation).

.. GENERAL LINKS

.. _`Django`: http://djangoproject.com/
.. _`Django Code of Conduct`: https://www.djangoproject.com/conduct/
.. _`BSD licensed`: http://www.linfo.org/bsdlicense.html
.. _`Wordpress`: http://wordpress.org/
.. _`great sites people have built using Mezzanine`: http://mezzanine.jupo.org/sites/
.. _`Pinax`: http://pinaxproject.com/
.. _`Mingus`: http://github.com/montylounge/django-mingus
.. _`Mezzanine`: http://mezzanine.jupo.org
.. _`Mezzanine project page`: http://mezzanine.jupo.org
.. _`Field Injection`: http://mezzanine.jupo.org/docs/model-customization.html#field-injection
.. _`Python`: http://python.org/
.. _`pip`: http://www.pip-installer.org/
.. _`bleach`: http://pypi.python.org/pypi/bleach
.. _`pytz`: http://pypi.python.org/pypi/pytz/
.. _`django-compressor`: https://pypi.python.org/pypi/django_compressor
.. _`Python Imaging Library`: http://www.pythonware.com/products/pil/
.. _`grappelli-safe`: http://github.com/stephenmcd/grappelli-safe
.. _`filebrowser-safe`: http://github.com/stephenmcd/filebrowser-safe/
.. _`Grappelli`: http://code.google.com/p/django-grappelli/
.. _`FileBrowser`: http://code.google.com/p/django-filebrowser/
.. _`South`: http://south.aeracode.org/
.. _`requests`: http://docs.python-requests.org/en/latest/
.. _`requests-oauth`: https://github.com/maraujop/requests-oauth
.. _`pyflakes`: http://pypi.python.org/pypi/pyflakes
.. _`pep8`: http://pypi.python.org/pypi/pep8
.. _`In-line page editing`: http://mezzanine.jupo.org/docs/inline-editing.html
.. _`custom content types`: http://mezzanine.jupo.org/docs/content-architecture.html#creating-custom-content-types
.. _`Search engine and API`: http://mezzanine.jupo.org/docs/search-engine.html
.. _`dashboard`: http://mezzanine.jupo.org/docs/admin-customization.html#dashboard
.. _`Themes Marketplace`: http://mezzathe.me/
.. _`Cartridge`: http://cartridge.jupo.org/
.. _`Custom templates`: http://mezzanine.jupo.org/docs/content-architecture.html#page-templates
.. _`test suite`: http://mezzanine.jupo.org/docs/packages.html#module-mezzanine.core.tests
.. _`JVM`: http://en.wikipedia.org/wiki/Java_virtual_machine
.. _`Jython`: http://www.jython.org/
.. _`Twitter Bootstrap`: http://twitter.github.com/bootstrap/
.. _`Disqus`: http://disqus.com/
.. _`Gravatar`: http://gravatar.com/
.. _`Google Analytics`: http://www.google.com/analytics/
.. _`Twitter`: http://twitter.com/
.. _`bit.ly`: http://bit.ly/
.. _`Akismet`: http://akismet.com/
.. _`project_template`: https://github.com/stephenmcd/mezzanine/tree/master/mezzanine/project_template
.. _`GitHub`: http://github.com/stephenmcd/mezzanine/
.. _`Bitbucket`: http://bitbucket.org/stephenmcd/mezzanine/
.. _`mezzanine-users`: http://groups.google.com/group/mezzanine-users/topics
.. _`security@jupo.org`: mailto:security@jupo.org?subject=Mezzanine+Security+Issue
.. _`GitHub issue tracker`: http://github.com/stephenmcd/mezzanine/issues
.. _`#mezzanine IRC channel`: irc://irc.freenode.net/mezzanine
.. _`Freenode`: http://freenode.net
.. _`Django coding style`: http://docs.djangoproject.com/en/dev/internals/contributing/#coding-style
.. _`PEP 8`: http://www.python.org/dev/peps/pep-0008/
.. _`Transiflex`: https://www.transifex.net/projects/p/mezzanine/
.. _`Mezzanine Grid on djangopackages.com`: http://www.djangopackages.com/grids/g/mezzanine/
.. _`Django's internationalization`: https://docs.djangoproject.com/en/dev/topics/i18n/translation/
.. _`Python Software Foundation`: http://www.python.org/psf/
.. _`Urban Airship`: http://urbanairship.com/
.. _`Django Packages`: http://djangopackages.com/
.. _`Hewlett Packard`: http://www.hp.com/
.. _`Tabblo`: http://www.tabblo.com/
.. _`The Linux Journal`: http://www.linuxjournal.com
.. _`Work For Pie`: http://workforpie.com/
.. _`virtualenvwrapper`: http://www.doughellmann.com/projects/virtualenvwrapper
