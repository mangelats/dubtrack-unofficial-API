# Endpoints
This page only contains a list of endpoints. The ful reference [can be found here](https://github.com/copying/dubtrack-unofficial-API/blob/master/call-reference.md) (They are ordered the exact same way, so this can be used to search for specific calls).

## Account
 - Log in: `POST /auth/dubtrack`
 - Log out: `GET /auth/logout`
 - Your basic info: `GET /auth/session`

## User
 - Info: `GET /user/{userid|username}`
 - Image: `GET /user/{userid}/image` and `GET /user/{userid}/image/large`
 - Followers `GET /user/{userid}/following`
 - Follow `POST /user/{userid}/following`
 - Unfollow `DELETE /user/{userid}/following`

## Playlists
 - Playlist list `GET /playlist`
 - Make new `POST /playlist`
 - Delete `DELETE /playlist/{playlistid}`
 - Songs `GET /playlist/{playlistid}/songs`
 - Add song `POST /playlist/{playlistid}/songs`
 - Remove song `REMOVE /playlist/{playlistid}/songs/{songid}`

## Room
 - Global aviable list: `GET /room`
 - Create room: `POST /room`
 - Update room `PUT /room/{roomid}`
 - Room details `GET /room/{roomid|roomUrl}`
 - Room users `GET /room/{roomid}/users`
 - Room muted users `GET /room/{roomid}/users/mute`
 - Room banned users `GET /room/{roomid}/users/ban`
 - Room user details `GET /room/{roomid}/users/{userid}`
 - Join room  none (uses PubNub)
 - Leave room `DELETE /room/{roomid}/users`
 - Send chat message `POST /chat/{roomid}`
 - Delete chat message `DELETE /chat/{roomid}/{messageid}`

## Room moderation
 - Kick user `POST chat/kick/{roomid}/user/{userid}`
 - Mute user `POST chat/mute/{roomid}/user/{userid}`
 - Unmute user `DELETE chat/mute/{roomid}/user/{userid}`
 - Ban user `POST chat/ban/{roomid}/user/{userid}`
 - Unban user `DELETE chat/ban/{roomid}/user/{userid}`
 - Set user role `POST /chat/{roleid}/{roomid}/user/{userid}`

## Room queue
 - Queue `GET room/{roomid}/playlist`
 - Queue details `GET room/{roomid}/playlist/details`
 - Current song `GET room/{roomid}/playlist/active`
 - Current song's dubs `GET room/{roomid}/playlist/active/dubs`
 - Skip song `POST chat/skip/{roomid}/{songid}`
 - Reorder `POST room/{roomid}/queue/order`
 - Remove user's song `DELETE room/{roomid}/queue/user/{userid}`
 - Remove DJ (remove all its songs) `DELETE room/{roomid}/queue/user/{userid}/all`
 - Pause/play `PUT room/{roomid}/queue/user/{userid}/pause`
 - Vote `POST room/{roomid}/playlist/{songid}/dubs`

## Room user's queue
 - Queue `GET user/session/room/{roomid}/queue`
 - Add song `POST room/{roomid}/playlist`
 - Delete song `DELETE room/{roomid}/playlist/{songid}`
 - Delete all song `DELETE room/{roomid}/playlist`
 - Lock/Unlock queue `POST /room/{roomid}/lockQueue`

## Song
 - Search `GET /song`
 - Details `GET song/{songid|songfkid}`
 - Redirect `GET song/{songid}/redirect`

## Private Messages (AKA conversations)
 - Open `GET /message`
 - New PM room `POST /message`
 - Poll for new messages `GET /new`
 - Details (including messages) `GET/message/{conversationid}`
 - Send PM `POST /message/{conversationid}`
 - Mark message as read `POST /message/{conversationid}/read`
