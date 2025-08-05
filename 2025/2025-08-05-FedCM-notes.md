# FedID WG/CG Telecon, 2025-08-05

* Moderators: Heather Flanagan

* Scribe: Dan Moore

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
    * Meeting schedule  
      * Options:  
        * FedID Hybrid Meeting on Monday, 27 October  
        * No FedID Hybrid Meeting the week of 27 October  
        * FedID Hybrid Meeting on Thursday, 30 October  
        * Some other option   
* Ecosystem Updates (5 minutes)  
* Issues  
  * [Support showing iframe origins in the UI, when they are third-party \#725](https://github.com/w3c-fedid/FedCM/issues/725)  
  * [Status of CR Blockers](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
* PRs  
  * n/a  
* Any Other Business (AOB)

# Notes

## Administrivia

* Heather: Looking for feedback around October meetings

## Ecosystem Updates (5 minutes)

* No ecosystem updates  
* Aaron Parecki from Okta may be doing demo in the future. 

## Issues

### [Support showing iframe origins in the UI, when they are third-party \#725](https://github.com/w3c-fedid/FedCM/issues/725)

* Christian: Did anyone have time to address comments in the issue? We’re stuck.  
* Tim: In WebAuthn, we have top and original origin. Don’t dictate you must display both to the user, but it is strongly recommended. Would have preferred it to be a requirement.  
* Christian: We are trying to limit UI requirements, but we didn’t think about that in this situation.  
* Tim: Unaware of anyone showing both.  
* Nicolás: WebAuthn doesn’t have an API to show both.  
* Christian: For FedCM in particular, we don’t always want to show iframe origin because it doesn’t always make sense to the user.  
* Tim: Where’s the line between abuse and legitimate behavior?  
* Christian: In their proposal, let the IdP manage it.  
* Tim: Also have permission policy in WebAuthn  
* Christian: Could imagine a specific permissions policy on whether the iframe needs to be shown, but not part of the proposal today.  
* Heather: We’ve tried to keep optional stuff outside of the core spec. Does this qualify? Touches on privacy concerns.  
* Christian: For this question, we need Ben/Firefox.  
* Nicolás: Impression was that Ben was okay with features, less okay with design. Maybe he’d be okay with it being optional and part of client metadata (non-core for now). Maybe reach out directly over chat.

### [Status of CR Blockers](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))

* Heather: One question, related to issue 616\. Lots of discussion, is that done?  
* Nicolás: Yes, it’s done spec-wise.  


## PRs

n/a

## Any Other Business (AOB)
Dan: What is the status of outreach to the safari team?

Heather: Going to reach out to them soon. Not going to block it, but not spending any resources to implement it.

George: Are we doing any recommendations for relying parties on what to do with the site.

Tim: Not a great answer, but with any of these APIs (Fido, WebAuthn), all are opt-in, so need to offer fall-back. Same for digital credentials, passkeys, etc. Agree there should be guidance.

Nicolás: Not sure where guidance should live, maybe not in spec. Browser engineers/companies do listen to feedback. Please reach out whenever you feel a browser should implement an API. Don’t listen to Chrome, but do listen to developers. That is a way to encourage them to implement. May take them a while due to FedCM size.

Tim: As an end user, market forces will impact. Happens with passkeys. Pressure from users will impact company decisions.

Dan: What does guidance look like?

George: Something about impact on user experience and how to explain the discrepancy for RPs and their end users. Generic guidance about failover makes sense as well. It means you have 2 sets of RP code. People do that with passkeys today, but it creates a weird user experience. \[Gave an example of passkey experience.\] These are things RPs will run into; more about awareness.

Tim: Passkeys are a good example of where people have ignored provided guidance. 

George: Agree, people are going to do that for non-technical reasons. Often puts developers in no-mans land.

Heather: Now that we agree there should be guidance; it won’t be in the spec, would be parallel documentation.

Tim: Around TPAC? time he’s going to create a group around authentication on the web (passkeys.dev, and others). Developer focused doc around all identity on the web.


# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* George Fletcher (Practical Identity LLC)  
* Phil Smart (Shibboleth/Jisc)   
* Dan Moore (FusionAuth)  
* Mike Jones (Self-Issued Consulting)  
* Nicolás Peña Moreno (Google Chrome)  
* Christian Biesinger (Google Chrome)
* Bjorn Hjelm (Yubico)