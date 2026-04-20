# FedID WG Telecon — DC API Series A, 2026-04-20

* Moderators: Heather

* Scribe: Lee

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * FYI: TPAC 2027 dates/location: 6–10 December 2027, Panamá  
* Ecosystem Updates (5 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Protocol Integrity Requirements for Request/Response Tampering \#494](https://github.com/w3c-fedid/digital-credentials/issues/494)  
  * Privacy status or issues  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (5 minutes)

* Heather: Feedback needed on the Interactive Auth Endpoint for the OpenVCI spec.

## DC API Issues & PRs

### [Protocol Integrity Requirements for Request/Response Tampering \#494](https://github.com/w3c-fedid/digital-credentials/issues/494)

* Heather: Covered in the [B call](https://github.com/w3c-fedid/meetings/blob/main/2026/2026-04-15-DCAPI-B-notes.md#protocol-integrity-requirements-for-requestresponse-tampering-494). Likely needed three separate issues (not yet filed). Bringing it back to this call for discussion.  
* Tim: Still struggling with the assumption that this API is for government IDs. But this spec isn’t specific to a given type of credential. Because we made the decision to layer things in this way, we can’t make decisions about these areas. But this debate comes up all the time. Decided not to include use-case-specific templates in the API. But have to decide to commit to the arch we picked.   
* Lee: Agree we need to stick with the generic API request protocol. We can say we have a dependency on what they provide. Then there’s the layer below, and that still doesn’t have complete specificity, at the OpenID4VP. We need to draw a line; this API is designed to get arbitrary things from wallets. We need to commit to the generic; stop going around in circles.   
* Tim: Need to draw a line in the sand and if there are fundamental issues with the architecture, people should object to the charter of the group.  
* Lee:  Remember that the premise is that we need an alternative to custom schemes. The latest EU draft did mandate DC API, but it’s still hotly contested, in part because of this uncertainty. Bear in mind that drastic changes will reduce the likelihood of its being used.   
* Heather: John from Mozilla said he thought there were options. I encouraged him to write them down.   
* Tim: Can propose a cert transparency thing if they want, but it would be out of scope of this spec. Can’t fundamentally change it at this point.  
* Lee: Keep in mind the balance, if you add gatekeeping inconsistent with some uses, then those people won’t use it, e.g., in EU regs. Too late to have this conversation.   
* Wendy: Need to find where we have captured this architectural layering decision in previous meetings, and use this to not relitigate these decisions unless new information is made available.  
* Wendy: Will take the action to find these materials.  
* Heather: Need folks to help with writing the privacy section of the spec. Have requested help from the W3C Privacy person, Tara Whalen.  
* 

# AOB

Top Level Origin:

* Mohamed: PR [419](https://github.com/w3c-fedid/digital-credentials/pull/419).. Proposes forwarding calling origin and top level origin. The problem is that Chrome, Android, and PXP don't support this. Proposing to take this out of the PR because it adds complexity, and look into adding it back later.  
* Tim:  Look at [Issue 95](https://github.com/w3c-fedid/digital-credentials/issues/95) which proposes client Data.   
* Lee: Client data JSON, replace any place that says "origin" with “client data hash”. Touches PXP (new name for Hybrid), Annex C, OpenID4VP … Everywhere we sign over an origin, we instead sign over client data. We probably should have done that from the start. WebAuthn does that. Makes sense. More contextual information, e.g., if it’s coming from a webview, should you include that in the client data? Big change, you’d have to figure out how to make it backward compatible.   
* Heather: Propose for v2?  
* Lee: Probably breaking enough that it would have to be v2, still need backward compatibility, all up the stack. V2 OpenID4VP, Annex C, Hybrid, everything would have to switch.   
* Tim: We could have gained useful experience from looking at parallel experience in a similar API (WebAuthn).   
* Tim: will have to come out as you can’t pass top origin right now.


Multi Responses:

* Helen: Multiple Responses is another breaking change.

V2

* Heather: Should we start tagging things for v2 and clearly and separating things.  
* Tim: At IIW, we can discuss all the breaking changes that might be needed for a v2.

Heather/Tim/Wendy: try to keep B call and dial in from IIW.

Mohamed: Please review [381](https://github.com/w3c-fedid/digital-credentials/pull/381) re webdriver. It’s awaiting Marcos adding supporting for parsing CDDL in respec and could use more eyes  
Tim: Can ask Nina to take a look.  
Mohamed: Nina is reviewing.

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Wendy Seltzer (co-chair)  
* Mohamed Amir Yosef (Google Chrome)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Tejas Dhagawkar(Microsoft Edge)  
* Isaiah Inuwa (Bitwarden)  
* Tim Cappalli (Okta)  
* Lee Campbell (Google Android)