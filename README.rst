Certifi: Python SSL Certificates
================================

`Certifi`_ provides Mozilla's carefully curated collection of Root Certificates for
validating the trustworthiness of SSL certificates while verifying the identity
of TLS hosts. It has been extracted from the `Requests`_ project.

Fork
------
This is a temporary workaround for versions of openssl < 1.1.1
by dropping expired letsencrypt certificate until mozilla updates their certificate budle.

Installation
------------

``certifi`` is available on PyPI. Simply install it with ``pip``::

    $ pip install git+https://github.com/jtracks/python-certifi.git

Usage
-----

To reference the installed certificate authority (CA) bundle, you can use the
built-in function::

    >>> import certifi

    >>> certifi.where()
    '/usr/local/lib/python3.7/site-packages/certifi/cacert.pem'

Or from the command line::

    $ python -m certifi
    /usr/local/lib/python3.7/site-packages/certifi/cacert.pem

Enjoy!

1024-bit Root Certificates
~~~~~~~~~~~~~~~~~~~~~~~~~~

Browsers and certificate authorities have concluded that 1024-bit keys are
unacceptably weak for certificates, particularly root certificates. For this
reason, Mozilla has removed any weak (i.e. 1024-bit key) certificate from its
bundle, replacing it with an equivalent strong (i.e. 2048-bit or greater key)
certificate from the same CA. Because Mozilla removed these certificates from
its bundle, ``certifi`` removed them as well.

In previous versions, ``certifi`` provided the ``certifi.old_where()`` function
to intentionally re-add the 1024-bit roots back into your bundle. This was not
recommended in production and therefore was removed at the end of 2018.

.. _`Certifi`: https://certifiio.readthedocs.io/en/latest/
.. _`Requests`: https://requests.readthedocs.io/en/master/

Addition/Removal of Certificates
--------------------------------

Certifi does not support any addition/removal or other modification of the
CA trust store content. This project is intended to provide a reliable and
highly portable root of trust to python deployments. Look to upstream projects
for methods to use alternate trust.
