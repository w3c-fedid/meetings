# FedID WG/CG Telecon, 2026-06-30

* Moderators:  Heather Flanagan

* Scribe: Phil

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
* Ecosystem Updates (10 minutes)  
* Discussion (40 minutes)  
  * [FedCM facilitates vendor lock-in \#827](https://github.com/w3c-fedid/FedCM/issues/827)  
  * [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)  
* Any Other Business (AOB)

# Notes

## Administrivia

* W3C Code of Conduct  
* Service Worker and .well-known on the agenda.

## Ecosystem Updates (10 minutes)

* Heather:  
  * Any updates?  
  * Nothing

## Discussion (40 minutes)

### [FedCM facilitates vendor lock-in \#827](https://github.com/w3c-fedid/FedCM/issues/827)

* Heather:  
  * Any updates on what is happening with Well-Known?  
  * Might need Will (Bartlett) for this one  
  * Also on the face-to-face agenda in September  
  * Want to make it easier to handle cross-site relationships.  
* Suresh:  
  * Will is waiting for a resolution and an update to issue 827 ([https://github.com/w3c-fedid/FedCM/issues/827](https://github.com/w3c-fedid/FedCM/issues/827)), and it can be discussed there.  
* Heather:  
  * From previous meetings, Will and Sam are to have a side conversation?  
* Suresh:  
  * Nicolas, what is your opinion on 827?  
* Nicolás:  
  * Need to fully understand the problem first. (PS. so needs Will.)  
* Heather:  
  * Need paths to get to more information, but can not be at the top-level.   
  * Putting IdP information at the top-level origin does not work well for a lot of cases. Can we agree where we put that if not on the top level?  
* Nicolás:  
  * Maybe 8 different issue?  
  * This is some kind of ramp-up deployment of FedCM.  
  * 827 is about changing IdP providers.  
  * Suresh, can you represent Will?  
* Suresh:  
  * I’ll try to summarise (827) and share with the group.  


### [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)

* Heather:  
  * Suresh, can you give an update?  
* Suresh:  
  * We are done with the discussions.  
  * Work on a prototype with MS.  
  * Reached out to Chromium folk on the Service Worker (SW) side.  
* Heather:  
  * Waiting for experience?  
* Suresh:  
  * Waiting for review  
  * Was some update in the last meeting about using SW.  
* Nicolás:  
  * How to isolate SW.  
* Suresh:  
  * Going to use Nonce.  
  * Some challenges, so Nonce is a simple way.  
* Nicolás:  
  * Not familiar with SW Nonce.  
* Suresh:  
  * Is for isolation.  
  * How are you going to handle SW isolation from IdP or FedCM managed.  
    * Two approaches:  
      * Nonce  
      * Storage key  
    * Nonce can be better handled for implementation's sake. Nonce is already in the Storage Key, so better for isolation.  
* Nicolás:  
  * What is Nonce?  
* Suresh:  
  * A kind of token, which is being used as a field for doing SW restriction from FedCM point of view.   
  * Is a member of the storage key.  
* Nicolas  
  * Does that change?  
* Suresh  
  * For a given IdP origin, we create a Nonce and pass it on to SW restriction which creates a storage key, and it creates a partition for the IdP origin. So if the user hits the IdP, it creates the same storage key based on the nonce.  
* Nicolás:  
  * So this is not the authentication nonce in the RP.  
* Suresh:  
  * No. Is different.  
  * (Suresh will share the design doc)  
* Nicolás:  
  * Any open questions?  
* Suresh:  
  * None that have not been answered.  
* Nicolás:  
  * Did you confirm that Microsoft IDP is OK with the approach?  
* Suresh  
  * Had a formal discussion with Microsoft IdP.  
  * <https://github.com/w3c-fedid/identity-handler/blob/main/identity-handler-explainer.md>

## 

## Any Other Business (AOB)

* Heather:  
  * CR targeted at Feb 2027\.  
  * First, we need to resolve all open issues.  
    * Do not need to *do* all the things, but need to *respond* to all the things.  
* Nicolás:  
  * Do we need to ship everything?  
* Heather:  
  * There was a concept of Core FedCM baseline, but Sam was not sure how we would define core without some of the people involved.  
  * FedCM is a big API, but it needs other browser engines to implement it.  
  * So we need to define what is in and out of scope. Defining Core has stalled.  
* Nicolás:  
  * Tricky (PS. to get other browser support)  
  * What would they like?  
* Heather:  
  * IdP registration was a Core feature?  
* Nicolás:  
  * Emelia was interested in that.  
  * Registration is a nice-to-have in CR.  
  * Suggested looking at the UX, but they (PS. not sure who ‘they’ are in this context) were not happy with that suggestion.  
* Heather:  
  * Well-Known changes, I think, should be in core as well.  
* Nicolás  
  * 827: I need to understand better, but Well-Known changes should get into core.  
* Heather:  
  * Nicolás, can you help understand what needs to be in the CR (from the issues).  
  * So might not be Feb 2027, still need to get through these issues.  
* Nicolás:  
  * Should we have new labels for this?  
* Heather:  
  * Labels for v2.  
  * Labels for ‘not going to do’.  
  * And then close what is possible.  
* Yi:  
  * Email verification in Chrome. Origin trials.

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Phil Smart (Shibboleth/Jisc)  
* Isaiah Inuwa (Bitwarden)  
* George Fletcher (independent)  
* [Nicolás Peña Moreno](mailto:npm@google.com) (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Yi Gu (Google Chrome)

