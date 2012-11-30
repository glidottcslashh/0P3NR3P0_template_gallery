# 0P3NR3P0 
## API Documentation + Sample Web Gallery 
* * * * 

The GLI.TC/H 0P3NR3P0 is an open/public repository of glitch art worx. Anyone can submit their worx to the 0P3NR3P0 and curate/program/source work from the 0P3NR3P0 for inclusion in their own glitch art events.

The 0P3NR3P0 itself is an online database developped by [yyolk](https://github.com/yyolk) and the gli.tc/h/bots. Artists can submit their worx four auto-inclusion into the database at [0p3nr3p0.net/](http://0p3nr3p0.net/). This page is documentation for how one might build a web gallery featuring the worx in the 0P3NR3P0 as well as a template gallery you can use to get your web gallery started.

* * * * 

All you need to know inorder to build your own 0P3NR3P0 web gallery is HTML, CSS (and a little bit of javascript), the following is a walkthrough for setting up your javascript to call and parse the data from 0P3NR3P0.


### // the data

each piece in the 0P3NR3P0 contains the following data:
* the piece itself (represented by a url, this might be a web art piece, video, sound, images etc), the title of the piece 
* the title of the piece (as a string)
* the authors name (as a string)
* the authors homepage (as a url)
* a description of the piece (as a string)
* tags the author associated with their piece (this is an array)

here's an example for how you might setup some global variables to store this data in:

### // ajax request

0P3NR3P0 is a [couchDB](http://couchdb.apache.org/) database, which uses json documents, so we recommend using [jQuery](http://jquery.com/) when building your web galleries. We'll use jQuery's [.ajax() method](http://api.jquery.com/jQuery.ajax/) to send requests to the following url: 

    https://glitch.iriscouch.com/openrepo/_design/0P3NR3P0/_view/recent-items

here's a basic ajax setup calling the 0P3NR3P0. Make sure to use [jsonp](http://en.wikipedia.org/wiki/JSONP) as you'll be requesting data from a server in a different domain

        $.ajax({
            url: 'https://glitch.iriscouch.com/openrepo/_design/0P3NR3P0/_view/recent-items',
            type: 'get',
            dataType: 'jsonp',
            success: function(data) {            
                // loop through the data here
            }
        });

### // loop through the data

in this template we use jQuery's [.each() method](http://api.jquery.com/each/) to iterate through the data, here's an example:

              $.each(data, function() {
                    $.each(this, function(key, val){
                         $.each(this, function(k, v){
                            if(v.title != undefined) { // only grab pieces
                                v.url;                 // is the piece url 
                                v.title;               // is the title
                                v.description;         // is the description
                                v.author;              // is the author
                                v.homepage_url;        // is the author's homepage
                            }
                         });
                    });                    
                });


here's a [sample web gallery](http://gli.tc/h/0P3NR3P0_sample_gallery/) we made along these lines