FacetView_ is a pure javascript frontend for ElasticSearch or SOLR search
indices.

It's been developed as a jQuery plugin and lets you easily embed a faceted
browse front end into any web page.

.. _FacetView: http://okfnlabs.org/facetview/

Development is now taking place in this repo: http://github.com/okfn/facetview


Demo
====

See http://okfnlabs.org/facetview/ or just take a look at index.html (if you
have the source).


Status
======

FacetView is pretty new, and still under active development but is already
pretty stable. If you have suggestions or want to make a contribution please
check out the github repo.


Using FacetView
===============

Add the following code to your web page::

  <script src="JQUERY-SOURCE"></script>
  <script type="text/javascript" src="YOUR-FACETVIEW-SOURCE"></script>
  
  <script type="text/javascript">
  jQuery(document).ready(function() {
      jQuery('jquery-selector').facetview();
  });
  </script>

* JQUERY-SOURCE – change this to wherever you get your jQuery from. For
  example, https://ajax.googleapis.com/ajax/libs/jquery/1.6.2/jquery.js. If you
  already have jQuery on your page / site, then you can miss out that first
  script tag entirely.
* YOUR-FACETVIEW-SOURCE – change this to whatever online you put your copy of
  facetview at. For example, http://bibsoup.net/static/jquery.facetview.js
* YOUR-PAGE-PART – change this to identify whatever part of the page you want
  to append the FacetView into. For example, ‘body’ would do, or you could have
  a <div> on your page like this::

    <div id="your-page-part></div>

.. note::
  
    You may also want to include css. The out of the box html and css is
    Bootstrap plus css/facetview.css. However, you are welcome to customize
    this or add your own.

Now that you have everything ready, you will probably want to customize to
get it looking the way you want it.


Customization
=============

Once you have FacetView all ready to go, you should probably do some
customisation. There are a few ways to do this:

Edit the config in jquery.facetview.js
--------------------------------------

Specify the defaults::

    var defaults = {
        "config_file":false,
        "default_filters":["journal","author","year"],
        "result_display_headers":["title","journal","author"],
        "ignore_fields":["_id","_rev"],
        "show_advanced":false,
        "search_url":"",
        "search_index":"elasticsearch",
        "default_url_params":{},
        "freetext_submit_delay":"700",
        "query_parameter":"q",
        "q":"*:*",
        "predefined_query_values":{},
        "default_paging":{}
    };

* config_file – the location of an external config file (explained below)
* default_filters – the filters you want to see down the right hand side, for
  filtering your results by.
* filter_query_key –
* result_display_headers – which fields to display in the result list (other
  fields are shown when you click on the result)
* ignore_fields – any fields not to show at all
* show_advanced – for now, just shows or hides the advanced panel, which at the
  moment only gives the options to add more filters
* search_url – the endpoint for submitting search queries to
* search_index – your index type, solr or elasticsearch
* default_url_params – parameters to pass through with every query; should
  include “wt”:”json” for SOLR queries to return JSON, and probably
  “facet.mincount”:1 for SOLR queries to ignore zero counts on facet values
* freetext_submit_delay – the delay in milliseconds before the free text search
  field triggers a result update
* query_parameter – the name of the search query parameter that should be
  passed to your index. usually this is “q”
* q – the default blank search query parameter, such as “:“
* predefined_query_values – any values you want embedded into the query every
  time a query is submitted, to restrict the result set
* default_paging – default result size, and default starting result

Pass in config settings when calling FacetView
----------------------------------------------

All of the above settings can also be defined when calling FacetView, and will
overwrite the values set in the file itself. So you can do something like
this::

  <script type="text/javascript">
  jQuery(document).ready(function() {
      jQuery('YOUR-PAGE-PART').facetview({
          "search_index":"solr",
          "query_parameter":"q"
      });
  });
  </script>

Provide the location of an external config file
-----------------------------------------------

(in development)

A JSON file can be made available anywhere on the web with any of the above
listed settings in it. Then, just pass the URL of your config file when you
call FacetView, and it will read that config file for you.

Change the layout by making and using a custom CSS file
-------------------------------------------------------

When FacetView runs, it calls a default CSS file. Take a look at the
jquery.facetview.js file – at the top, it defines a CSS file location, then
calls it into your page. You can copy that CSS file, make your own version,
then call your version instead. This will allow you to style it however you
want.


Copyright and License
=====================

Copyright 2011 Open Knowledge Foundation and Cottage Labs.

Licensed under the `MIT License`_

.. _MIT License: http://www.opensource.org/licenses/mit-license.php

