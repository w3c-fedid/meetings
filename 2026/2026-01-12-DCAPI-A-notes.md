# FedID WG Telecon — DC API Series A, 2026-01-12

* Moderators: Heather

* Scribe: Matthew Miller

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)? [Matthew Miller](mailto:mattmil3@cisco.com)  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (40 minutes)  
  * [Canonical test objects for OpenID4VP and Openid4VCI \#433](https://github.com/w3c-fedid/digital-credentials/issues/433)  
  * [Define "complete credential request with error" \#421](https://github.com/w3c-fedid/digital-credentials/pull/421)  
  * [Introduce "active promise" concept for request coordinator. \#417](https://github.com/w3c-fedid/digital-credentials/pull/417)  
  * [Registry PR](https://github.com/w3c-fedid/digital-credentials/pull/401)  
  * [Security Considerations PRs](https://github.com/w3c-fedid/digital-credentials/pulls?q=is%3Apr+is%3Aopen+label%3Asecurity-considerations)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (10 minutes)

* Lee: California DMV implemented DC API

## DC API Issues & PRs

### [Canonical test objects for OpenID4VP and Openid4VCI \#433](https://github.com/w3c-fedid/digital-credentials/issues/433)

Tim: Already in the relevant specs, just need to add them to DC API spec.

### [Define "complete credential request with error" \#421](https://github.com/w3c-fedid/digital-credentials/pull/421)

Heather: Nothing else to discuss here, it has all the approvals it needs.

### [Introduce "active promise" concept for request coordinator. \#417](https://github.com/w3c-fedid/digital-credentials/pull/417)

Matt: Seems a bit too implementation-specific to include in the spec.  
Mohamed: Adds more color to the responsibility of the coordinator. Problem is, user agents get promises from CredMan spec but it’s unclear what to do with it. For clarity, it makes sense to put it into the DC API.

### [Registry PR](https://github.com/w3c-fedid/digital-credentials/pull/401)

Tim: Currently called “supported protocols.” This appears to be controversial to some, so let’s ask the group.  
Christian: For implementations of this protocol, they should support all of these protocols.  
Tim:   
Lee: “As a browser implementer, this is what you should support.”  
Heather: As an observation, talking to people in the EU the biggest source of confusion is the question of who’s implementing what. It's important to clarify this to answer that question. Coming back to “how do we name the thing,” “supported protocols” seems important.  
Tim: This spec is about the web layer.  
Mohamed: The main purpose of listing the protocols is to evaluate the security properties of the API. Whatever we call it here, we can tweak it later.  
Heather: Are we in agreement that “supported protocols” is fine?  
Tim: As long as it’s not “permitted” or “allowed.”  
Mohamed: My concern about “supported” is that the API is defined to be a dumb pipe. “Supported” implies the API does something more to support requests.  
Wendy: Sounds like we’re not going to reach consensus here today. Maybe we can raise the specific question of wording async, see if “recognized” or other less opinionated words might help us.  
Lee: Is the only problem here that Safari doesn’t want to implement everything?  
Heather: To Mohamed’s point, there’s more issues with “supported” than that.  
Lee: We’ve changed the API from being a dumb pipe to a fully-specced API, where the browser can do what they like with the request. “Supported,” then, is the right word. A separate issue is, do user agents have to support them all?  
Mohamed: I take Lee’s point. So now I’m less concerned about “supported.”  
Heather: Hearing more consensus about “supported.” We will go ahead and put a link to this discussion in the notes and see if we can’t get a broader consensus.  
Heather: Aside from naming, what else can we discuss?  
Mohamed: Did we get consensus on the enum?  
Tim: Sounds like he’s not opposed to it? ([GitHub comment](https://github.com/w3c-fedid/digital-credentials/pull/401#discussion_r2681068647)) Also fine with separating presentation and issuance enums.  
Heather: If you haven’t looked at this PR then please do. It’s one of the more important PRs. Feedback is greatly appreciated.  
Tim: 

### [Security Considerations PRs](https://github.com/w3c-fedid/digital-credentials/pulls?q=is%3Apr+is%3Aopen+label%3Asecurity-considerations)

Heather: I encourage you all to take a look at all of them. We will be going over them in the next few weeks.  
Simone: The general idea is that we should start from [Issue 424](https://github.com/w3c-fedid/digital-credentials/pull/424). The Security Considerations section is non-normative, but of course we can discuss which bits can be made normative. Sections have been defined for “in-scope” and “out-of-scope” threats or attacks, security properties and threat responses, assumptions, DoS considerations, residual threats, misuse, and applicability.  
Heather: Structure seems like a great place to start.  
Simone: We’re not trying to reinvent the wheel, e.g. [Issue 426](https://github.com/w3c-fedid/digital-credentials/pull/426) adds references to Secure Context to threat modeling.  
Matthew: This seems like a great structure. Is there any prioritization of issues to help determine review order?  
Simone: For starters, help contribute to the [Security Considerations Google Doc](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.dilz864boly).  
Mohamed: We’ve been working in that Google Doc, but it’s hard to add all of it in a single PR. Structure PR (424) is the most important one. Then Security Context (426) is the next most important one.  
Mohamed: What do we think about respecting the “Draft” status of PRs, then removing the status when it’s ready for review?  
Matt: Great idea.

# AOB

* . 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* George Fletcher (Practical Identity, LLC)  
* Christian Bormann (SPRIND)  
* Tim Cappalli (Okta)  
* Mohamed Amir Yosef (Google Chrome)  
* Simone Onofri (W3C)  
* Wendy Seltzer  
* Matthew Miller (Cisco)  
* Bjorn Hjelm (Yubico)  
* Luke Dary (Red Hat/IBM)  
* Brian Campbell  
* David Waite  
* Amir Sharif  
* Isaiah Inuwa  
* Michael Jones