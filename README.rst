==================
python-poppler-qt5
==================

A Python binding for libpoppler-qt5 that aims for completeness and for being
actively maintained.

Created and currently maintained by Wilbert Berendsen <wbsoft@xs4all.nl>.

Homepage: https://pypi.python.org/pypi/python-poppler-qt5/


Usage::

    import popplerqt5
    d = popplerqt5.Poppler.Document.load('file.pdf')


Documentation
-------------

The Python API closely follows the Poppler Qt5 C++ interface library API,
documented at http://people.freedesktop.org/~aacid/docs/qt5/ .

Note: Releases of PyQt5 < 5.4 currently do not support the QtXml module,
all methods that use the QDomDocument, QDomElement and QDomNode types are
disabled. This concerns the ``Document::toc()`` method and some constructors
and the ``store()`` methods in the ``Annotation`` subclasses. So, using
PyQt5 >= 5.4 is recommended.

Whereever the C++ API requires ``QList``, ``QSet`` or ``QLinkedList``, any
Python sequence can be used. 
API calls that return ``QList``, ``QSet`` or ``QLinkedList`` all return Python
lists.

There are a few other differences:

``Poppler::Document::getPdfVersion(int *major, int *minor)`` can simply be
called as ``d.getPdfVersion()``, (where ``d`` is a ``Poppler::Document``
instance); it will return a tuple of two integers (major, minor).

``Poppler::Document`` has ``__len__`` and ``__getitem__`` methods, corresponding
to ``numPages()`` and ``page(int num)``.

``Poppler::FontIterator`` (returned by ``Poppler::Document::newFontIterator``)
is also a Python iterable (e.g. has ``__iter__()`` and ``__next__()`` methods).
So although you can use::

    it = document.newFontIterator()
    while it.hasNext():
        fonts = it.next()  # list of FontInfo objects
        ...

you can also use the more Pythonic::

    for fonts in document.newFontIterator():
        ...

In addition to the Poppler namespace, there are two toplevel module
functions:

    ``popplerqt5.version()``
        returns the version of the ``python-poppler-qt5`` package as a
        tuple of ints, e.g. ``(0, 18, 2)``.
    
    ``popplerqt5.poppler_version()``
        returns the version of the linked Poppler-Qt5 library as a
        tuple of ints, e.g. ``(0, 24, 5)``.
        
        This is determined at build time. If at build time the Poppler-Qt5
        version could not be determined and was not specified, an empty
        tuple might be returned.

