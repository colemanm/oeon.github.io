---
title: Finally processed Brasil 2010 tracks
layout: post
style: |
  body {
    font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  }
---  

<p>So, I had heard about <a href="http://sethoscope.net/heatmap/" title="heatmap.py" target="_blank">heatmap.py</a> - you can find it on <a href="https://github.com/sethoscope/heatmap" title="GitHub" target="_blank">GitHub</a> - and wanted to try it out.</p>
<p>We were down in Brasil last year for the Holidays. Every chance I got, I tracked our location from my phone with <a href="http://www.codesector.com/maverick.php" title="Maverick" target="_blank">Maverick</a>. Now, I use <a href="http://www.locusmap.eu/" title="Locus" target="_blank">Locus</a> - mainly because the Author (<a href="http://www.asamm.cz/" title="Menion Asamm" target="_blank">Menion Asamm</a>) incorporated MBTiles support upon <a href="http://forum.asamm.cz/viewtopic.php?p=2114#p2114" title="my suggestion" target="_blank">my suggestion</a>. By the way, I hate my Android phone now and can&#8217;t wait to go back to iOS - however, I digress!</p>
<p>I had about a dozen .gpx tracks and today I finally processed them! The trickiest part was merging them into a single .gpx file. I thought ogr2ogr initially was going to be the way but I ended up using GPSBabel and <a href="http://wiki.openstreetmap.org/wiki/Using_filters_with_GPSBabel#Merge_tracks" title="this method" target="_blank">this method</a> from the OpenStreetMap wiki.</p>
<p>Here was the first output:</p>
<p><a href="http://www.flickr.com/photos/j03lar50n/6391993447/" title="brasil2010 by j03lar50n, on Flickr" target="_blank"><img alt="brasil2010" height="242" src="http://farm8.staticflickr.com/7005/6391993447_79b2c8fca1_b.jpg" width="1024"/></a></p>
<p>The two main places we were hanging however, were <a href="http://en.wikipedia.org/wiki/Arma%C3%A7%C3%A3o_dos_B%C3%BAzios" title="Búzios" target="_blank">Búzios</a> (wow, it really needs some OpenStreetMap data!):</p>
<p><a href="http://www.flickr.com/photos/j03lar50n/6391993653/" title="buz2010 by j03lar50n, on Flickr" target="_blank"><img alt="buz2010" height="640" src="http://farm8.staticflickr.com/7154/6391993653_a5da3a597c_z.jpg" width="429"/></a></p>
<p>and Rio - specifically Urca, Jardim Botanico and across the bridge in Niteroi:</p>
<p><a href="http://www.flickr.com/photos/j03lar50n/6391993953/" title="rio2010 by j03lar50n, on Flickr" target="_blank"><img alt="rio2010" height="788" src="http://farm8.staticflickr.com/7145/6391993953_c8c61e9d9d_b.jpg" width="817"/></a></p>
<p>For my close ups on Buzios and Rio - I imported the merged.gpx into JOSM, converted to .osm and did quick selections around Buzios/Rio &gt; saved back into .gpx and ran heatmap.py again. I know there may be some better ways to do this but it was quick and I got the results I was looking for. Also, I failed on the bash script to do the .gpx merge all-slick-style &#8230; I had to append every .gpx file name into the gpsbabel command - don&#8217;t know if that script on the OSM Wiki works for OS X Terminal too? But happy I got to this before the 1 year mark came, cheers!</p>
