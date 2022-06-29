# Basic definitions
> The article contains important terms for understanding the system.

## Node
***Node*** is server that runs [evade84-node](https://github.com/evade84/evade84-node) instance.
Anyone in the world can run evade84 node (even you, little pickle)!

> Every node has ***name***. Node owner may call his or her node as he likes.

## Pool
***Pool*** is something like chat-room or chat in Telegram. It contains messages sent by users.

Every pool has a unique ***address*** 
(which is literally a hex value of pools [uuid4](https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_(random))). 

Also, pool may optionally have a ***tag***. It is a unique readable identifier (e.g. `my-blog123`). 
It can be used to link any specific pool as well as pool *address*.

> Pool *tag* and pool *address* are called ***pool identifier***. 

### Pool metadata
Pool may have some metadata:

* ***Description*** (optional, mutable) - description of pool 
* ***Creator signature*** (optional immutable) - [signature](#signature) of the pool creator
* ***Creation date*** (required, immutable) - date of pool creation
* ***Encryption info*** (required, immutable) - information about pool encryption
* ***Publicity*** (required, immutable) - information about pool publicity

### Pool types
Pool must be one of the following types:

| Type          | Who can write messages | Who can read messages | Who can manage pool | AES Encryption |
|---------------|------------------------|-----------------------|---------------------|----------------|
| ***wall***    | anyone                 | anyone                | *master-key* owner  | no             |
| ***chat***    | *writer-key* owner     | *reader-key* owner    | *master-key* owner  | optional       |
| ***channel*** | *writer-key* owner     | anyone                | *master-key* owner  | no             |
| ***mailbox*** | anyone                 | *reader-key* owner    | *master-key* owner  | no             |

* ***wall*** is like a real wall - anyone can read from it and write anything on it!
![wall](https://i.pinimg.com/originals/8b/5a/ec/8b5aec28a13eaf85248b54a45ca9b9d1.jpg)
* ***chat*** is like a private dialog - only participants have access to it. It also may be encrypted!
![chat](https://pbs.twimg.com/media/BJVaTIrCUAAaPkp.jpg)
* ***channel*** is like a TV, Telegram or YouTube channel - anyone can read and watch it, but only a few people with access can provide content!
![channel](http://flowjournal.org/wp-content/uploads/2009/09/hdtv.png)
* ***mailbox*** is like a real mailbox (I mean box with a small hole for letters and lock on it) - anyone can throw letter into it, only key owners are able to open it and read messages!
![mailbox](https://media.tenor.com/images/dad345322abaecc84f726fe844441984/raw)

### Pool access keys
Access to pool is managed via ***access keys***.
There are three different types of them:

* ***master-key*** is present in pools of any type. It provides access to editing (including keys) and deleting pool.
* ***writer-key*** provides access to writing messages in pools. 
* ***reader-key*** provides access to reading messages in pools.

> Pool, depending on its [type](#pool-types) has *writer-key* and/or *reader-key*. But it always has a *master-key*.

## Message
***Message*** is... well... a message! Pools contains list of messages.
Messages may optionally have authors [signature](#signature) and may be optionally encrypted using 
[AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard). Every message has ***id*** - serial number
of the message in specific pool.

## Signature
***Signature*** is used to authorize users. It is something that proves, that action was performed by the specific user.
Anyone can create as many signatures as needed. Moreover, signature is optional, you may stay fully anonymous if you wish!

![signature](https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/Alan_Turing_signature.svg/1280px-Alan_Turing_signature.svg.png)

*Signature* has ***value*** - name or pseudonym (may be not unique) and ***uuid*** - unique identifier.


> *Pool identifier* and *signature identifier* are different things. 
*Pool identifier* means *pool tag* or *pool address*, when *signature identifier* means certain string which is unique and used to identify signature.

### Signature metadata
Signatures also have some metadata:

* ***Description*** (optional, mutable) - description of signature.
* ***Creation date*** (required, immutable) - date when signature was created.

### Signature access key
Signature access is managed using **signature access key**.
Anyone who owns this key is able to sign his/her messages or created pools with specific signature; edit signature description.

### Deleting signature
Signature cannot be deleted.
