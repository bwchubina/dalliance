Performance
-----------

 - Performance must stay at least as good as r310
     + Good way of measuring this?
 - Browser support:
     + Mozilla (FF3.5, Camino???)
     + Safari (3.1 or later)
     + Chrome.
     + Not IE<9. 
     + IE9 is looking doable:
          * UI draws correctly (IE9dp2).
          * DAS-fetching can be made to work (requires dedicated code path using XDomainRequest)
	  * Currently no features displaying
	  * Probably transform and/or clipping problems.
 
Real Soon Now
-------------

 - Improvements to the config system
     + Reset without reloading page.
     + Config. updates in the static HTML should override localstorage.
       - Store a hash of the static config?
       - How does this work if multiple pages share a cookieKey?
     + Multiple sessions + switching.
 - Cache server capabilities in the DAS layer (i.e. maxbins!)
     + Most code is in, currently doesn't work because of missing Access-Control-Expose-Headers support.
     + https://bugs.webkit.org/show_bug.cgi?id=41210
     + May be able to do something with DAS/1.6 sources since these *should* list caps in the sources document???
 - Better configuration of quantitative tracks.
     + Global y-zoom? [Matias wants this.  Wouldn't per-trackgroup be better?  Needs an explicit idea of track-groups.]
     + Switch between bars/colourways? [Leave this for now]
     + Increase/decrease viewed height of quant tracks?
 - Separate concepts of Known Space and Drawn Space.
 - Page embedding
     + Allow multiple browser instances in a given page (i.e. remove all static state).
     + Also allow instances which *do* share some state? (e.g. coarse and fine views on the same data)?
       How much state to share? 
 - Publication-quality SVG export.
 - Generalize the placard code?
 - Think about cancelling long-running XHRs if they're no longer needed?
 - DAS on geneID coords.
 - Auto-detection of credentialed servers?
 - Undo
 - Tabmargin cleanup
    + Wider by default?
    + Auto-adjust size?
    + Think about control placement
    + Rename tiers?

Nice to have
------------

 - More stylesheet stuff
   + Support ZINDEX?
   + Rainbowed LINEPLOT glyphs?
   + More thought about how how to combine LINEPLOT with other glyphs in the same tier.
 - Add a track removal button to error placards?
 - Ability to re-bump w/o re-fetching all the data
     + Should allow more aggressive spec-fetching?
     + Allow fetches that add to the working set, rather than replacing it.
     + Try to respect existing feature placements when scrolling.
 - Expand/collapse per-feature-group (expand transcripts for individual genes?  don't think anyone else is doing this, but I'd use it!)
 - Gene search:
     + Basic implementation works with E!  Needs more testing.
     + Would be nice if it offered proper keyword search, rather than pure feature-but-ID
     + Any reason not to just hack the server to do this?
     + Suggest-as-you-type?
 - Support for a more compact encoding for quantitative tracks.
     + Will need some server suppport.  
     + Adding a new encoding to Dazzle shouldn't be too painful.
     + DAS/1.6: has been some discussion of CONNEG but nothing finalized.
 - User-uploaded data
     + Round-tripped in via Dastard?
     + Also interesting to do LOCAL data additions?
 - State persistance between sessions
     + Add a "make URL" button?
  - Tier groups
     + Should yZoom together.
     + Other quantitative stuff?  If we support colourway switching then probably.
     + Do they have any meaning for non-quant tracks?
     + Drag together when re-ordering????
     + How are these defined?  DASSTYLE is hopeless.  Extended <sources> document?
  - Dedicated configuration/persistance language?
  - Distance between a pair of features.
  - Jiggle labels so they're always visible
     + For genes, try to keep them attached to exons.

Blue sky
--------
    
 - Tourist mode
    + Fast movement between POIs. 
 - Real-time collaborative features
    + i.e. multiple users viewing a browser with shared state.
    + Annotation (Using DAS writeback protocols?)
    + View synchronization?
    + Chat 
    + Websockets work nicely for this.  Prototype at DAS Workshop '10.
 - Navigate by blatting user sequences to the genome
    + How to do this in a DASish world?
    + Relationship with tourist mode?
 - Flip into vertical orientation (AceDB-like!)
    + How much of the rendering code would end up ori-dependent?
 - MultiContigView equivalent?
 - Coord-system mapping?


The Server Side
---------------
 
 - Tidy up the Allow-Credentials support in Dazzle.
 - Are we better off using JKDBs to serve sequence?
    + A JKDB-based sequence server could also usefully compute GC composition, etc., etc., on the fly. [done now]
 - bigFile-backed servers?
 - BAM-backed servers. 
    + Done using Picard.  Potential scalability issues in the future but working for now.
 - Dazzle replacement (i.e. fast, scalable, DAS middleware).
    + Any ideas from Cadastral worth following up?
    + If I write a new one, would I still do it in Java?
        * BioJava 1.4?  "BioJava 3"?  New API?
    + Alternatively... do a "Dazzle 1.5" major update
        * possible to keep the decent bits while re-doing the plugin API?
 - DAS3? :-)