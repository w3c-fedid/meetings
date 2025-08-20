# FedID WG/CG Telecon, 2025-08-19

* Moderators: Heather Flanagan

* Scribe:  Wendy

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
    * Note: IIW dates have changed\!  
  * [2025 TPAC](https://www.w3.org/2025/11/TPAC/schedule.html) FedID WG meeting dates:   
    * Thursday, 13 November, @ 09:00-12:30 UTC+9  
    * Friday, 14 November, @ 09:00-12:30 UTC+9  
* Ecosystem Updates (5 minutes)  
* Issues  
  * [Support showing iframe origins in the UI, when they are third-party \#725](https://github.com/w3c-fedid/FedCM/issues/725)  
  * [Consider forcing accounts push on registered IDPs \#24](https://github.com/w3c-fedid/idp-registration/issues/24)  
  * [Status of FPWD‐identified Issues (Consensus Blockers for CR)](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
* PRs  
  * n/a  
* Any Other Business (AOB)

# Notes

## Administrivia

* Membership, Code of Conduct  
* Heather: IIW Week of 20 Oct. We will not have a WG/CG meeting, TPAC follows soon after. OpenID Foundation still looking to hold meetings  
* TPAC is coming\! 2 sessions. Inclined to split between the specs. We’’ll start working on agenda

## Ecosystem Updates (5 minutes)

* None

## Issues

### [Support showing iframe origins in the UI, when they are third-party \#725](https://github.com/w3c-fedid/FedCM/issues/725)

* Christian: From my perspective, after comments from Ben, resolved. I’ll write a PR. If you have thoughts on the feature, please comment on the issue if you haven’t. 

### [Consider forcing accounts push on registered IDPs \#24](https://github.com/w3c-fedid/idp-registration/issues/24)

* Nicolas: For IdP registration, accounts push: IdPs provide some information about the user, e.g., login, and save, so that when a user visits RP, we don’t have to perform any fetches, assuming it has been registered in the past. Advantages: privacy. Some issues with fetching because we want to allow multiple origins in the same domain. Instead, pull the data from the browser, so the registered IDP doesn’t get notified when the user sees an account, only when the account is used, after the user agrees to use the account. Improved performance because of reduced fetches, and improved privacy for the same reason. Does anyone have concerns or other thoughts?  
* Emily: Need some time to think about it.   
* Nicolas: Has Microsoft looked at IdP registration?   
* Emily: We are interested, though we haven’t yet done any implementation. Thinking about it especially for enterprise use cases  
* Nicolas: You’d need to update accounts info whenever a user visits IdP. Set an expiration time so stale info doesn’t show up. Pick a reasonable expiration (and re-visit) time. THat’s the tradeoff: the accounts shown could potentially be stale. Say you changed info on a different device. It wouldn’t be reflected immediately on the other device, until you visit IdP again. Please chime in on the issue  
* Sam: I wasn’t thinking this would be mutually exclusive with pull. Just makes things simpler, especially in regard to multiple IdPs. With the proposal to not have permission prompts for IdPs, expect more IdPs, then caching more information in the browser can make life easier. Sequencing point  
* Sam: Concretely, names, email addresses, profile pictures. Also: phone numbers/usernames. That’s what’s cached. After the user picks in the account chooser, then a pull request for update to refresh stale data.   
* Emily: That makes sense as optimization  
* Sam: Some of our intuition we’re trying to validate, is whether users change those identifiers as often as other data (we expect not)  
* Emily; I’m more concerned whether there’s a security impact if the user changes email or phone number, and it doesn’t get reflected on other devices.   
* Nicolas: You’d still see the update when you hit the server.   
* Emily: There are multiple UX for account selection. Do pushed accounts show up in all?  
* Sam: We intend it for all.   
* Nicolas: If you auto-signed in, you could get a popup.   
* Sam: It might just be an error  
* Nicolas: \[thinking\]  
* \[musings about how and whether users get the opportunity to correct errors\]


Sam: Verified email autocomplete is something we’d like to talk about with the group sometime soon. Dick Hardt and I have been working on it in another repo 

* (From chat) ﻿@Sam Goto are the chaining use cases that Dick Hardt has working fine with FedCM? Since you are working with him already, he might also be a good person to ask about this use case as Hello is a stateful “proxy IDP”.

### [Status of FPWD‐identified Issues (Consensus Blockers for CR)](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))

* Heather: Of the 7 issues listed as blockers, 4 don’t have any proposals yet. Do you have any thoughts on how to progress them?  (Stage 0\)  
* Nicolas: [\#578](https://github.com/w3c-fedid/FedCM/issues/578) is done already thanks to Suresh. [https://github.com/w3c-fedid/idp-registration/issues/13](https://github.com/w3c-fedid/idp-registration/issues/13)   
* Sam: Trying to understand [\#618](https://github.com/w3c-fedid/FedCM/issues/618), if it’s more than link decoration  
* George: There’s an escape hatch to let the IDP take over authentication, if you could trigger that. There are some parties in the chain that are just proxies. You might have an API gateway acting as the front door, but it doesn’t do any authentication, just a redirect. That’s a common pattern, and chains can be longer than one redirect.   
* Sam: That's my understanding, via a popup window.   
* Nicolas: How do you know which accounts to show?  
* Sam: Say you’re logged out, we open a popup window for the user to log in to IdP. IdP may choose another IdP with traditional federation.  
* George: Often need to pass parameters to another party. Effectively, IdP hint, to point to, e.g., sign in with Facebook from AOL authorization. Facebook would get the client ID of the AOL IdP. The RP needed to tell the AOL IdP that the user wanted to login with FB. If we have an equivalent to PAR. Probably helpful to have Phil re-test with the latest version. I’ve seen a chain of at least 4 hops in the wild.   
* Sam: Two questions, does it break in current deployment, and can they move to FedCM?  
* George: “Broken” can be difficult to figure out with heuristics for stripping link-decoration. If the first IdP is using FedCM to talk to other parties, and that fails, it’s broken.   
* Achim: Not the smoothest experience. You can’t run these proxy flows through FedCM.  
* Heather: I’d like to ask Phil to do a demo and show us what the “break” looks like.  
* Nicolas: Will we have a discussion whether this should remain a CR blocker? Mozilla had tagged it as such.  
* Heather: Chairs will discuss  
* Heather: [\#729](https://github.com/w3c-fedid/FedCM/issues/729).   
* Christian: Think it’s a small fix.   
* Nicolas: Let’s ask if there are any concerns to close.   
* Sam: It sounds as though we have a path to closing most of the issues you raised. The chained IDP has the most open.   
* Heather: Those were the stage 0 issues. There are a few others.   
* 


## PRs

n/a

## Any Other Business (AOB)

* Heather: We’ll see if we have agenda for next week. Likely no call Sept. 2, day after US Labor Day. Will update calendar



# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Wendy Seltzer (co-chair)  
* George Fletcher (Practical Identity LLC)  
* Yi Gu (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Sam Goto (Google Chrome)  
* Michael Knowles (Google Chrome)  
* Mike Jones (Self-Issued)  
* Alex B Chalmers (self)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Emily Lauber (Microsoft Identity)   
* Ketan Mehta (NIST)  
* Achim Schlosser (Bertelsmann, co-chair)  
* Simone Onofri (W3C)  
  