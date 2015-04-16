# Trail Assist: Agency Data + Citizen Data

* [Seth Fitzsimmons](https://github.com/mojodna), [Stamen
  Design](http://stamen.com/)
* [Jereme Monteau](https://github.com/jmoe), [Trailhead Labs](http://www.trailheadlabs.com/)
* [Dan Rademacher](https://github.com/danrademacher), [Stamen
  Design](http://stamen.com/)

[![Slides on SpeakerDeck](https://speakerd.s3.amazonaws.com/presentations/2272aee5bea24dd080363f0b8729a719/slide_0.jpg)](https://speakerdeck.com/mojodna/trail-assist)

Our goal over the weekend of the [#dev4outdoors
hackathon](http://openglobe.github.io/myamerica-devsummit/) at the Department
of the Interior was to make substantial progress on adding detail and texture
inside the 3,000+ parks in the [Recreation Information Database
(RIDB)](https://ridb.recreation.gov/).

The RIDB gets you point locations and more than 40 text attributes like
“camping” and “paddling.”

But where exactly are those amenities? And what do those parks actually look
like? People visit parks not for the point at the other end of a driving route
but rather for the rich experience they’ll have when they get there.

They’re going to want to know what that experience is before they get there.
And once they’re, they want a good map.

When faced with thousands of parks, we think social media and open data are key
resources to not only fill in the gaps but also show the diversity of
experiences you can have in parks.

So, how to fill in a map like this?

![]()

Ask all the people: Agency staff, park volunteers,
[OpenStreetMappers](http://openstreetmap.org/), social media users. Fill in the
details of the park with help from social media and crowd-sourced map data!

On [Caliparks.org](http://www.caliparks.org/), we harvest Instagram photos to
show how people experience thousands of parks:

![]()

[Trailhead Labs](http://www.trailheadlabs.com/) built the [open
source](https://github.com/CodeForPortland/trailheadit)
[traileditor.org](http://traileditor.org/) so people can email in photos of
trailheads, to build a crowd-sourced trailhead database with images and
detailed information:

![]()

But crowdsourced data is not without its challenges. It can work amazingly well
at scale, but it can also be wrong.

That’s where Trail Assist comes in. We propose to make it easier than ever for
the parks community, including park visitors, to report and flag bootleg trails
(also called social trails or even desire lines). The system can also help
agencies improve their own data.

First, email a photo of the suspected bootleg trail to
[social@traileditor.org](mailto:social@traileditor.org), and that will add it
to the TrailEditor site.

Then we provide some information about what bootleg trails are and why we
should be concerned about them.

But more important, we push that point location to [OpenStreetMap
(OSM)](http://openstreetmap.org/), the largest and most detailed publicly
accessible map of the world ever made.

That information then appears on OSM and alerts agencies or volunteer mappers
that they should inspect the area more closely.

For that, we’ve begun developing tools that make it much simpler to see where
open data and official data differ.

Working within the open source [Java OSM editor
(JOSM)](https://josm.openstreetmap.de/), we used some tools built by
[Stamen](http://stamen.com/) (the backend of [Map
Stack](http://mapstack.stamen.com)) and API integration with
[CartoDB](http://cartodb.com/) to make a view like this:</p>

![]()

The yellow is agency data. The magenta is OSM data, and the variable blue lines
are the [Strava](http://strava.com/) [Global
Heatmap](http://labs.strava.com/heatmap/). We use layer compositing blend modes
to make yellow and magenta cancel to white, and then layer on the Strava map,
making it instantly obvious which trails are most likely to be social trails
and which of those are most heavily used.

## Bringing richer trails data into the OSM community

One of our key goals is to improve data within OSM in a way that is true to the
community that makes the map, and therefore gets owned by volunteer mappers,
vastly increasing the likelihood that data quality will be maintained and
improved over time.

While we worked on-site during the hackathon, we engaged in a larger
conversation (via Slack and social media) with members of the OSM community
about trails and trailhead data. Brandon Knight
([@geobrando](https://twitter.com/geobrando)) published a detailed proposal for
[a new standard for defining trailheads within
OSM](https://wiki.openstreetmap.org/wiki/Proposed_features/trailhead).

That inspired community discussion (so far, 20 responses in the community
thread), and a clear, succinct definition (in our opinion) emerged:
A transition point between a trail network and the developed transportation
network of roads, mass transit, etc. (See the start of the discussion
[here](https://lists.openstreetmap.org/pipermail/tagging/2015-April/023797.html).)

In our work at the hackathon, we also began circulating a proposal for a new
`social_path` tag to clearly mark areas where trails exist that aren’t part of
the official trail network.

Our goals for this proposal are twofold: to enrich the data already present
within OSM and to facilitate exclusion of such trails.  Deleting unsanctioned
trails is problematic, as they clearly exist in the real world.

Like roads, most trails fall under the responsibility of a government agency
that designates the permitted uses of a trail (whether horses or bikes are
allowed, for example), and they also determine when a trail should not be used,
particularly if there are safety or environmental considerations. The trail
still exists, and (rather than deleting it) we can further specify its
characteristics within OSM.

Beyond preventing edit wars, we attempted to come up with a scheme that would
facilitate easy exclusion of the data from most maps (to discourage use in the
real world) while remaining available for cases when such data is legitimately
useful (e.g. for evacuation or firefighting). Within the OSM community, such
tagging could be considered “tagging for the renderer” (since there’s a clear
intent to influence how they’re displayed, and this is generally discouraged),
but we prefer to look at it as being akin to describing the precedence and use
of roads using `highway=tertiary`, `highway=service`, etc.

As with roads, not all trails are equal.

For developers of websites and apps for parks, there’s a huge benefit in using
OSM as a (free!) one-stop-shop for data regardless of jurisdiction. In fact,
the benefit is so huge that developers will keep doing it. Even if the data is
wrong.

Better to make the data right AND provide easy tools for hiding or marking
prohibited trails. So let map designers query for trails where `highway !=
social_path` and they get to serve better data, while agencies get a clear path
to better maps across products they might not even know about and the open data
community gets more accurate data.

## What’s next?

* Enhance the proof of concept to more easily incorporate data from any source.
* Investigate potential integration with the [NPMap](http://www.nps.gov/npmap/)
  team’s [Places Editor modifications to
  iD](http://nationalparkservice.github.io/places-editor/edit/).
* Work with the OSM community and local agencies to propose and drive adoption
  of a social trail tagging norm.
* Organize a grassroots Trail Blitz in the Bay Area to field test the tools.
* Field test the tools with data from local agencies.
* Package up the tools for use by others.
