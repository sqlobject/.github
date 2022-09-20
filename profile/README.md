# SQLObject

## For users

SQLObject is an object-relational mapper, i.e., a library that will wrap
your database tables in Python classes, and your rows in Python
instances.

It currently supports MySQL, PostgreSQL and SQLite; connections to other
backends - Firebird, Sybase, MSSQL and MaxDB (also known as SAPDB) - are
lesser debugged).

Python 2.7 or 3.4+ is required.

To install it from [PyPI](https://pypi.org/project/SQLObject/) use the command

    pip install sqlobject

This is a small example:

Create a simple class that wraps a table:

    >>> from sqlobject import *
    >>>
    >>> sqlhub.processConnection = connectionForURI('sqlite:/:memory:')
    >>>
    >>> class Person(SQLObject):
    ...     fname = StringCol()
    ...     mi = StringCol(length=1, default=None)
    ...     lname = StringCol()
    ...
    >>> Person.createTable()

Use the object:

    >>> p = Person(fname="John", lname="Doe")
    >>> p
    <Person 1 fname='John' mi=None lname='Doe'>
    >>> p.fname
    'John'
    >>> p.mi = 'Q'
    >>> p2 = Person.get(1)
    >>> p2
    <Person 1 fname='John' mi='Q' lname='Doe'>
    >>> p is p2
    True

Queries:

    >>> p3 = Person.selectBy(lname="Doe")[0]
    >>> p3
    <Person 1 fname='John' mi='Q' lname='Doe'>
    >>> pc = Person.select(Person.q.lname=="Doe").count()
    >>> pc
    1

For more information please see the documentation in
[SQLObject.rst](../../../sqlobject/blob/master/docs/SQLObject.rst),
or online at http://sqlobject.org/.

Discussions should be conducted at SQLObject-discuss mailing list.
See instructions and archives at https://sourceforge.net/p/sqlobject/mailman/.

StackOverflow: https://stackoverflow.com/questions/tagged/sqlobject

## For developers and contributors

To help SQLObject please send
[pull requests](https://github.com/sqlobject/sqlobject/pulls).

[Developer Guide](http://sqlobject.org/DeveloperGuide.html) is available.
