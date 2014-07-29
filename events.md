---
layout: page
title: Joind.in API Documentation
---
## Events

This page deals with the various event pages and data structures of events.

## Landing Page

[{{ site.apiurl }}]({{ site.apiurl }})

Output:

~~~~
events: {{ site.apiurl }}/v2.1/events
hot-events: {{ site.apiurl }}/v2.1/events?filter=hot
upcoming-events: {{ site.apiurl }}/v2.1/events?filter=upcoming
past-events: {{ site.apiurl }}/v2.1/events?filter=past
open-cfps: {{ site.apiurl }}/v2.1/events?filter=cfp
~~~~

## Filtering the Events Collection

We currently support the following parameters for filtering events:

*  ``filter``: as shown in the landing page example, this can take the following values:

   - ``hot``: the "hot" events; these are soon/recent events, with priority given to events with the most attendees.  Usually the default view.
   - ``upcoming``: future events, sorted by date with the soonest first
   - ``past``: past events, sorted by date with the most recent first
   - ``cfps``: events that currently have open CfPs

*  ``title``: Search for an event by title (partial match, e.g."Benelux" will find "PHP Benelux Conference 2014")
*  ``stub``: Search for an event by its short name (exact match, e.g. "phpbnl14")
*  ``tags``: Events with a particular tag.  You can supply as many of these as you like by doing something like ``tags[]=php&tags[]=community``
*  ``startdate``: Search for events on or after this date (should be fairly flexible about what date format you give it)
*  ``enddate``: Search for events before this date (should be fairly flexible about what date format you give it)

You can supply as many of these as you wish; the filters will combine for the most part.

## Event Format

When requesting either one event or a collection of events, your data response will include both a root ``events`` element with a numerically-indexed results array, and a ``meta`` element (see [{{ site.baseurl }}/index.html]({{ site.baseurl }}/index.html)

An example of a single event (using sample data):

~~~~
events:
    0:
        name: DevConf
        url_friendly_name: devconf-2014
        start_date: 2014-01-07T00:00:00+01:00
        end_date: 2014-01-09T23:59:59+01:00
        description: Aliquam vulputate vulputate lobortis. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Pellentesque elementum placerat lectus, sit amet dictum urna euismod quis. Suspendisse mattis suscipit ante, nec consectetur magna aliquet non. Vivamus gravida, dolor ut porta bibendum, mauris ligula condimentum est, id facilisis ante massa a justo.
        stub: D125
        href: http://devconf.example.org
        attendee_count: 5
        attending:
        event_comments_count: 2
        tracks_count: 1
        talks_count: 5
        icon:
        tags:
        uri: {{ site.apiurl }}/v2.1/events/3
        verbose_uri: {{ site.apiurl }}/v2.1/events/3?verbose=yes
        comments_uri: {{ site.apiurl }}/v2.1/events/3/comments
        talks_uri: {{ site.apiurl }}/v2.1/events/3/talks
        attending_uri: {{ site.apiurl }}/v2.1/events/3/attending
        website_uri: http://joind.in/event/view/3
        humane_website_uri: http://joind.in/event/D125
        attendees_uri: {{ site.apiurl }}/v2.1/events/3/attendees
meta:
    count: 1
    this_page: {{ site.apiurl }}/v2.1/events/3?start=0&resultsperpage=20
~~~~

## Verbose Event Format

Append ``verbose=yes`` to the URL to get more fields.  The data format will be:

~~~~
events:
    0:
        name: DevConf
        url_friendly_name: devconf-2014
        start_date: 2014-01-07T00:00:00+01:00
        end_date: 2014-01-09T23:59:59+01:00
        description: Aliquam vulputate vulputate lobortis. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Pellentesque elementum placerat lectus, sit amet dictum urna euismod quis. Suspendisse mattis suscipit ante, nec consectetur magna aliquet non. Vivamus gravida, dolor ut porta bibendum, mauris ligula condimentum est, id facilisis ante massa a justo.
        stub: D125
        href: http://devconf.example.org
        icon:
        latitude: 32.4976260000000000
        longitude: -86.3685450000000000
        tz_continent: Europe
        tz_place: Amsterdam
        location: Millbrook
        hashtag: #D125
        attendee_count: 5
        attending:
        comments_enabled: 1
        event_comments_count: 2
        tracks_count: 1
        talks_count: 5
        cfp_start_date: 2014-01-01T01:00:00+01:00
        cfp_end_date: 2014-01-04T01:00:00+01:00
        cfp_url: http://devconf.example.org/cfp
        talk_comments_count: 12
        tags:
        uri: http://api.joindin.local/v2.1/events/3
        verbose_uri: http://api.joindin.local/v2.1/events/3?verbose=yes
        comments_uri: http://api.joindin.local/v2.1/events/3/comments
        talks_uri: http://api.joindin.local/v2.1/events/3/talks
        attending_uri: http://api.joindin.local/v2.1/events/3/attending
        website_uri: http://joind.in/event/view/3
        humane_website_uri: http://joind.in/event/D125
        all_talk_comments_uri: http://api.joindin.local/v2.1/events/3/talk_comments
        hosts:
            0:
                host_name: Bruce Simmons
                host_uri: http://api.joindin.local/v2.1/users/2
            1:
                host_name: James Barnes
                host_uri: http://api.joindin.local/v2.1/users/11
            2:
                host_name: Arthur Dunn
                host_uri: http://api.joindin.local/v2.1/users/9
            3:
                host_name: Jennifer Cole
                host_uri: http://api.joindin.local/v2.1/users/5
        attendees_uri: http://api.joindin.local/v2.1/events/3/attendees
meta:
    count: 1
    this_page: http://api.joindin.local/v2.1/events/3?verbose=yes&start=0&resultsperpage=20
~~~~

## Event Data Fields

*  ``name``: The event name
*  ``url-friendly-name``: An inflected version of the event name that is url safe.
*  ``start_date``: The beginning of the event in ISO format
*  ``end_date``: The end of the event in ISO format
*  ``description``: Some information about the event
*  ``stub``: A short, unique identifier for this event.  Used by the website to make a quicklink
*  ``href``: URL for the event's own website
*  ``icon``: URL for this event's logo or icon used on the joind.in site
*  ``latitude``: Where the event geographically is
*  ``longitude``:  Where the event geographically is
*  ``tz_continent``: Continent part of the timezone identifier
*  ``tz_place``: Second part of the timezone identifier
*  ``location``: Name of the venue or event location
*  ``hashtag``: The hashtag to use on social networks when referring to this event
*  ``attendee_count``: Calculated field showing how many people are marked as attending this event
*  ``attending``: Whether the current user (if any) is attending this event
*  ``comments_enabled``: Whether this event is currently open for comment
*  ``event_comments_count``: Calculated field showing how many event comments have been made on this event
*  ``tracks_count``: Number of tracks at this event
*  ``talks_count``: Total number of talks at this event, across all tracks
*  ``cfp_start_date``: When the call for papers will begin, in ISO format
*  ``cfp_end_date``: When the call for papers will end, in ISO format
*  ``cfp_url``: The URL for finding out more about the call for papers
*  ``talk_comments_count``: Calculated field showing how many comments were made across all the sessions at the event.
*  ``tags``: An array of tags applied to this event to facilitate finding similar events
*  ``website_uri``: Where to find the website joind.in page for this event
*  ``website_humane_uri``: Where to find the website joind.in page for this event, using the quicklink if there is one (depends whether the event has a stub)
*  ``hosts``: The organisers for this event.  An array where each element gives both the ``host_uri`` of the user and a display name to use.  *See also* [users]({{ site.baseurl}}/users.html)


## Event Hypermedia

There are links to other useful places in the API.  These are:

*  ``uri``: This event (useful if you see the result in a collection and only want one of it), the URI is the event identifier.
*  ``verbose_uri``: The verbose representation of the event.
*  ``comments_uri``: The *event* comments on this event (talk comments are separate).  *See also* [event comments]({{ site.baseurl }}/event_comments.html).
*  ``talks_uri``:  All the talks and other sessions delivered at this event.  *See also* [talks]({{ site.baseurl }}/talks.html).
*  ``attending_uri``: POST/DELETE to this URI as an authenticated user to indictate that you are/aren't attending (current attending status is in the ``attending`` field).
*  ``all_talkcomments_uri``: All the comments from all of the talks at this event, in order of date with the newest comments first. *See also* [talk comments]({{ site.baseurl }}).
*  ``attendees_uri``: A list of all users marked as attending this event.  *See also* [users]({{ site.baseurl}}/users.html).


## Submitting Events

You can submit events for approval via the API (site admins events are auto-approved) by POSTing to the main events collection.

Here's an example:

<pre class="embedcurl"> curl -v -H "Content-Type: application/json" -H "Authorization: OAuth 2ffcd58992c73241" -X POST http://api.dev.joind.in:8080/v2.1/events/ -d '{"name": "New Event", "description": "this is going to be an awesome event, where great talks will take place and many people will gather", "start_date": "2014-09-08T12:15:00+01:00", "end_date": "2014-09-11T20:00:00+01:00", "tz_continent": "Europe", "tz_place": "Madrid"}'
</pre>

<!-- You only need to reference this script once per page. -->
<script src="https://www.embedcurl.com/embedcurl.min.js" async></script>

These are the only required fields:

 * ``name``
 * ``description``
 * ``start_date`` (PHP uses strtotime to parse this field, it's pretty tolerant)
 * ``end_date`` (PHP uses strtotime to parse this field, it's pretty tolerant)
 * ``tz_continent`` (e.g. "Europe", "America")
 * ``tz_place`` (e.g. "Amsterdam", "Chicago")

You may also add any or all of these additional fields:

 * ``href`` must be a valid URL
 * ``cfp_url`` must be a valid URL
 * ``cfp_start_date`` (PHP uses strtotime to parse this field, it's pretty tolerant)
 * ``cfp_end_date`` (PHP uses strtotime to parse this field, it's pretty tolerant)
 
The response should include a 201 Created header.  Here is an example of a full request and response:

~~~~
> POST /v2.1/events/ HTTP/1.1
> User-Agent: curl/7.32.0
> Host: api.dev.joind.in:8080
> Accept: */*
> Content-Type: application/json
> Authorization: OAuth 2ffcd58992c73241
> Content-Length: 271
> 
* upload completely sent off: 271 out of 271 bytes
< HTTP/1.1 201 Created
< Date: Sun, 02 Mar 2014 20:26:02 GMT
* Server Apache/2.2.15 (CentOS) is not blacklisted
< Server: Apache/2.2.15 (CentOS)
< X-Powered-By: PHP/5.3.3
< Location: http://api.dev.joind.in:8080/v2.1/events/
< Content-Length: 0
< Connection: close
< Content-Type: text/html; charset=UTF-8
< 
~~~~
