# Dubtrack.fm API protocol
## About
I'm making this unofficial reference because there is no updated one. While I was making this project ([dub-bot](https://github.com/copying/dub-bot)) I didn't find much usefull information. It's being a pain to recollect all this information and I don't want people to have this experience.

This reference is language-free reference. It should work in any programming language if is impemented correctly.

## Introduction

Dubtrack's protocol makes calls to `https://api.dubtrack.fm/`. If it request information, it will return the desired value.

To send information to the client, it will use a [PubNub](). The client will recive informative messages. We won't, in any case, post messages (instead we will use HTTPS calls to the API). The PubNub requires a subscribe key to be able to recive this messages. The subscription key is `sub-c-2b40f72a-6b59-11e3-ab46-02ee2ddab7fe` (found it out there and works perfectly).

## More information
[Dubtrack's HTTPS calls reference](https://github.com/copying/dub-bot/wiki/dubtrack-call-reference)

[Dubtrack's PubNub messages reference](https://github.com/copying/dub-bot/wiki/dubtrack-pubnub-reference)

## Help in this reference
Any help is welcomed. This reference has yet to be fully tested and I know for sure that there are missing things.