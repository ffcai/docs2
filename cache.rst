Cache
*****

Cache Control
=============

#. Cache ::

    proxy.config.http.cache.http

   Set to ``0``: Test if ATS disables caching HTTP requests.
	
   Set to ``1``: Test if ATS enables caching HTTP requests.

Caching HTTP Objects
====================

#. Client Directives

   By default, ATS does not cache objects with the following request headers:

   * ``Authorization``
   * ``Cache-Control: no-store``
   * ``Cache-Control: no-cache``
   * ``Cookie`` (for text objects)
   
   We need to test the following scenarios:

   * Test if ATS does not cache objects with the above request headers.
   * Test if ATS can ignore client no-cache headers.
   * Test if ATS caches cookied content.

#. Origin Server Directives

By default, Traffic Server does not cache objects with the following response headers:

* ``Cache-Control: no-store``
* ``Cache-Control: private``
* ``WWW-Authenticate``
* ``Set-Cookie``
* ``Cache-Control: no-cache``
* ``Expires``

We need to test the following scenarios:

* Test if ATS does not cache objects with the above response headers.
* Test if ATS can ignore ``WWW-Authenticate`` headers.
* Test if ATS can ignore server ``no-cache`` headers.

Heuristic Expiration
====================

::

	proxy.config.http.cache.heuristic_min_lifetime
	proxy.config.http.cache.heuristic_max_lifetime
	proxy.config.http.cache.heuristic_lm_factor

Test if the heuristic minimum lifetime, maximum lifetime and aging factor take effect.

::

	proxy.config.http.cache.fuzz.time
	proxy.config.http.cache.fuzz.probability
	proxy.config.http.cache.fuzz.min_time

Test if the fuzz time, probability and minimum time take effect.

Dynamic Content & Content Negotiation
=====================================

::

	proxy.config.http.cache.vary_default_text

Test if Traffic Server varies on the specified header for text documents.

::

	proxy.config.http.cache.vary_default_images

Test if Traffic Server varies on the specified header for images.

::

	proxy.config.http.cache.vary_default_other

Test if Traffic Server varies on the specified header for anything other than text and images.

Negative Response Caching
=========================

::

	proxy.config.http.negative_caching_enabled

Set to ``0``: Test if Traffic Server does not cache negative responses when a requested page does not exist.

Set to ``1``: Test if Traffic Server caches negative responses when a requested page does not exist.

::

	proxy.config.http.negative_caching_lifetime

Set to ``N``: Test if Traffic Server keeps the negative responses valid in cache for ``N`` seconds.

Negative Revalidate
===================


PUSH
====

::

	proxy.config.http.push_method_enabled

Set to ``1``: Test if ATS allows to deliver content directly to the cache without a user request via ``PUSH`` method.
