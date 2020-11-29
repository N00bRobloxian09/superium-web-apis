# superium-web-apis

im sorry for my english, lol

| Domain | Description |
| -: | :- |
| [api.superium.net](https://api.superium.net/docs) | Misc Endpoints |

Undocumented APIs
=================
* [User APIs](#user-apis)
* [Avatar APIs](#avatar-apis)
* [Friendship APIs](#friendship-apis)
* [Guild APIs](#guild-apis)
* [Item APIs](#item-apis)
* [Auth APIs](#auth-apis)

User APIs
---------
#### Sends an verification email
* https://superium.net/api/send_verification_email?ReturnUrl=/[page_name]
> ReturnUrl: a page to redirect to after sending the request

#### Switches between the dark/light theme
* https://superium.net/api/ToggleDarkTheme
    ```json
    light/dark
    ```
    
#### Currency Conversion Calculator
* https://superium.net/api/calculateconversion?input=[number]&c=[type]
> input: an amount of bricks/studs

> c: b, s (b means bricks) (s means studs)
```json
    returns a number
```

#### Currency Conversion
* https://superium.net/api/StudToBrick
> studInput: a number of studs to convert
* https://superium.net/api/BrickToStud
> brickInput: a number of bricks to convert


#### Fetch a trade
* https://superium.net/api/fetch/trade?id=[tradeId]
> tradeId = a target trade id (example with a id 5437)

```json
  {"id":"5437","user_from":"5669","user_to":"451","f1":"50153","f2":"34282","f3":"0","f4":"0","t1":"50110","t2":"0","t3":"0","t4":"0","seen":"0","status":"PENDING","f1name":"Pumpking Top-Hat ","f1id":"5548","f1serial":"61","f1worth":"372","f2name":"The Fire Crown","f2id":"3875","f2serial":"10","f2worth":"5,861","f3name":"","f3id":0,"f3serial":0,"f3worth":0,"f4name":"","f4id":0,"f4serial":0,"f4worth":0,"t1name":"Pumpking Top-Hat ","t1id":"5548","t1serial":"48","t1worth":"372","t2name":"","t2id":0,"t2serial":0,"t2worth":0,"t3name":"","t3id":0,"t3serial":0,"t3worth":0,"t4name":"","t4id":0,"t4serial":0,"t4worth":0}
```

##### Errors
1. Not logged in: {'error': true }
2. Not allowed to fetch the trade: {'error': true }

#### Trade action
* https://superium.net/api/TradeAction
> id: a target trade id

> action: an action (accept, decline)

##### Errors
1. Not logged in: {'error': true }
2. Not allowed to interact with the trade: {'error': true }

#### Log out
* https://superium.net/Login/Expire


Avatar APIs
---------

#### Set body part color
* https://superium.net/api/SetPartColor?color=[id]&part=[part]
> id: a color id 

> part: part=currentlySelected (which is Head), part=(body part name)

#### Take off an item
* https://superium.net/api/TakeOff
> id: item id (you need to own it)

#### Wear an item
* https://superium.net/api/Wear
> id: item id (you need to own it)

#### Fetch inventory
* https://superium.net/api/fetch/wardrobe?cat=[inventoryType]&page=[page]
> cat: tool, hat, face, shirt, pants

> page: a page id

#### Load worn items 
* https://superium.net/api/fetch/wearing

#### Render avatar
* https://superium.net/api/renderAvatar


Friendship APIs
---------

#### Send a Friend Request
* https://superium.net/api/AddFriend
> id: a target user id

> csrf: your csrf token

#### Unfriend a user (Target needs to be your friend)
* https://superium.net/api/RemoveFriend?id=[userId]
> id: a target user id

#### Block a user
* https://superium.net/api/block?id=[userId]
> userId: a user id, for example ?id=1

#### Fetch all friend requests
* https://superium.net/api/fetch/friendrequests?page=[pageId]
> pageId: a page id, or ?page=currentPage, Warning: the max page is 100

#### Accept all friend requests
* https://superium.net/api/AcceptAll

##### Errors
1. Not logged in: You are not logged in!

#### Decline all friend requests
* https://superium.net/api/RemoveAll

##### Errors
1. Not logged in: You are not logged in!

Guild APIs
---------

#### Get members
* https://superium.net/api/fetch/guildmembers?gid=[guildId]&role=[role]&page=[page]
> guildId: a guild id

> role: a role name (can get the id thru F12, and searching for data-roleid)

> page: a page id, currentPage

```html
<div class="columns">
  <!-- this thing below repeats (10 members = 10 divs) -->
<div class='column is-2'>
  <img src='https://superium.net/assets/thumbnails/avatars/[avatarhash].png'>
  <center><a href='/User/?id=[userId]'>[username]</a></center>
</div>
  
</div>
```

#### Get Store Items
* https://superium.net/api/fetch/guildstore?gid=[guildId]&page=[page]
> guildId: a guild id

> page: a page id, currentPage

```html
returns the same thing like get members but it's not users it's items
```

#### Join a guild
* https://superium.net/api/JoinGuild?id=[guildId]
> guildId: a guild id

#### Leave a guild
* https://superium.net/api/LeaveGuild?id=[guildId]
> guildId: a guild id

#### 
* https://superium.net
> 
> 

Game APIs
---------

#### Join a game
* https://superium.net/api/JoinBeta?id=[gameId]
> gameId: a game id

Item APIs
---------

#### Sell an Limited
* https://superium.net/api/doSellLimited
> serial: your serial id

> itemid: limited id

> price: chosen price in bricks (max 1000000000, min 1)

##### Errors
1. Logged-in user doesnt own the item, returns: err:inv

#### Purchase an item
* https://superium.net/api/PurchaseItem
> id: item id

> csrf: your csrf token

##### Errors
1. invalid assetId
2. invalid item
3. already own this item
4. not logged in
5. item is off-sale
6. not having enough currency
7. item has sold out

#### Purcahse an limited (requires blim)
* https://superium.net/api/PurchaseCollectible
> id: blim

> blim = code below
```js
var blim = [itemid];
```

> csrf: your csrf token

##### Errors
1. invalid assetId
2. invalid item
3. already own this item
4. not logged in
5. item is off-sale
6. not having enough currency
7. selling this item

#### Purcahse an limited with id
* https://superium.net/api/PurchaseCollectible
> id: item id

> csrf: your csrf token

##### Errors
1. invalid assetId
2. invalid item
3. already own this item
4. not logged in
5. item is off-sale
6. not having enough currency
7. selling this item

Auth APIs
---------

#### Check if a name is taken
* https://superium.net/api/NameAvailability?name=[name]
> name: a chosen name lol?

```json
{"Error": false,"Message": "OK"}
```

##### Errors
1. username must be at least 3 characters
2. inappropriate username
3. username contains special characters
4. username is already taken! Try [name](random numbers like "XYZ237") instead

#### Register a new account
* https://superium.net/api/finishregistration
> username: chosen username

> password: chosen passowrd

> confirmpassword: your chosen password

> email: chosen email

> referer: target userId (REFERER IS OPTIONAL), default 0

```json
unknown
```

##### Errors
1. reCAPTCHA failed, please try again
2. other errors are unknown, sadly
