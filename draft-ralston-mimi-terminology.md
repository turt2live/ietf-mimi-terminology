---
title: "MIMI Terminology"
abbrev: "MIMI Terminology"
category: info

docname: draft-ralston-mimi-terminology-latest
submissiontype: IETF  # also: "independent", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Applications and Real-Time"
workgroup: "More Instant Messaging Interoperability"
keyword:
 - mimi terminology
 - mimi definitions
 - mimi words
venue:
  group: "More Instant Messaging Interoperability"
  type: "Working Group"
  mail: "mimi@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/mimi/"
  github: "turt2live/ietf-mimi-terminology"
  latest: "https://turt2live.github.io/ietf-mimi-terminology/draft-ralston-mimi-terminology.html"

author:
 -
    fullname: Travis Ralston
    organization: The Matrix.org Foundation C.I.C.
    email: travisr@matrix.org

normative:

informative:


--- abstract

This document introduces a set of terminology to use when discussing or describing
concepts within MIMI.

--- middle

# Introduction

The More Instant Messaging Interoperability (MIMI) working group is chartered to
specify the minimal set of mechanisms to make modern instant messaging applications
interoperable. Through prior discussions and upcoming documents, it's become important
to have a shared understanding for what is being discussed specifically.

This document expands upon MLS's {{!I-D.ietf-mls-protocol}} {{!I-D.ietf-mls-architecture}}
terminology by defining terms specific to MIMI's purpose. Document authors SHOULD prefix
terms from MLS with "MLS" to denote where the term is specifically coming from. For example,
"MLS Group" versus "Group". This document defines terms which are non-conflicting to help
ensure clarity when the MLS prefix is missing, however.

Documents within the MIMI working group may introduce their own terminology to explain
concepts within their context. Those documents SHOULD NOT override or change the terminology
described in this document or from MLS.

# Terminology

**TODO(TR): How much of this is replaced by {{?I-D.barnes-mimi-arch}}?**

MIMI defines:

**Messaging Provider** or **Provider**: A service offering instant messaging to users.
Each provider has a server to route events between users (or clients, specifically).

**User**: A (normally) human operator of a client. Users have a **User ID** to identify
them canonically within the system.

**User Identity**: A mapping of **User ID** to external identifier, such as a phone number.
In some cases, the user identity can be synonymous with the user ID, however the default
assumption if not clarified is that they are different concepts.

**Client**: A user interface for messaging, performing encryption as needed. Presents
rooms to the user to interact with. Synonymous with MLS Client. Clients have a
**Client ID** to canonically identify them among a user's other clients. Clients
can additionally be called **Devices** to differentiate them from a named application.

**Room**: The place where users communicate. This is semantically distinct from an
MLS Group: an MLS Group is responsible for handling client keys while a room is
simply the user-facing construct for communication, however systems can declare a Room
to be the same as an MLS Group depending on their design. Rooms have a **Room ID** to
canonically identify them within the system. Rooms can additionally be called **Chats**,
**Conversations**, and **Channels**.

A room can have any one of many different characterizations/behaviours, called **Room Types**:

* **DM**: A direct message room between exactly two users. DMs are typically created
  when a user searches for another user to message, rather than creating a group Room.
  All users in the room have the same permission capabilities under the access control
  semantics. The room name is that of the other user in the DM. DMs are typically
  canonical: exactly one Room with the other user exists at a time.

* **Group DM**: A subtype of DMs where there are more than two users. The room name
  consists of the other users in the DM. Inherited from DMs, Group DMs are also
  canonical: creating a new Group DM with the exact same users ultimately redirects to
  the existing room instead of creating a new one. These may also be called **Ad-hoc Rooms**
  in some scenarios.

* **Group Chat**: A room which requires an invite to be able to participate, and can have
  zero or more users. A user-provided room name is defined for the room. Typically,
  the creator has admin permissions while other designated users have either admin permissions
  or moderator permissions. Most users have default permissions which allow them to send
  events to the room. Unlike (Group) DMs, multiple rooms with the same set of users
  can exist at the same time, even with the same room name.

* **Public Room**: A group chat which does not require an invite to participate. Usually
  these types of rooms are discovered through a directory or website. Rooms which require
  a request to join, or knock, are considered public rooms. Sometimes these will be referred
  to as **Public Chatrooms**.

* **Auditorium Room**: Either a group chat or public room where most users are unable to
  send events and cannot be seen as room participants by other users. When an event is sent,
  it may appear to be sent by the room itself rather than the specific user who sent it.
  Sometimes these are called **Auditorium Chats**.

Depending on the system, a room's type can be mutable. For example, a user may be permitted
to introduce new users to a group DM to implicitly convert it to a group room, or they
simply may be unable to implicitly or explicity change the room type.

**Room Name**: The title or human-focused textually distinguishing factor for the room. It
may be automatically generated based on the room participants.

**Room Avatar**: A picture or graphic associated with the room, usually in combination with
a room name. Room avatars can be automatically generated based on the room participants.

**Room Participant**: A joined user in the room. Note that this may have implications on the
associated MLS Members in the MLS Group for the user's devices.


**Event**: The container for an encrypted MLS Message, sent over the wire between servers
and clients (through their local servers). Events have an **Event ID** to canonically
identify them at least within the room.

**Room Property**: Information stored in the room, such as the name, topic, avatar, room participants,
etc. This may be in the shape of an event. Note that room properties are different from
what is needed to construct an MLS Group Context.

**Message**: Synonymous with an MLS Message. Messages have a **Message ID** to canonically
identify them at least within the group. These are essentially what a user would call a
"message", though specifically the unencrypted portion. When encrypted, they are called events.

**Server**: Responsible for routing events to other servers and local clients. The collection
of servers and clients in a room form the MLS Delivery Service (DS).

**Hub Server**: The specific server responsible for routing events to other servers in the
context of a room. Sometimes this is shortened to **Hub**.

**Owning Server**: If applicable, the server specifically responsible for applying access
control to a room. Typically, this will also be the hub server for the room. This should *not*
be shortened to "owner" to avoid confusion with other related concepts.

**Client-Server API**: The interface between a client and server. This may be nothing more
than a function call if the client and server are the same logical entity.

**Server-Server API**: The interface between a server and another server.

**Transport**: The method and format for moving information between entities. For example,
a Client-Server API might describe HTTPS and JSON as its transport. For added clarity,
documents should clarify which API surface they are defining a transport for ("Server-Server
Transport", for example). MIMI is not chartered to define the Client-Server Transport.

**Message Format**: The specific format that clients use within the encrypted body of an
MLS Message. Sometimes this will also be called the **Content Format**.

**Access Control**: The set of algorithms which determine whether an event or MLS Message
is permitted in the room/group. For instance, this may define whether an MLS Proposal
is accepted or whether the user is able to become a room participant.

**Admin Permissions**: Typically at least the user who created the room, these permissions
grant the associated users an ability to change the permissions of other users in the room.
The set of users with these permissions in a room are called **Admins**. Admin permissions
typically inherit moderator permissions.

**Moderator Permissions**: These permissions grant the associated users an ability to kick,
ban, or otherwise restrict another user's ability to use the room. For example, deleting
a spammer's events. The set of users with these permissions in a room are called **Moderators**.

Note that with both moderator permissions and admin permissions a system may have finer
granularity, such as a set of users being able to kick but not ban. Documents with these
semantics should clarify this case.

**Invite**: An action taken by a user in a room to encourage another user to become a
room participant (or joined to the room). This can be explicit through the server-server API,
or implicit with an join link/join code.

**Join Link**: A machine-readable mechanism for a user to join the room, represented as a URL
or QR code.

**Join Code** or **Join Password**: A text-based string a user may enter to join a room.
The string may be shared with the user verbatim or encoded with a QR code, for example.

**Direct Invite**: An invite to a DM or Group DM. These invites might appear in a different
section of the client's UI to denote their semantic difference from a non-DM invite.

**Kick**: An action taken by a user to remove another user from a room, assuming the sender
has moderator permissions. The affected user can re-join the room with either another invite
or by simply joining, depending on the room type.

**Ban**: Similar to kicking, a user is kicked from the room and not allowed to re-join
until unbanned by a moderator. If a user is banned, they are typically not able to
knock to get back into the room either.

**Knock**: A request from a user (who is not currently a room participant) to join the
room. Upon acceptance, the requesting user may receive an invite or be directly joined to
the room. Upon rejection, the requesting user can be banned or otherwise declined.

**Status**: Temporarily displayed text or images associated with a user's profile. Instagram
Stories are an example of a user's status.

## Diagram Reference

In the simplest possible form, interoperable messaging between two end users looks as such:

~~~ aasvg
+----------+       +------------+       +------------+       +----------+
|          |   A   |            |   B   |            |   C   |          |
| Client 1 |<----->| Provider 1 |<----->| Provider 2 |<----->| Client 2 |
|          |       |            |       |            |       |          |
+----------+       +------------+       +------------+       +----------+
     ^                                                             ^
     |                              D                              |
     +-------------------------------------------------------------+
~~~
{: #fig-typical-arch title="Typical, simplified, architecture for interoperability"}

In this figure, Client 1 is directly connected to Provider 1 over `A`. `A` is a
provider-specific Client-Server API and transport. Similarly, Client 2 is directly
connected to Provider 2 over `C`. `C` is also a provider-specific Client-Server API
and transport.

Provider 1 and 2 talk to each other with a Server-Server API over a transport. This is `B`
in the figure.

Clients additionally have an implicit method of communication (`D` in the figure) where
they use a shared Message Format. There is no transport for `D` in this figure: the figure
is denoting that servers/providers are unable to assist with a format conversion due
to the event's content (an MLS message) being encrypted.

# IANA Considerations

This document has no IANA actions.


--- back
