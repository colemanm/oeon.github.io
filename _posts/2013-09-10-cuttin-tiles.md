---
layout: post
title: cuttin tiles
tagline: "Dirty little tiles, rolled by hand, with free software."
category: work
tags:
  - gdal
  - gdal2tiles
  - vrt
published: true
style: |
  body {
    font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  }
---

<a href="http://www.flickr.com/photos/icathing/9860160/" title="Tile bench by icathing, on Flickr"><img src="http://farm1.staticflickr.com/5/9860160_ff26d182e3.jpg" width="500" height="375" alt="Tile bench"></a>

**tl:dr** This is adventure with GDAL, specifically gdal2tiles and the VRT format. I had more than 1,000 'raw' .tif files of 1-foot resolution imagery, totalling 300+ gigabytes. Looking for 'web tiles' / a Tile Map Service ([TMS](http://wiki.openstreetmap.org/wiki/Setting_up_TMS)), I stumbled upon the adventures below…

<a href="http://www.flickr.com/photos/skinnylawyer/8144013050/" title="Space Shuttle Endeavour at California Science Center by InSapphoWeTrust, on Flickr"><img src="http://farm9.staticflickr.com/8053/8144013050_a0b983b4e0_m.jpg" width="240" height="159" alt="Space Shuttle Endeavour at California Science Center"></a>

My local County acquired countywide 1-foot imagery. At work, we are often editing OpenStreetMap and we wanted to use our own current/more-accurate data, so we built "a VRT (Virtual Dataset) that is a mosaic of the list of input GDAL datasets", *warped* it to web mercator and cut it up with gdal2tiles.

1. `gdalbuildvrt merge.vrt *.tif` mosaic/merge all teh .tif files

2. `gdalwarp -t_srs EPSG:3857 -dstnodata 0 -of VRT merge.vrt mergewarp.vrt` warp them alls, `-dstnodata 0` worked to carry through the input nodata - [*i think*](http://trac.osgeo.org/gdal/wiki/UserDocs/GdalWarp)

3. `mkdir tiles` make a folder for your output

4. `gdal2tiles.py -v mergewarp.vrt tiles/` many options, see the [docs](http://www.gdal.org/gdal2tiles.html). You'll want to use `-e` if you need to stop/resume a job (see below).  

---

>joe larson @oeon
>rough calcs say 34 hours for gdal2tiles to cut zoom 18

---

*^temporary^ see [tweet](https://twitter.com/oeon/status/376159617450901504) since I can't embed without breaking Jekyll - yes, I tried [this](https://github.com/scottwb/jekyll-tweet-tag/issues/1) already :/*

I started the job on a Friday night and sometime Monday it finished. 1.24 million .png tiles and 91-ish gigabytes later - done! By default zoom level 7 - 18 were made.

<a href="http://www.flickr.com/photos/the-consortium/7238535480/" title="House of the Faun by The Consortium, on Flickr"><img src="http://farm8.staticflickr.com/7076/7238535480_8d5d3cec86_m.jpg" width="240" height="180" alt="House of the Faun"></a>

Dirty little tiles, rolled by hand, with free software.

<a href="http://www.flickr.com/photos/j03lar50n/9715500498/" title="Screen Shot 2013-09-09 at 8.22.17 PM by j03lar50n, on Flickr"><img src="http://farm3.staticflickr.com/2847/9715500498_d01aff3efa_c.jpg" width="800" height="530" alt="Screen Shot 2013-09-09 at 8.22.17 PM"></a>

There were a few stragglers because some .tif's were delievered in CA State Plane Zone V meters (instead of [EPSG:2229](spatialreference.org/ref/epsg/2229/) - feet!) but working to get the rest done. Remember that `-e` flag for gdal2tiles I mentioned? Well, this is a situation where you'll need it. I need to delete all the tiles that were created with those nodata/white tiles and run it again, with that flag.

<a href="http://www.flickr.com/photos/j03lar50n/9723873672/" title="vrt-e by j03lar50n, on Flickr"><img src="http://farm8.staticflickr.com/7357/9723873672_cf5e388970_o.gif" width="502" height="564" alt="vrt-e"></a>

### Final stats:
<a href="http://www.flickr.com/photos/j03lar50n/9723599817/" title="tiles_size by j03lar50n, on Flickr"><img src="http://farm8.staticflickr.com/7324/9723599817_2b332c7952_o.png" width="345" height="240" alt="tiles_size"></a>

###Final thoughts:
- Might cut some lower zoom levels - up to 21? Wow, how long will that take?
- Might try saving reducing the TMS total size by using something else (NAIP?) at the higher zoom levels.
- I'm not sure how much compression at the early stages of the processing would effect the results, both quality and size. I am going to see how processing this same area but from MrSID format, will affect size/quality.
- .vrt / VRT has come a long way. Just a couple years ago - I think it was just coming out and things like this weren't possible. Thanks FrankW!

<a href="http://www.flickr.com/photos/robven/3134215506/" title="Alcazar Tiles 17 by roberto_venturini, on Flickr"><img src="http://farm4.staticflickr.com/3285/3134215506_6546eb79af.jpg" width="492" height="500" alt="Alcazar Tiles 17"></a>
