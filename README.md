# Dubtrack unofficial API
This repository contains all the information about the dubtrack.fm API.

This reference is unofficial mostly found out by testing. It is also work in process so there may be a few errors (right now everything had been tested except for some features of playlist, room queue and user queue).

## About
If you found this is probably because you are looking for some dubtrack API documentation. The official is not updatted and I couldn't find another reference site. I needed the call reference for a project: [DubBot](https://github.com/copying/DubBot). I don't want more people to feel the pain of looking for the calls so here it is.

## Introduction
Dubtrack's protocol makes calls to `https://api.dubtrack.fm/`. If it request information, it will return the desired value.

To send information to the client, it will use a [PubNub](https://www.pubnub.com/). The client will recive informative messages. We won't, in any case, post messages (instead we will use HTTPS calls to the API). The PubNub requires a subscribe key to be able to recive this messages. The subscription key is `sub-c-2b40f72a-6b59-11e3-ab46-02ee2ddab7fe` (found it out there and works perfectly).

## More information
[Dubtrack's HTTPS calls reference](https://github.com/copying/dubtrack-unofficial-API/blob/master/call-reference.md)

[Dubtrack's PubNub messages reference](https://github.com/copying/dubtrack-unofficial-API/blob/master/pubnub-reference.md)

## Help in this reference
Any help is welcomed. This reference has yet to be fully tested and I know for sure that there are missing things.
