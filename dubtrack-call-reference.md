# Protocol Reference
This article is a list of all the found calls to teh dubtrack.fm server.

There are still missing most of returned objects (but it is written that they return one).

For a list of endpoints you can [follow this link](https://github.com/copying/dub-bot/wiki/endpoints) (it is in the exact same order so it's also usefull to find a specific call).

## Account
#### Log in
`POST /auth/dubtrack`
 - username
 - password

#### Log out
`GET /auth/logout`

#### Basic info
Gets your information

`GET /auth/session`

**Returns**
```js
//Everything without comment are ignored
//The only exception is for sending a PM
{
	"_force_updated":<Number>,
	"userInfo":{
		"_id":<String>, //this is userInfo id (not users so not used)
		"userid":<String>, //user id
		"__v":0
	},
	"_id": <String>, //user object id (the same as user id)
	"username":<String>, //username
	"status":1, //?
	"roleid":<Number>, //id of the permissions you have
	"dubs":0,	//dubs you have
	"created":<Number>, //time where the account was created
	"profileImage":{
		"public_id":<String>,
		"version":<Number>,
		"width":<Number>,
		"height":<Number>,
		"format":"png",
		"resource_type":
		"image",
		"tags":[],
		"bytes":<Number>,
		"type":"upload",
		"etag":<String>,
		"url":<url>,
		"secure_url":<url>
	},
	"__v":0
}
```




## User
#### Info
`GET /user/{userid|username}`

**Returns**
```js
{
	"userInfo":{
		"_id":<String>, //this is userInfo id (not users so not used)
		"userid":<String>, //user id
		"__v":0
	},
	"_id":<String>, //user id
	"username":<String>, //username
	"status":1,
	"roleid":1,
	"dubs":0,
	"created":<Number>, //time where the account was created
	"profileImage":{
		"public_id":<String>,
		"version":<Number>,
		"width":<Number>,
		"height":<Number>,
		"format":"png",
		"resource_type":"image",
		"tags":[],
		"bytes":321903,
		"type":"upload",
		"etag":<String>,
		"url":<url>,
		"secure_url":<url>
	},
	"__v":0
}
```

#### Image
`GET /user/{userid}/image` (normal size)

`GET /user/{userid}/image/large` (large size)

**Redirects**
To the image file.

#### Followers
`GET /user/{userid}/following`

**Array of Object**
```js
//Array of this types of objects
{
	"_id":<String>, //object id (should be ignored)
	"userid":<String>, //follower id
	"following":<String>, //followed id
	"created":<Number>, //When the follower followed him 
	"__v":0
}
```

#### Follow
`POST /user/{userid}/following`

#### Unfollow
`DELETE /user/{userid}/following`





## Playlists
#### Playlist list
`GET /playlist`

**Returns array of**
```js
{
	"_id":<String>, //playlist id
	"name":<String>, //playlist name
	"status":1, //??? (provable internal)
	"removed":<Boolean>,
	"isPublic":<Boolean>,
	"created":<Number>, //time where it was created
	"type":<String>, //If it's an imported playlist, if it's from 'youtube' or 'soundcloud'. null otherwise.
	"fkid":<String>, //If it's an imported playlist, id from the original site. null otherwise.
	"userid":<String>, //user id of who has it
	"__v":0,
	"totalItems":<Number> //Total number of items the playlist has
}
```

#### Make new
`POST /playlist`

**Form**
 - `name` playlist name
 - `isPublic` if the playlist is public (used?)

#### Delete
`DELETE /playlist/{playlistid}`

#### Songs
`GET /playlist/{playlistid}/songs`

**Form**
 - `page` (optional) page of the playlist
 - `name` (optional) name filter

#### Add song
`POST /playlist/{playlistid}/songs`

**Form**
 - `type` 'youtube' or 'soundcloud'
 - `fkid` id of the song (depens if it is from souncloud or youtube)

#### Remove song
`REMOVE /playlist/{playlistid}/songs/{songid}`




## Room
#### Global aviable list
`GET /room`

**Returns**

Array of objects with the information about the room (quite a lot!).

#### Create room:
`POST /room`

**Form**

Object with the information about the room.

**Warning:** Every user can have a maximum of 5 rooms which at the moment can't be deleted.

#### Update room
`PUT /room/{roomid}`

**Form**

Object of the new data of the room.


#### Room details
`GET /room/{roomid|roomUrl}`

**Returns**

Object with the information about the room.

#### Room users
`GET /room/{roomid}/users`

**Returns**

Array of user objects.

#### Room muted users
`GET /room/{roomid}/users/mute`

**Returns**

Array of user objects.

#### Room banned users
`GET /room/{roomid}/users/ban`

**Returns**

Array of user objects.
`
#### Room user details
`GET /room/{roomid}/users/{userid}`

**Returns**

Object with information about this user in this room (user's information, dubs, how many times his songs had been skipped, etc.)

#### Leave room
`DELETE /room/{roomid}/users`

#### Send chat message
`POST /chat/{roomid}`

**Form**
 - `message`
 - `time` current time
 - `realTimeChannel` NubPub chat id
 - `type` must be 'chat-message'

#### Delete chat message
`DELETE /chat/{roomid}/{messageid}`




## Room moderation
#### Kick user
`POST chat/kick/{roomid}/user/{userid}`

**Form**
- `realTimeChannel`
- `message` message to send with the kick.

#### Mute user
`POST chat/mute/{roomid}/user/{userid}`

#### Unmute user
`DELETE chat/mute/{roomid}/user/{userid}`

**Form**
- `realTimeChannel`

#### Ban user
`POST chat/ban/{roomid}/user/{userid}`

**Form**
- `realTimeChannel`
- `time` time in minuts of the ban

#### Unban user
`DELETE chat/ban/{roomid}/user/{userid}`

**Form**
- `realTimeChannel`

#### Set user role
`POST /chat/{roleid}/{roomid}/user/{userid}`



## Room queue
#### Queue 
`GET room/{roomid}/playlist`

**Returns**

Array of Song objects (the order is the queue order).

#### Queue details 
`GET room/{roomid}/playlist/details`

**Returns**

Array of Song objects with details (the order is the queue order).

#### Current song 
`GET room/{roomid}/playlist/active`

**Returns**

A Song object.

#### Current song's dubs 
`GET room/{roomid}/playlist/active/dubs`

**Returns**

TO DO 

#### Skip song 
`POST chat/skip/{roomid}/{songid}`

#### Reorder 
`POST room/{roomid}/queue/order`

**Form**

Object with the new order.

#### Remove user's song 
`DELETE room/{roomid}/queue/user/{userid}`

#### Remove DJ (remove all its songs) 
`DELETE room/{roomid}/queue/user/{userid}/all`

#### Pause/play 
`PUT room/{roomid}/queue/user/{userid}/pause`

**Form**
 - `pause` If it's paused or unpaused ('1' if paused, '0' if not).

#### Vote 
`POST room/{roomid}/playlist/{songid}/dubs`

**Form**
 - `type` 'updub' or 'downdub'

#### Lock/Unlock queue
`POST /room/{roomid}/lockQueue`
 - `lockQueue` '0' or '1' ('1' is to lock, '0' to unlock)




## Room user's queue
#### Queue
`GET user/session/room/{roomid}/queue`

**Returns**

Array of Songs of the queue (in order).

#### Add song
`POST room/{roomid}/playlist`

**Form**
 - `songType` 'youtube' or 'soundcloud'
 - `songId` (usually called fkid throw the API) id of the song (depens if it is from souncloud or youtube)

#### Delete song
`DELETE room/{roomid}/playlist/{songid}`

#### Delete all song
`DELETE room/{roomid}/playlist`

#### Reorder songs
`POST user/session/room/{roomid}/playlist/order`

**Form**

 - `order[]` id of the song (one for every song).



## Song
#### Search
`GET /song`

**Form**
 - `type` 'youtube' or 'soundcloud'
 - `name` The searched string
 - `details` ??? (seems how detailed the information is wanted)
 - `nextPageToken` Part of the page system.

**Returns**

Object with information. Once of this is the list of items (result of the search).

#### Details
`GET song/{songid|songfkid}`

**Returns**

Song object (obviouly with all the details).

#### Redirect
`GET song/{songid}/redirect`

**Redirects** to the original song/video (in YouTube or SoundCloud).




## Private messages (AKA conversations)
#### Open chats
`GET /message`

**Returns**

List of the open conversations.

#### New conversation room
`POST /message`

**Form**
 - `usersid[]` id of the user. This same parameter is used for all the people in the chat (maximum of 10).

#### Poll for new (unread) messages
`GET /new`

**Returns**

Number of unread conversations.

#### Conversation details (and messages)
`GET/message/{conversationid}`

**Returns**

Details about the private chat, including the messages (which is why it is used for).

#### Send message
`POST /message/{conversationid}`
 - `message` Message to be sended
 - `time` current time


#### Mark message as read
`POST /message/{conversationid}/read`

**Returns**

The last message (usefull for chat applications efficiency).