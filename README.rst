==========
Changelog
==========

A `Sphinx <http://sphinx.pocoo.org/>`_ extension to generate changelog files.

This is an experimental, possibly-not-useful extension that's used by the
`SQLAlchemy <http://www.sqlalchemy.org>`_ project and related projects.

Configuration
=============

A sample configuration in ``conf.py`` looks like this::

    extensions = [
                # changelog extension
                'changelog',

                # your other sphinx extensions
                # ...
            ]


    # section names - optional
    changelog_sections = ["general", "rendering", "tests"]

    # tags to sort on inside of sections - also optional
    changelog_inner_tag_sort = ["feature", "bug"]

    # how to render changelog links - these are plain
    # python string templates, ticket/pullreq/changeset number goes
    # in "%s"
    changelog_render_ticket = "http://bitbucket.org/myusername/myproject/issue/%s"
    changelog_render_pullreq = "http://bitbucket.org/myusername/myproject/pullrequest/%s"
    changelog_render_changeset = "http://bitbucket.org/myusername/myproject/changeset/%s"

Usage
=====

Changelog introduces the ``changelog`` and ``change`` directives::

    ====================
    Changelog for 1.5.6
    ====================

    .. changelog::
        :version: 1.5.6
        :released: Sun Oct 12 2008

        .. change::
            :tags: general
            :tickets: 27

          Improved the frobnozzle.

        .. change::
            :tags: rendering, tests
            :pullreq: 8
            :changeset: a9d7cc0b56c2

          Rendering tests now correctly render.


With the above markup, the changes above will be rendered into document sections
per changelog, then each change within organized into paragraphs, including
special markup for tags, tickets mentioned, pull requests, changesets.   The entries will
be grouped and sorted by tag according to the configuration of the ``changelog_sections``
and ``changelog_inner_tag_sort`` configurations.

A "compound tag" can also be used, if the configuration has a section like this::

    changelog_sections = ["orm declarative", "orm"]

Then change entries which contain both the ``orm`` and ``declarative`` tags will be
grouped under a section called ``orm declarative``, followed by the ``orm`` section where
change entries that only have ``orm`` will be placed.

Other Markup
============

The ``:ticket:`` directive will make use of the ``changelog_render_ticket`` markup
to render a ticket link::

    :ticket:`456`



