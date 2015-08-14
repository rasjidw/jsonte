=============================
Jsonte (Json Type Extensions)
=============================

* Free software: Simplified BSD license

Documentation
-------------

Jsonte is just a simple and well defined way of 'extending' json to support some additional types.

The primary goal is to add support for data types that are commonly used in databases.  In particular:

* dates, times, and timestamps (both with and without timezones)
* arbitrary precision numeric entries
* binary data

A secondary goal was to do this in such a way that the resulting json was easily human readable, and
also programming language agnostic.

The format is simple, and is always itself valid json.

::

   * A date:      { "#date": "2015-05-28" }
   * A time:      { "#time": "22:12:42.381000" }
   * A timestamp: { "#tstamp": "2015-05-28T22:13:42.381000" }

These are just the ISO formats for each of the above items.

::

   * A numeric entry:  { "#num": "1234.0000" }
   * Some binary data: { "#bin": "SGVsbG8gV29ybGQhAA==" }

The numeric entry is encoded as a string so the degree of precision is not lost.
The binary data is just base64 encoded.

Key Escaping
~~~~~~~~~~~~

Keys in objects that start with either a hash (#) or a tidle (~) are escaped by a tidle (~) being prefixed to the key.
This is to avoid any accidental collisions with the 'special' object keys used, ensuring unambiguous reversibility.

So an object that would normaly be encoded as ``{"#bin": 1234}`` would become ``{"~#bin": 1234}`` when encoded by jsonte,
and ``{"~foo": "bar"}`` would become ``{"~~foo": "bar"}``


Implementations
---------------

Python: `python-jsonte <https://github.com/rasjidw/python-jsonte>`_

Others: to come...
