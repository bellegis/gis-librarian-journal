---
layout: post
title: LibraryCloud API pt. 1
subtitle: Starting to explore the Harvard Library catalog API for working with maps
gh-repo: bellegis/gis-librarian-journal
tags: [coding]
author: Belle Lipton
cover-img: /assets/img/cover.png
thumbnail-img: /assets/img/mods.png
share-img: /assets/img/cover.png

---


A quick update today! I have been learning more about the Harvard Library API, [Library Cloud](https://harvardwiki.atlassian.net/wiki/spaces/LibraryStaffDoc/pages/43287734/LibraryCloud+APIs). 

My goals are:

1. Ultimately, to be able to finesse collections we have across various systems so they are easier to work with geospatially for students
2. Get my arms around the HOLLIS API and share what I’ve learned to be relevant to maps with researchers who are interested in accessing our collections this way
3. Get all the extra benefits of getting deeper into our collections as I develop

Starting out, I’ve just been trying a catch-all query across all fields:`q=` along with a filter by ownerCode: `ownerCodeFHCL.MAPS` . This definitely isn’t the most efficient call; I can already tell I’m not capturing everything. For instance, searching for our founding `Ebeling` collection in HOLLIS vs. the applet I’m working on currently only yields 24 results to the astounding 4,211 map results in HOLLIS. I’ll post fixes to this I discover as I chip away at it more.

The first steps so far have been parsing the MODS data. Queries return bibliographic records in MODS format, which is XML structured with tags. I learned about all of the various ways to encode catalog records during library school, but it’s still been a doozy and a refresh to make sense of the MODS structures.

![many hierarchical attributes about a library record](https://bellegis.github.io/gis-librarian-journal/assets/img/mods.png)

For now, I want to display a certain amount of fields, so I can get to know what’s included in the metadata. I can think of all sorts of interesting ways to leverage different fields. Right now, I’m really into the genre fields; it would be pedagogically compelling and a great way into the collections to be able to browse, for instance, by `Genre`. Imagine an image-rich gallery for all `Early works to 1800s` or maps with `Timetables` .

<iframe src="https://uv-v4.netlify.app/uv.html#?manifest=https://iiif.lib.harvard.edu/manifests/ids:482179709&c=0&m=0&cv=0&config=&locales=en-GB:English (GB),cy-GB:Cymraeg,fr-FR:Français (FR),pl-PL:Polski,sv-SE:Svenska&xywh=-246,-61,8180,5070&r=0" width="800" height="600" allowfullscreen frameborder="0"></iframe>

Right now it’s been interesting even just making a mini HOLLIS. 

![searching for Ottens and displaying a map result](https://bellegis.github.io/gis-librarian-journal/assets/img/search.gif)

I was curious what all of the different attributes for image URLs seemed to be for. I’m still not 100% certain on the intended functions for each one, but my favorite I’ve discovered is an attribute `access` with the value `object in context`. This tells you all of the other Harvard Library digital collections a library object has been included in. I’ve always felt a bit out of my depth at the sheer scale of thematic collections here at Harvard, so its been wonderful to see our maps contextualized by the broader impact of the fields they shed light on. So far, I’ve found some of our maps which have been written up in projects such as the [Islamic Heritage Project](https://curiosity.lib.harvard.edu/islamic-heritage-project?utm_source=library.harvard), [Worlds of Change](https://curiosity.lib.harvard.edu/worlds-of-change) documenting records at Harvard that relate to 17th and 18th century North America, and one about [sponsored expeditions and scientific discovery](https://library.harvard.edu/collections/expeditions-and-discoveries-sponsored-exploration-and-scientific-discovery-modern-age). 

Here are some print outs of a MODS structure for one returned record (not including attributes).


``` xml
mods > mods:
mods > titleInfo > titleInfo:
mods > titleInfo > title > title:Nova ac verissima Maris Caspii ante hac maximam fere partem nobis incogniti ac regionum adjacentium delineatio
mods > titleInfo > subTitle > subTitle:jussu invictissimi principis Petri Alexii fil. magni Russorum imperatoris
mods > titleInfo > titleInfo:
mods > titleInfo > title > title:Maris Caspii ante hac maximam fere partem nobis incogniti ac regionum adjacentium delineatio
mods > name > name:
mods > name > namePart > namePart:Ottens, R. (Reinier)
mods > name > namePart > namePart:1698-1750
mods > name > role > role:
mods > name > role > roleTerm > roleTerm:creator
mods > name > name:
mods > name > namePart > namePart:Keizer, Jacob
mods > name > namePart > namePart:active 1706-1750
mods > name > name:
mods > name > namePart > namePart:Ottens, Johanna
mods > name > namePart > namePart:active 1765
mods > name > name:
mods > name > namePart > namePart:Ottens, J. (Josua)
mods > name > namePart > namePart:1704-1765
mods > typeOfResource > typeOfResource:cartographic
mods > genre > genre:map
mods > genre > genre:Early maps
mods > genre > genre:Maps
mods > originInfo > originInfo:
mods > originInfo > place > place:
mods > originInfo > place > placeTerm > placeTerm:ne
mods > originInfo > place > placeTerm > placeTerm:Netherlands
mods > originInfo > place > place:
mods > originInfo > place > placeTerm > placeTerm:Amsterdam
mods > originInfo > publisher > publisher:Gedruk't. ... by de Wed. I. Ottens, op de Nieuwen Dyk in de Werelt kaart
mods > originInfo > dateIssued > dateIssued:[1720?]
mods > originInfo > dateIssued > dateIssued:1720
mods > originInfo > issuance > issuance:monographic
mods > language > language:
mods > language > languageTerm > languageTerm:lat
mods > language > languageTerm > languageTerm:Latin
mods > language > language:
mods > language > languageTerm > languageTerm:dut
mods > physicalDescription > physicalDescription:
mods > physicalDescription > extent > extent:1 map : hand col. ; 47 x 57 cm.
mods > note > note:immenso labore et maximis sumptibus facta, atque ex autographo in lucem edita per Reinerum Ottens geographum Amstelaedam ; Iacob Keyser sculp.
mods > note > note:Covers portions of Iran, Turkmenistan, Kazakhstan, Russia and Azerbaijan.
mods > note > note:Relief shown pictorially. Depth shown by soundings.
mods > note > note:Oriented with North to the left.
mods > note > note:Colored in outline.
mods > note > note:Includes ill.
mods > note > note:Appears in: Atlas maior cum generales omnium totius orbis regnorum rerumpubl. atque insularum tum particulares praecipuarum in iis provinciarum ducatuum comitatuum ceterarum que minorum regionum ac divisionum tabulas geographicas continens ex optimis ac novissimis quibusque variorum autorum tabulis collectus et eleganti ordine dispositus / Reiner Ottens. [1641-1729]. Vol. 7, map No. 23.
mods > note > note:In Latin with a publication note in Dutch and place names in Greek, Russian, Persian, Arabic, and Turkish in Latin script.
mods > subject > subject:
mods > subject > cartographics > cartographics:
mods > subject > cartographics > scale > scale:Scale [ca. 1:2,000,000]
mods > subject > cartographics > coordinates > coordinates:(E 42°00'00"--E 58°35'00"/N 47°55'00"--N 35°36'00").
mods > subject > subject:
mods > subject > geographic > geographic:Caspian Sea Region
mods > subject > genre > genre:Maps
mods > subject > genre > genre:Early works to 1800
mods > subject > subject:
mods > subject > geographic > geographic:Caspian Sea
mods > subject > genre > genre:Maps
mods > subject > genre > genre:Early works to 1800
mods > subject > subject:
mods > subject > geographic > geographic:Caspian Sea Coast
mods > subject > genre > genre:Maps
mods > subject > genre > genre:Early works to 1800
mods > subject > subject:
mods > subject > hierarchicalGeographic > hierarchicalGeographic:
mods > subject > hierarchicalGeographic > country > country:Netherlands
mods > subject > hierarchicalGeographic > city > city:Amsterdam
mods > relatedItem > relatedItem:
mods > relatedItem > titleInfo > titleInfo:
mods > relatedItem > titleInfo > title > title:Open Collections Program at Harvard University
mods > relatedItem > titleInfo > partName > partName:Islamic Heritage Project
mods > relatedItem > relatedItem:
mods > relatedItem > titleInfo > titleInfo:
mods > relatedItem > titleInfo > title > title:Harvard Map Collection
mods > relatedItem > titleInfo > partName > partName:Krawciw Collection
mods > identifier > identifier:646117946
mods > relatedItem > relatedItem:
mods > relatedItem > location > location:
mods > relatedItem > location > url > url:https://id.lib.harvard.edu/alma/990119757930203941/catalog
mods > location > location:
mods > location > url > url:https://nrs.harvard.edu/urn-3:FHCL:3119416?buttons=Y
mods > location > url > url:https://ids.lib.harvard.edu/ids/iiif/13604150/full/,150/0/default.jpg
mods > location > url > url:https://id.lib.harvard.edu/curiosity/islamic-heritage-project/40-990119757930203941
mods > location > url > url:https://id.lib.harvard.edu/digital_collections/990119757930203941
mods > location > holdingSimple > holdingSimple:
mods > location > holdingSimple > copyInformation > copyInformation:
mods > location > holdingSimple > copyInformation > note > note:Electronic reproduction. Cambridge, Mass. : Harvard College Library Digital Imaging Group, 2009. (Open Collections Program at Harvard University. Islamic Heritage Project). Copy digitized: XXXXX Library: [call no.].
mods > location > location:
mods > location > physicalLocation > physicalLocation:Harvard Map Collection, Harvard University
mods > location > shelfLocator > shelfLocator:G5692.C3 1720 .O8 1-2
mods > extension > extension:
mods > extension > extension:
mods > extension > extension:
mods > recordInfo > recordInfo:
mods > recordInfo > descriptionStandard > descriptionStandard:aacr
mods > recordInfo > recordCreationDate > recordCreationDate:090518
mods > recordInfo > recordChangeDate > recordChangeDate:20200715
mods > recordInfo > recordIdentifier > recordIdentifier:990119757930203941
mods > recordInfo > recordOrigin > recordOrigin:Converted from MARCXML to MODS version 3.6 using MARC21slim2MODS3-6.xsl
        (Revision 1.117 2017/02/14)

```