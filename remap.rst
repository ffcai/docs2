Remap
*****

Map Type
========

#. map

   Translates an incoming request URL to the appropriate origin server URL.

   Test if ``map`` rule works.

   Done: `test_remap <https://github.com/apache/trafficserver/blob/master/ci/new_tsqa/tests/test_remap.py>`_
		
#. map_with_recv_port

   Exactly like ``map`` except that ``map_with_recv_port`` uses the port at which the request was received to perform the mapping instead of the port present in the request.
	
   Test if ``map_with_recv_port`` rule works.

#. map_with_referer

   Extended version of ``map``, which can be used to activate “deep linking protection”, where target URLs are only accessible when the Referer header is set to a URL that is allowed to link to the target.

   Test if ``map_with_referer`` rule works.
	
#. reverse_map

   Translates the URL in origin server redirect responses to point to Traffic Server.

   Test if ``reverse_map`` rule works.
	
#. redirect
	
   Redirects HTTP requests permanently without having to contact the origin server. Permanent redirects notify the browser of the URL change (by returning an HTTP status code 301) so that the browser can update bookmarks.

   Test if ``redirect`` rule works.

#. redirect_temporary
	
   Redirects HTTP requests temporarily without having to contact the origin server. Temporary redirects notify the browser of the URL change for the current request only (by returning an HTTP status code 307).

   Test if ``redirect_temporary`` rule works.

Precedence
==========

Remap rules are not processed top-down, but based on an internal priority. Once these rules are executed we pick the first match based on configuration file parse order.

#. ``map_with_recv_port`` and ``regex_map_with_recv_port``
#. ``map and regex_map`` and ``reverse_map``
#. ``redirect`` and ``redirect_temporary``
#. ``regex_redirect`` and ``regex_redirect_temporary``

Test if it follows the above priority.

Test if it follows the parse order within same priority.

Match-All
=========

A map rule with a single ``/`` acts as a wildcard, it will match any request. This should be use with care, and certainly only once at the end of the remap.config file. E.g. ::
	
    map / http://all.example.com

Test if ``Match-All`` rule works.

Regex Map Type
==============

#. regex_map

   The ``regex`` qualifier can also be used for ``map``. When present, ``map`` mappings are checked first. If there is a match, then it is chosen without evaluating the “regular expression” mapping rules.
	
   Test if `regex_map` rule works.
	
#. map_with_recv_port
	
   The ``regex`` qualifier can also be used for ``map_with_recv_port``. When present, ``map_with_recv_port`` mappings are checked first. If there is a match, then it is chosen without evaluating the “regular expression” mapping rules.
	
   Test if ``regex_map_with_recv_port`` rule works.
	
#. redirect
	
   The ``regex`` qualifier can also be used for ``redirect``. When present, ``redirect`` mappings are checked first. If there is a match, then it is chosen without evaluating the “regular expression” mapping rules.
	
   Test if `regex_redirect` rule works.

#. redirect_temporary
	
   The ``regex`` qualifier can also be used for ``redirect_temporary``. When present, ``redirect_temporary`` mappings are checked first. If there is a match, then it is chosen without evaluating the “regular expression” mapping rules.
	
   Test if ``regex_redirect_temporary`` rule works.

Plugin Chaining
===============

Test if plugins can be configured to be evaluated in a specific order, passing the results from one in to the next.

ACL Filters
===========

Test if ACL filters work.

Named Filters
=============

Test if named filters work.

Including Additional Remap Files
================================

Test if ``.include`` directive works.
