# Dubtrack unofficial API
This repository contains all the information about the dubtrack.fm API.

This reference is unofficial mostly found out by testing. It is also work in process so there may be a few errors (right now everything had been tested except for some features of playlist, room queue and user queue).

## Introduction

Dubtrack's protocol makes calls to `https://api.dubtrack.fm/`. If it request information, it will return the desired value.

To send information to the client, it will use a [PubNub](). The client will recive informative messages. We won't, in any case, post messages (instead we will use HTTPS calls to the API). The PubNub requires a subscribe key to be able to recive this messages. The subscription key is `sub-c-2b40f72a-6b59-11e3-ab46-02ee2ddab7fe` (found it out there and works perfectly).

## More information
[Dubtrack's HTTPS calls reference](https://github.com/copying/dub-bot/wiki/dubtrack-call-reference)

[Dubtrack's PubNub messages reference](https://github.com/copying/dub-bot/wiki/dubtrack-pubnub-reference)

## Help in this reference
Any help is welcomed. This reference has yet to be fully tested and I know for sure that there are missing things.
