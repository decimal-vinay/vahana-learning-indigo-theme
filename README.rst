Indigo, a cool blue theme for Open edX
======================================

Indigo is an elegant, customizable theme for `Open edX <https://open.edx.org>`__.

.. image:: ./screenshots/01-landing-page.png
    :alt: Platform landing page

**Note**: This version of the Indigo theme is compatible with the Palm release of Open edX.

You can view the theme in action at https://demo.openedx.overhang.io.

Installation
------------

Indigo was specially developed to be used with `Tutor <https://docs.tutor.overhang.io>`__ (at least v14.0.0). If you have not installed Open edX with Tutor, then installation instructions will vary.

Since Tutor v13.2.0, Indigo can be installed as a Tutor plugin::

    tutor plugins install vahana
    tutor plugins enable vahana
    tutor config save

Rebuild the Openedx docker image::

    tutor images build openedx

Restart your platform::

    tutor local start -d

You will then have to enable the "vahana" theme, as per the `Tutor documentation <https://docs.tutor.overhang.io/local.html#setting-a-new-theme>`__::

    tutor local do settheme vahana

Configuration
-------------

- ``INDIGO_WELCOME_MESSAGE`` (default: "The place for all your online learning")
- ``INDIGO_PRIMARY_COLOR`` (default: "#3b85ff")
- ``INDIGO_FOOTER_NAV_LINKS`` (default: ``[{"title": "About", "url": "/about"}, {"title": "Contact", "url": "/contact"}]``)
- ``INDIGO_FOOTER_LEGAL_LINKS`` (default: ``[{"title": "Terms of service", "url": "/tos"}, {"title": "Indigo theme for Open edX", "url": "https://github.com/decimal-vinay/vahana-learning-indigo-theme"}]``)

The ``INDIGO_*`` settings listed above may be modified by running ``tutor config save --set INDIGO_...=...``. For instance, to remove all links from the footer, run::

    tutor config save --set "INDIGO_FOOTER_NAV_LINKS=[]" --set "INDIGO_FOOTER_LEGAL_LINKS=[]"

Or, to set the primary color to forest green, run::

    # Note: The nested quotes are needed in order to handle the hash (#) correctly.
    tutor config save --set 'INDIGO_PRIMARY_COLOR="#225522"'

Customization
-------------

This plugin can serve as a starting point to create your own themes. Just fork this repository and modify the files as you see fit.

Changing the default logo and other images
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The theme images are stored in `vahanalearning/templates/vahanalearning/lms/static/images <https://github.com/decimal-vinay/vahana-learning-indigo-theme/tree/master/vahanalearning/templates/vahanalearning/lms/static/images>`__ for the LMS, and in `vahanalearning/templates/vahanalearning/cms/static/images <https://github.com/decimal-vinay/vahana-learning-indigo-theme/tree/master/vahanalearning/templates/vahanalearning/cms/static/images>`__ for the CMS. To use custom images in your theme, just replace the files stored in these folders with your own.

Overriding the default "about", "contact", etc. static pages
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

By default, the ``/about`` and ``/contact`` pages contain a simple line of text: "This page left intentionally blank. Feel free to add your own content". This is of course unusable in production. In the following, we detail how to override just any of the static templates used in Open edX.

The static templates used by Open edX to render those pages are all stored in the `edx-platform/lms/templates/static_templates <https://github.com/edx/edx-platform/tree/open-release/palm.master/lms/templates/static_templates>`__ folder. To override those templates, you should add your own in the following folder::

    ls vahanalearning/templates/vahanalearning/lms/templates/static_templates"

For instance, edit the "donate.html" file in this directory. We can derive the content of this file from the contents of the `donate.html <https://github.com/edx/edx-platform/blob/open-release/palm.master/lms/templates/static_templates/donate.html>`__ static template in edx-platform::

    <%page expression_filter="h"/>
    <%! from django.utils.translation import ugettext as _ %>
    <%inherit file="../main.html" />

    <%block name="pagetitle">${_("Donate")}</%block>

    <main id="main" aria-label="Content" tabindex="-1">
        <section class="container about">
            <h1>
                <%block name="pageheader">${page_header or _("Donate")}</%block>
            </h1>
            <p>
                <%block name="pagecontent">Add a compelling message here, asking for donations.</%block>
            </p>
        </section>
    </main>

This new template will then be used to render the /donate url.

Troubleshooting
---------------

This Tutor plugin is maintained by Régis Behmo from `Overhang.IO <https://overhang.io>`__. Community support is available from the official `Open edX forum <https://discuss.openedx.org>`__. Do you need help with this plugin? See the `troubleshooting <https://docs.tutor.overhang.io/troubleshooting.html>`__ section from the Tutor documentation.


License
-------

This work is licensed under the terms of the `GNU Affero General Public License (AGPL) <https://github.com/decimal-vinay/vahana-learning-indigo-theme/blob/master/LICENSE.txt>`_.
