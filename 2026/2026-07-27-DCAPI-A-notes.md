# FedID WG Telecon — DC API Series A, 2026-07-27

* Moderators: Heather

* Scribe: Christian

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [WBS Vote](https://www.w3.org/wbs/154550/fediddcapienc/) on response encryption \- closes today  
* Ecosystem Updates (5 minutes)  
* https://www.w3.org/wbs/154550/fediddcapienc/DC API Issues & PRs (45 minutes)  
  * [Classify validation failures into specific exception types\#515](https://github.com/w3c-fedid/digital-credentials/pull/515)  
  * [Add document origin to request context\#512](https://github.com/w3c-fedid/digital-credentials/pull/512)  
  * [Mandate one presentation protocol MUST be supported\#454](https://github.com/w3c-fedid/digital-credentials/pull/454)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (10 minutes)

The vote deadline for response encryption is ending this evening, so please make sure to vote\! Brian asks about the methodology of counting the votes and Heather responds that it seems to mainly come down to the 2 core choices of normatively requiring response encryption or not.

## DC API Issues & PRs (45 minutes)

### [Classify validation failures into specific exception types\#515](https://github.com/w3c-fedid/digital-credentials/pull/515)

* Matthew comments that the broad buckets seem fine, but verifiers might be frustrated that there aren’t more granular errors, but the direction seems fine and we can still add errors later.  
* Heather asks for more reviews, otherwise after Tim’s review it will likely be merged after the next call.

### [Add document origin to request context\#512](https://github.com/w3c-fedid/digital-credentials/pull/512)

* Seems to be fixing a bug and Heather asks if anyone had the chance to look at it.

### [Mandate one presentation protocol MUST be supported\#454](https://github.com/w3c-fedid/digital-credentials/pull/454)

* Heather introduces that this PR states that one protocol must be supported but it doesn’t state which one.  
* Lee responds that in his perspective it should still say that all must be supported — at the very least, the browser should pass through all protocols. For the browser to only support a subset is bad for everyone and especially for developers.  
* Christian agrees that at least forwarding all protocols should be mandated.  
* Matthew responds that there is a PR by Tim ([https://github.com/w3c-fedid/digital-credentials/pull/474](https://github.com/w3c-fedid/digital-credentials/pull/474)) that seems to be related. The PR states that all cross-device requests must go to the platform (instead of all requests). There seems to be more to it than this one PR. This seems to have stalled since March/April and should be taken to a B-call with Marcos & Tim present.  
* Brian responds that 454 only says you must support one of the protocols and passing through (cross-device) is not part of it, so it should be reconciled with the other PR (\#474).  
* Matthew asks if we need to have another vote on this topic and proposes to state that cross-device requests go to platform and we might have to revisit later on and discuss the “all requests go to platform” perspective.

## Any Other Business (AOB)

* Simone mentions that ARF 3.0 was published.  
* Lee mentions that the Implementing Acts were published and the DC API is in it.  
* Christian adds that there are pretty strong requirements on DC API (mediating API) in the implementing acts, such as support for both protocols and both credential formats — look for mediating API in [https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1731](https://eur-lex.europa.eu/legal-content/EN/ALL/?uri=CELEX%3A32026R1731) 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Matthew Miller (Cisco)  
* Brian Campbell (Ping)  
* Christian Bormann (SPRIND)  
* Helen Qin (Google Android)  
* Lee Campbell (Google Android)  
* Ryan Watkins (Mastercard)  
* George Fletcher (Practical Identity LLC)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* René Léveillé (1Password)

