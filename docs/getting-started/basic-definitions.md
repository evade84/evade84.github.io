# Basic definitions
> The article contains important terms for understanding the system.

## Pool
***Pool*** is something like chat-room or chat in Telegram. It contains messages sent by users.

Every pool has an unique ***address*** (which is literally a hex value of [uuid4](https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_(random))). 

Also pool may optionally have a ***tag***. It is an unique readable identifier (e.g. `my-blog123`). 
It can be used to link any specific pool as well as pool *address*.

> Pool *tag* and pool *address* are called ***pool identifier***. 

### Pool meta data
Pool also has some meta data (all fields are **optional**):

* ***Description*** (mutable) - description of pool 
* ***Creator signature*** (mutable) - *signature* of pool creator
* ***Creation date*** (immutable) - date of pool creation

### Pool types
Pool must be one of the following types:

| Type          | Who can write messages | Who can read messages | Who can manage pool  |
|---------------|------------------------|-----------------------|----------------------|
| ***wall***    | anyone                 | anyone                | *master-key* owner   |
| ***vault***   | *write-key* owner      | *read-key* owner      | *master-key* owner   |
| ***media***   | *write-key* owner      | anyone                | *master-key* owner   |
| ***box***     | anyone                 | *read-key* owner      | *master-key* owner   |

* ***wall*** is like real wall - anyone can read from it and write anything on it!
* ***vault*** is like real vault - it is safe and no passerby is able to break in it!
* ***channel*** is like real media - anyone can read it, but only few people with access are able to write!
* ***box*** is like real box (I mean box with a small hole for papers and lock on it) - anyone can throw paper in it, only key owners are able to open it and read content of papers! 

### Pool access keys
Access to pool is managed via *access keys*.
There are three different types of them:

* ***master-key*** is present in pools of any type. It provides access to:
* * Editing pool meta data
* * Editing *write-key* and *master-key*
* * Deleting pool
* ***write-key*** provides access to writing messages in pools which are *vault* or *channel*.
* ***read-key*** provides access to reading messages in pools which are *vault* or *box*.

> Pool, depending on its type has *write-key* and/or *read-key*. But it always has a *master-key*.

### Indexable and non-indexable pools
...

## Signature
***Signature*** is used to authorize users. It is something that proves, that action was performed by the specific user.
Anyone can create as many signatures as needed. Moreover, signature is optional, you may stay fully anonymous if you wish!

*Signature* has ***name*** (must be unique) and ***identifier***.

> *Pool identifier* and *signature identifier* are different things. 
*Pool identifier* means *pool tag* or *pool address*, when *signature identifier* means certain string which is unique and used to identify signature.

### Signature meta data
Signatures have meta data (all fields are **optional**):

* ***Description*** (mutable) - description of signature.
* ***Creation date*** (immutable) - date when signature was created.

### Signature access key
Signature access is managed using **signature access key**.
Anyone who owns this key is able to sign his/her messages or created pools with specific signature; edit signature description.

### Deleting signature
Signature cannot be deleted.

