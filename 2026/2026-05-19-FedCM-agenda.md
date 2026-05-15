# FedID CG/WG Agenda - FedCM - 19 May 2026 

## Logistics

The FedID WG call will be held at 15:00 UTC.


* We are using Zoom for the meeting.
    * Please log in to see the [W3C FedID WG Events Calendar](https://www.w3.org/groups/wg/fedid/calendar/) for dial-in details. 
    * Participation is restricted to [FedID WG participants](https://www.w3.org/groups/wg/fedid/participants/) and [FedID CG participants](https://www.w3.org/groups/cg/fed-id/participants/).
* The link to the minutes document is in the W3C Calendar. 

## Agenda

* Administrivia
  * Scribe volunteer(s)?
  * Reminders: 
     * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)
     * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)
     * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)

* Ecosystem Updates (10 minutes)

* Discussion (40 minutes)
   * [Enabling IDP Interception in FedCM Request #815](https://github.com/w3c-fedid/FedCM/pull/815)
     * PR #815 proposes a mechanism that would allow Identity Providers to handle certain FedCM requests using a Service Worker-based mechanism. The motivating use cases include request signing / proof-of-possession patterns such as DPoP, operational failover, geographic or jurisdiction-specific routing, caching during outages, and integration with legacy identity systems. The discussion in the PR, which is extensive, has raised detailed questions across FedCM request processing, Service Worker dispatch, Fetch semantics, privacy, and IDP security expectations. Some of the detailed review appears to depend on higher-level direction from the WG.



* Any Other Business (AOB)
 