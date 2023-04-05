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
concepts within MIMI. It is neutral of any specific protocol or approach.

--- middle

# Introduction

The More Instant Messaging Interoperability (MIMI) working group is chartered to
specify the minimal set of mechanisms to make modern instant messaging applications
interoperable. Through prior discussions and upcoming documents, it's become important
to have a shared understanding for what is being discussed specifically.

This document aims to neutrally describe each part of an interoperable instant messaging
application. Note that some terminology comes from MIMI's use of MLS. [!I-D.ietf-mls-architecture]

Documents within the MIMI working group may introduce their own terminology to explain
concepts within their context. Those documents SHOULD NOT override or change the terminology
described in this document.

# Typical Architecture

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



# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO: Acknowledgments
