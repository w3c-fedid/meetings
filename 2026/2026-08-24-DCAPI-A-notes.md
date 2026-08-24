# FedID WG Telecon — DC API Series A, 2026-08-24

* Moderators: Heather

* Scribe: Wendy

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?   
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Note: next two calls are canceled (September 1 & 7\)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [clientData (26H2 edition) \#574](https://github.com/w3c-fedid/digital-credentials/issues/574)  
  * [EUDI Wallet functional conformance testing \#471](https://github.com/w3c-fedid/digital-credentials/issues/471)  
  * [Define error handling \#130](https://github.com/w3c-fedid/digital-credentials/issues/130)  
  * [Security: Expand Threat Model and mitigate malicious payloads — \#533](https://github.com/w3c-fedid/digital-credentials/pull/533)  
  * [Privacy: Add Data Clearing and Credential Availability protections — \#536](https://github.com/w3c-fedid/digital-credentials/pull/536)  
  * [Restore the origin-bound declaration on DigitalCredential — \#559](https://github.com/w3c-fedid/digital-credentials/pull/559)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (10 minutes)

Heather: Convo on slack about how DC API is referenced in the implementing acts. Legal, complicated. August 20 in the FedID/WG slack. [https://w3ccommunity.slack.com/archives/C06RR5RQUDT/p1787249005401179](https://w3ccommunity.slack.com/archives/C06RR5RQUDT/p1787249005401179) 

## DC API Issues & PRs (45 minutes)

### [clientData (26H2 edition) \#574](https://github.com/w3c-fedid/digital-credentials/issues/574)

Heather: Has anyone else looked at this?  
Mohamed: Can this wait until after CR? If we’re trying to push for CR by TPAC, this one might be controversial and take longer than usual to merge.   
Heather: Please review and add your opinion, including on the timing pre/post-CR.

### [EUDI Wallet functional conformance testing \#471](https://github.com/w3c-fedid/digital-credentials/issues/471)

Heather: I was hoping Simone would be here. Is it relevant to the spec?  
Wendy: Propose to close. We want to help the ecosystem, but don’t see much here in W3C remit.  
Christian: My understanding is that it doesn’t change the spec. It’s about conformance testing.   
John: All the other tests happening in theory at OpenID Foundation.   
Christian: The Commission is working on automated conformance descriptions. And OpenID has some conformance testing. We’ve learned that having some automated testing is extremely valuable for the ecosystem.   
Heather: Propose to close.  
Christian: It might make sense to invite Oliver Taboux (sp?) to the call.

### [Define error handling \#130](https://github.com/w3c-fedid/digital-credentials/issues/130)

Heather: Marcos reopened this saying [\#421](https://github.com/w3c-fedid/digital-credentials/pull/421) didn’t address.   
Mohamed: Many of the errors are defined already. I’d like to understand what Marcos thinks is missing.  
Tim: In general, at this point, it’s more productive to open new issues than reopen old ones. 

### [Security: Expand Threat Model and mitigate malicious payloads — \#533](https://github.com/w3c-fedid/digital-credentials/pull/533)

Mohamed: Thanks for review, Tim. I’m waiting for Marcos. This came from a horizontal security review. To note where the API can/can’t address malicious payloads.  
Christian: Adding a statement that this API can’t fix breaks in the browser or API, or can’t defend against malicious payloads.  
Mohamed: Right, that’s on the credential manager.  
Christian: Think about how the different entities interact.  
Heather: And that helps address some of Nick’s questions.  
Mohamed: Context for the wallet-binding discussion.  
Heather: Good to merge after further reviews requested.	

### [Privacy: Add Data Clearing and Credential Availability protections — \#536](https://github.com/w3c-fedid/digital-credentials/pull/536)

Heather: Does this close any other open privacy issues?  
Mohamed: Helps address some gaps. Make sure we don’t leak credential availability.   
Heather: Any concerns? \[silence\] After review, good to merge.

### [Restore the origin-bound declaration on DigitalCredential — \#559](https://github.com/w3c-fedid/digital-credentials/pull/559)

Heather: Anything the group needs to discuss?   
Mohamed: Borderline editorial, but we wanted to ask the group. Moving the whole origin-check to the credential manager level and removing it from here. Also restoring origin-bound declaration.  
Heather: Do you know when webappsec will discuss?  
Mohamed: Nina has already approved.   
Heather: Hearing no other concerns right now. Good to go when other things unblock it. 

## Any Other Business (AOB)

* Mohamed: Regarded wallet-binding token. I’m working on a PR that has Apple and Google alignment. We’ve been discussing it for a long time, and it will really want review from the group.  
* Tim: I don’t think there’s consensus on sharing platform-specific identifiers with the web. THat might still be in the proposal, and should be discussed with the group.   
* Tim: I think we had agreed we weren’t going to ship cross-device issuance at CR.  
* Mohamed: I hadn’t understood it that way.   
* Christian: Should we try to have a side discussion at GDC next week?   
* Tim: I think the TAG will have a concern with sharing platform-specific identifiers through web API. It would be great to get TAG input earlier.   
* Mohamed: Is that a concern for binding token or only for allow-list? It’s up to the platform to decide what to do with the token  
* Tim: WEI in an API, if you squint at it. Sharing platform-specific attestation through the web API.   
* Mohamed: The web API only shares the nonce.  
* Tim: What's your answer if I’m on Linux and want to interop? It can’t without a platform-proprietary component? Some people will have issues with that.   
* Mohamed: Thanks for sharing that concern. I won’t be in Geneva.   
* Heather: It will likely take multiple conversations.  
* Christian: Is there a writeup of the proposed solution?   
* Mohamed: Option 3 in the wallet-binding token issue. [https://github.com/w3c-fedid/digital-credentials/issues/382](https://github.com/w3c-fedid/digital-credentials/issues/382)   
* Heather: If you have opinions, please offer them in the issue, so we can see all the inputs of the group toward consensus. 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Wendy Seltzer (co-chair)  
* Mohamed Amir Yosef (Google Chrome)  
* Christian Bormann (SPRIND)  
* Ryan Watkins (Mastercard)  
* Bjorn Hjelm (Yubico)  
* Tim Cappalli  
* Rene Leveille  
* John Bradley

