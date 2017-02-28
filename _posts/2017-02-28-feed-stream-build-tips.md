---
layout: single
title: feed stream build tips 
tags: [feed, stream, activity]
---
The brief design is

* Actor. The object that performed the activity.
* Verb. The verb phrase that identifies the action of the activity.
* Action Object. (Optional) The object linked to the action itself.
* Target. (Optional) The object to which the activity was performed.

For example: justquick (actor) closed (verb) issue 2 (object) on django-activity-stream(target) 12 hours ago

For user friendly,

1. we can combine the actors into one line to make the feeds less;
2. we can use redis to generate feeds per user (feed:user\_id);
3. split online users and offline users, push the online users first.

We can build this with good design frameworks: [Django Activity Stream ][1] and [getstream][2].

[1]:	http://django-activity-stream.readthedocs.io/en/latest/
[2]:	http://getstream.io/