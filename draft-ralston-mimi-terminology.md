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
 - next generation
 - unicorn
 - sparkling distributed ledger
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

This document expands upon MLS's [!I-D.ietf-mls-protocol] [!I-D.ietf-mls-architecture]
terminology by defining terms specific to MIMI's purpose. Document authors SHOULD prefix
terms from the MLS specification with "MLS" to denote that the term is specifically coming
from the MLS specification. For example, "MLS Group" versus "Group". This document defines
terms which are non-conflicting to help ensure clarity when the MLS prefix is missing, however.

Documents within the MIMI working group may introduce their own terminology to explain
concepts within their context. Those documents SHOULD NOT override or change the terminology
described in this document or from MLS.

# Terminology

MIMI defines:

**User**: A (normally) human operator of a *client*. *Users* have a **User ID** to identify
them canonically within the system.

**Client**: A user interface for messaging, performing encryption as needed. Presents
*rooms* to the *user* to interact with. Synonymous with *MLS Client*. *Clients* have a
**Client ID** to canonically identify them among a *user's* other *clients*.

**Room**: The place where *users* communicate. Depending on design, this may be synonymous
with an *MLS Group*. The default assumption if not clarified is that the *room* and *group*
are different concepts/entities. *Rooms* have a **Room ID** to canonically identify them
within the system, which may be a **Group ID** if the concepts are synonymous.

**Room Member**: A *user's* membership in relation to a *room*. If the concepts of *room* and
*MLS Group* are synonymous, this will be no different than an *MLS Member*, however if different
then this will be which represents the *MLS Member* to the *room*.

**Event**: The container for an encrypted *MLS Message*, sent over the wire between *servers*
and *clients* (through their local *servers*). *Events* have an **Event ID** to canonically
identify them at least within the *room*.

**Room Property**: Information stored in the *room*, such as the name, topic, avatar,
*room membership*, etc. This may be in the shape of an *event*. Note that *room properties* are
different from what is needed to construct an *MLS Group Context*.

**Message**: Synonymous with an *MLS Message*. *Messages* have a **Message ID** to canonically
identify them at least within the *group*.

**Server**: Synonymous with an *MLS Delivery Service (DS)*. Responsible for routing *events*
to other *servers* and local *clients*. Note that the role of a *server* can be accomplished
in the same logical place as a *client* (i.e.: in peer-to-peer environments), however the
default assumption if not clarified is that the *client* and *server* are two different
entities.

**Client-Server API**: The interface between a *client* and *server*. This may be nothing more
than a function call if the *client* and *server* are the same logical entity.

**Server-Server API**: The interface between a *server* and another *server*.

**Transport**: The method and format for moving information between entities. For example,
a *Client-Server API* might describe HTTPS and JSON as its *transport*. For added clarity,
documents should clarify which API surface they are defining a *transport* for ("Server-Server
Transport", for example).

**Access Control**: The set of algorithms which determine whether an *event* or *MLS Message*
is permitted in the *room*/*group*. For instance, this may define whether an *MLS Proposal*
is accepted or whether the *user* is able to become a *room member*.

**Message Format**: The specific format that *clients* use within the encrypted body of an
*MLS Message*. Sometimes this will also be called the **Content Format**.

**User Identity**: A mapping of **User ID** to external identifier, such as a phone number.
In some cases, the *user identity* can be synonymous with the *user ID*, however the default
assumption if not clarified is that they are different concepts.

**Messaging Provider** or **Provider**: A service offering instant messaging to *users*.
Typically a *provider* will have a *server* to route *events* between *users* (or *clients*,
specifically).

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

In this figure, Client 1 is directly connected to Provider 1 over channel `A`. `A` is a
provider-specific Client-Server API and transport. Similarly, Client 2 is directly
connected to Provider 2 over channel `C`. `C` is also a provider-specific Client-Server API
and transport.

Provider 1 and 2 talk to each other with a Server-Server API over a transport. This is `B`
in the figure.

Clients additionally have an implicit channel (`D` in the figure) where they use a shared
Message Format. There is no transport for `D` in this figure: the figure is denoting that
servers/providers are unable to assist with a format conversion due to the event's content
(an MLS message) being encrypted.

# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO: Acknowledgments
