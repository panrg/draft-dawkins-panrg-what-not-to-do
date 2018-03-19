---
title: "Path Aware Networking: A Bestiary of Roads Not Taken"
abbrev: What Not To Do
docname: draft-dawkins-panrg-what-not-to-do-latest
date: 
category: info

ipr: trust200902
area: IRTF
workgroup: PANRG
keyword: Fails
keyword: Networking
keyword: Aware
keyword: Path
keyword: PAN

stand_alone: yes
pi: 

author:
  -
    ins: S. Dawkins
    name: Spencer Dawkins
    organization: Huawei Technologies
    email: spencerdawkins.ietf@gmail.com
    role: editor

informative:

  RFC0793:
  
  RFC1633:
  
  RFC2475:

  RFC2581:
  
  RFC5533:
  
  RFC5974:
  
  RFC5681:
  
  RFC7418:

  NOTE_WELL:
    target: https://www.ietf.org/about/note-well.html
    title: IETF Note Well

  PANRG-99:
    target: https://datatracker.ietf.org/meeting/99/sessions/panrg
    title: "Path Aware Networking Research Group - IETF-99"
    date: July 2017

  PATH-Decade:
    target: https://datatracker.ietf.org/doc/slides-99-panrg-a-decade-of-path-awareness/
    title: "A Decade of Path Awareness"
    author:
      name: Olivier Bonaventure
      ins: O. Bonaventure
    date: July 2017

  PANRG:
    target: https://irtf.org/panrg
    title: "Path Aware Networking Research Group (Home Page)"
 
  TRIGTRAN-55:
    target: https://www.ietf.org/proceedings/55/239.htm 
    title: "Triggers for Transport BOF at IETF 55"
    date: July 2003
 
  TRIGTRAN-56:
    target: https://www.ietf.org/proceedings/56/251.htm 
    title: "Triggers for Transport BOF at IETF 56"
    date: November 2003
 
--- abstract

At the first meeting of the proposed Path Aware Networking Research Group, Oliver Bonaventure led a discussion of 
our mostly-unsuccessful attempts to exploit Path Awareness to achieve a variety of goals, over the past decade. 
At the end of that discussion,
the research group agreed to catalog and analyze these ideas, to extract lessons for network researchers.

This document contains that catalog and analysis.

--- middle
# Introduction

At IETF 99, the proposed Path Aware Networking Research Group {{PANRG}} held its first meeting {{PANRG-99}}, and the first presentation 
in that session was "A Decade of Path Awareness" {{PATH-Decade}}. At the end of this discussion, two things were 
abundantly clear. 

- The Internet community has accumulated considerable experience with many Path Awareness ideas over a long period 
of time, and

- Although some Path Awareness ideas have been successfully deployed (for example, Differentiated Services, or 
DiffServ {{RFC2475}}), most of these ideas haven't seen widespread adoption. The reasons for this non-adoption are many 
and varied.

The meta-lessons from this experience are

- Path Aware Networking is more Research than Engineering, so establishing an IRTF Research Group for Path Aware Networking 
is the right thing to do {{RFC7418}}, and

- Cataloging and analyzing our experience to learn the reasons for non-adoption 
is a great first step for the proposed Research Group.

This document contains that catalog and analysis. 

## About this Document

This document is not intended to include every idea about Path Aware Networking that we can find. 
Instead, we include enough ideas
to provide background for new lessons to guide researchers in their work, 
in order to add those lessons to Section 2.

There is no shame to having your idea included in this document. We were trying to engineer something that was research.
The document editor started with a subsection on his own idea. The only shame is not learning from experience, and not
sharing that experience with other networking researchers and engineers.

This document is being built collaboratively. To contribute your experience, please send a Github pull request to https://github.com/panrg/draft-dawkins-panrg-what-not-to-do.

Discussion of contributed experiences should take place on the PANRG mailing list.

# Summary of Lessons Learned

This section summarizes the Lessons Learned from the contributed sections in Section 4.

- The benefit of Path Awareness has to be great enough to overcome entropy for already-deployed devices. The colloquial 
American English expression, "If it ain't broke, don't fix it" is in full flower on today's Internet.

- If intermediate devices along the path can't be trusted, it's difficult to rely on intermediate devices to drive 
changes to behaviors.

- If operators can't charge for a Path Aware technology in order to recover the costs of deploying it, the benefits 
must be really significant.

# Template for Contributions

There are many things that could be said about the Path Aware networking technologies that have been developed. 
For the purposes of this document, contributors are requested to provide

- the name of a technology, including an abbreviation if one was used
- if available, a long-term pointer to the best reference describing the technology
- a short description of the problem the technology was intended to solve
- a short description of the reasons why the technology wasn't adopted
- a short statement of the lessons that researchers can learn from our experience with this technology.

# Contributions 

The editor has added some suggested subsections as a starting place, but others are solicited and welcome. 

## Integrated Services (IntServ) and follow-on Technologies (NSIS)

Write-up of Integrated Services (IntServ) {{RFC1633}} and follow-on Technologies (NSIS) {{RFC5974}}

Your description could be here.

## Triggers for Transport (TRIGTRAN)

TCP {{RFC0793}} has a well-known weakness - the end-to-end flow control mechanism has only a single signal, the loss of a segment, 
and semi-modern TCPs (since the late 1980s) have interpreted the loss of a segment as evidence that the path between two endpoints has
become congested enough to exhaust buffers on intermediate hops, so that the TCP sender should "back off" - reduce its
sending rate until it knows that its segments are now being delivered without loss {{RFC2581}}. More modern TCPs have added a growing
array of strategies about how to establish the sending rate {{RFC5681}}, but when a path is no longer operational, TCPs can
wait many seconds before retrying a segment, even if the path becomes operational while the sender is waiting to retry.

The thinking in Triggers for Transport was that if a path completely stopped working because its first-hop link was "down",
that somehow TCP could be signaled when the first-hop link returned to service, and the sending TCP could retry immediately,
without waiting for a full Retransmission Time Out (RTO). 

Two TRIGTRAN BOFs were held, at IETF 55 {{TRIGTRAN-55}} and IETF 56 {{TRIGTRAN-56}}, but this work was not chartered, 
and the reasons why provide several useful lessons for researchers.

- TRIGTRAN triggers are only provided when the first-hop link is "down", so TRIGTRAN triggers couldn't replace normal
TCP retransmission behavior if the path failed because some link further along the network path was "down". So TRIGTRAN
triggers added complexity to an already complex TCP state machine, and didn't allow any existing complexity to be removed.
- The state of the art in the early 2000s was that TRIGTRAN triggers were assumed to be unauthenticated, so they couldn't
be trusted to tell a sender to "speed up", only to "slow down". This reduced the benefit to implementers.
- intermediate forwarding devices required modification to provide TRIGTRAN triggers, but operators couldn't charge for
TRIGTRAN triggers, so there was no way to recover the cost of modifying, testing, and deploying updated intermediate 
devices.

## SHIM6

Write-up of SHIM6 {{RFC5533}}

Your description could be here.

# Security Considerations

This document describes ideas that were not adopted and widely deployed on the Internet, so it doesn't affect
the security of the Internet. 

If this document meets its goals, we may develop new ideas for Path Aware Networking that would affect the security of the
Internet, but those effects will be described in the corresponding RFCs for those ideas.

# IANA Considerations

This document makes no requests of IANA.

# Acknowledgements

The section on Triggers for Transport (TRIGTRAN) was provided by Spencer Dawkins.

Review comments were provided by (your name could be here).

--- back

