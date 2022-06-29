# Basic definitions
> The article contains important terms for understanding the system.

## Node
***Node*** is server that runs [evade84-node](https://github.com/evade84/evade84-node) instance.
Anyone is able to run node!

## Pool
***Pool*** is something like chat-room or chat in Telegram. It contains messages sent by users.

Every pool has a unique ***address*** (which is literally a hex value of pools [uuid4](https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_(random))). 

Also pool may optionally have a ***tag***. It is a unique readable identifier (e.g. `my-blog123`). 
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

* ***wall*** is like real wall - anyone can read from it and write anything on it!
* ***chat*** is like private dialog - only participants have access to it. It also may be encrypted!
* ***channel*** is like channel in Telegram or YouTube - anyone can get information from it, but only few people with access are able to write!
* ***mailbox*** is like real mailbox (I mean box with a small hole for letters and lock on it) - anyone can throw letter into it, only key owners are able to open it and read messages! 

### Pool access keys
Access to pool is managed via ***access keys***.
There are three different types of them:

* ***master-key*** is present in pools of any type. It provides access to:
* * Editing pool metadata
* * Editing *writer-key* and *master-key*
* * Deleting pool
* ***writer-key*** provides access to writing messages in pools which are *chat* or *channel*.
* ***reader-key*** provides access to reading messages in pools which are *chat* or *mailbox*.

> Pool, depending on its type has *writer-key* and/or *reader-key*. But it always has a *master-key*.

## Signature
***Signature*** is used to authorize users. It is something that proves, that action was performed by the specific user.
Anyone can create as many signatures as needed. Moreover, signature is optional, you may stay fully anonymous if you wish!

*Signature* has ***value*** (your name or pseudonym) and ***uuid*** (unique identifier).

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
