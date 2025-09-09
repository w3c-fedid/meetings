# FedID WG/CG Telecon, 2025-09-09

* Moderators: Wendy Seltzer

* Scribe: Phil

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
* Ecosystem Updates (5 minutes) \*  
* Issues & PRs  
  * [Consider forcing accounts push on registered IDPs \#24](https://github.com/w3c-fedid/idp-registration/issues/24)  
  * [Add multi IDP on active mode \#5](https://github.com/w3c-fedid/multi-idp/issues/5)  
  * [Support chained authentication flows before reducing heuristics and classifications/lists in navigational tracking mitigations \#618](https://github.com/w3c-fedid/FedCM/issues/618)  
* Any Other Business (AOB)

# Notes

## Administrivia

* Wendy:  
  * WG reminders. Talking about FedCM.   
  * TPAC two meeting dates, Thursday and Friday, Nov 13th and 14th (see above)  
  * Remote participation is possible. Any questions let us know.

## Ecosystem Updates 

* Wendy:  
  * Ecosystem updates….nope

## Issues & PRs

### [Consider forcing accounts push on registered IDPs \#24](https://github.com/w3c-fedid/idp-registration/issues/24)  
  * Nicolás:  
    * Making progress on (IdP) registration and showing permission or not. Now I want to surface the idea of only allowing registration to work with accounts push. IdP tells the user-agent in advance which accounts the user is logged into, signing status header, expiration, etc. Allows building the FedCM API without having to do (as many) fetches. Depends on IdP Type, which protocol the IdP and RP supports.  
    * Has anybody tried registration, and any comments or concerns? Improved privacy and performance (main gains)  
    * May or may not be feasible for the IdP to do accounts push. Any thoughts? Or we will proceed.  
  * Emily:  
    * Discussed before. Re-authentication does not have an option for the error to be passed back. How does that work with the push model?  
  * Nicolás:  
    * For the push model, there is an ahead-of-sync situation.   
    * A user may want to use an account that got logged out of the IdP. Server-side logout would result in the account not being present. The IdP could show an error or continuation to allow the user to log into a different account  
    * Another option: the sign in expires, IdP session has expired, but the user is still logged in. Sign-in status can be set via sub-resources, so the IdP should be able to update that when required—alongside the expiry of the IdP cookie.   
    * With accounts push, the account would not be shown in the list; there would not be an error in that case. As there is no fetch, there is no timing attack, so would not need to show the mis-match dialog.   
  * Emily:  
    * In the first scenario, it makes sense for the IdP to offer continue-on.  
    * The issue was with silent authentication. If there is some kind of error (e.g., the account is logged out on the server, but still logged in on the browser), there is no option for an error.  
  * Nicolás:  
    * For re-authentication, you cannot use continue-on. Do not want to let IdP use pop-ups without a user gesture. So in silent mode, we do not want to allow the IdP to show a pop-up (spam), so we want to show an error (no alternative to that).    
  * Sam:  
    * The accounts endpoint would not return if the cookie had expired. But in accounts-push, we would think they are logged in. But will find out at the assertion endpoint to actually determine if this is a valid re-authentication.  
  * Emily:  
    * If not valid, what can the IdP communicate to the user, e.g., to select another account?  
  * Sam:  
    * Not now, but we could allow the user to re-authenticate after a user gesture.  
    * This is independent from accounts push  
  * Emily:  
    * Can or cannot be addressed?  
  * Sam:  
    * It can.   
    * Accounts selector could show something more meaningful  
    * IdP could communicate to the browser that it wants to re-auth, and the browser could allow a popup.  
    * Neither accounts pull nor push supports it right now, but they could.  
  * Yi:  
    * IdP can use error API to allow IdP to pop-up a window  
    * But not as well as needed, but we could in the future  
  * Emelia:  
    * Another case: the account is deactivated by the IdP. Google removes my account, but the browser still thinks  that I am logged in. Does account push solve that?  
  * Christian:  
    * The only way to update the list of accounts is if the user uses the IdP again and the IdP notifies the browser the account is not valid.  
    * Otherwise, the account would appear in the list, the user would select, and the IdP would fail and require continue on  
  * Nicolás:  
    * Except that is not the case with the auto re-authentication.  
    * (PS did not catch, but we can do something to improve that)  
  * Emelia:  
    * That answers my question.  
  * Emelia:  
    * How far have we got with "Type any", and being able to support large and decentralised IdPs? E.g., Mastodon servers are all IdPs, Solid has the same thing. Any progress?  
  * Nicolás:  
    * The Type is something we have been using. Implementation is not great, but it does exist. Haven't decided where the type will go. Either the configURL (needs fetching) or the registration call (but need to re-register if you change type).  
    * Other question, proposal to remove the well-known checks for registered IdPs (IdPs that use the registration IdP). Easier to do if we use accounts push (fewer tracking vectors).   
    * Supports multiple IdPs in eTLD+1, helps with the smaller IdP scenarios.  
  * Emelia:  
    * I think that makes sense; I will go check progress.  
    * Is the co-author of: [draft-parecki-oauth-client-id-metadata-document-03](https://datatracker.ietf.org/doc/html/draft-parecki-oauth-client-id-metadata-document-03)  
  * Nicolás:   
    * I’ll take an action item to update explainer  
    * Not a lot of progress; UI is the tricky part. Internal discussion on UX, a bit stalled, but unblocked. More progress in the near term.  
  * Emelia:  
    * Improving the authentication experience for social platforms. FedCM will help this.  
  * Sam:  
    * Making forward progress on IdP registration API; Mastodon and Bluesky use cases are good.  
    * Prototype in Chrome behind flags. Can we get help on trying that?  
  * Emelia:  
    * Mastodon are looking at the Client ID Metadata Document draft to circumvent the (OIDC) dynamic registration process.  
    * FedCM fits with the ideas of that, so would be interested to use this.  
    * Another question: mostly Chrome that has the implementations, what about other browsers?  
  * Wendy:  
    * Mozilla deprioritised this work for now.  
    * So at the moment, not a lot of Mozilla participation.  
    * We’ve not historically seen Safari participation.   
  * Emelia:  
    * Safari is pushing the passkey stuff heavily. This seems to fit with that.  
  * Wendy:  
    * We would love to see more implementer participation. Hearing from others in the broader ecosystem about needs… Make your voices heard.  
  * Emelia:  
    * Document about the intent to implement.   
      * I maintain this software and want to implement FedCM. Adds weight to the argument for other browsers to implement that.  
  * Tim:  
    * That does happen through the standards process.  
  * Emelia:  
    * More centralised point, to say, simplify the OAuth flow using FedCM go here to find out more (PS, did not catch the end).  
### [Add multi IDP on active mode \#5](https://github.com/w3c-fedid/multi-idp/issues/5)  
  * Nicolás:  
    * Propose Multi-IdP issue be closed in terms of CR blockers.   
    * This has been implemented for passive mode. No plans to add this for active mode (user gesture needed). No demand for it. UX questions around what that would look like.  
    * Based on that, is anybody opposed to considering Multi-IdP to be closed as a CR blocker? No plan to tackle it for active mode right now.   
    * Does this seem OK to people?  
  * Emily:  
    * Remind me, please — difference between active and passive?  
  * Nicolás:  
    * Active mode requires a user gesture to show the FedCM browser dialog.   
    * Passive mode, FedCM activates on page load for the RP (importantly, without user gesture). A dialog may or may not be shown. If all conditions hold, the accounts chooser is shown.  
    * Allows RPs to increase login rates.   
  * Wendy:  
    * Proposal to leave the issue open, but take it off the blocker list?  
  * Nicolás:  
    * The proposal is to close issue \#2. Is still open because of active mode, but propose closing that issue (moving it off CR blockers), but keeping \#5 open in case we receive support.  
  * Wendy:  
    * Will add a note to issue \#2 with a proposal to close.   
    * Close at next meeting if no objections  
### [Support chained authentication flows before reducing heuristics and classifications/lists in navigational tracking mitigations \#618](https://github.com/w3c-fedid/FedCM/issues/618)  
  * Sam:  
    * Issue discussed last week. Did I capture the discussion?  
    * Wanted to capture; this is a use case that FedCM could not satisfy.  
    * Heard from others that this is not an immediate problem due to 3PC mitigations, but could be for link decoration.  
    * Other groups (PrivacyCG, for example) could cite FedCM as a way to overcome issues if link decoration degrades redirect authentication flows.  
  * George:  
    * If we are going to end up writing an implementor's guide, we should call out that this use case is not supported.   
    * Also, in an Enterprise, all the Enterprise deployments are chained in some way, which would preclude them from using this.  
  * Phil: 	  
    * Agreed, thanks for writing, adds clarity to what can and can’t be used.   
    * For now, I can’t see a better route.  
    * That can conclude the issue for the moment.  
  * Sam:  
    * Not concluding permanently, but for now.   
  * Wendy:  
    * Seems like approval, so we can close, but need a follow up explanation of what else needs to be done to resolve the conversation.  
  * Sam:  
    * Nothing else is actionable right now.  
    * When we write implementation guides we can add that.  
    * Nothing else actionable for now.  
  * Wendy:  
    * The issue describes the work done. Thanks George and Phil for adding input to that.  
    * Will keep watching that.  
  * Sam:  
    * Mark as Wont Fix and resolve.  
  * Wendy:  
    * Will mark as wont fix.

## Any Other Business (AOB)

* Tim:  
  * New CG for developers for best practices on implementing (passkey.dev and digital credentials). Web Identity & Credentials Adoption Community Group.  
  * Needs support for the group to be created:  
    * [https://www.w3.org/community/groups/proposed/](https://www.w3.org/community/groups/proposed/)  
    * Bottom group listed.  
* Sam:  
  * We need this.  
  * Plenty of stuff in identity is not related to digital credentials  
* Tim:  
  * Credentials are wider scoped than Digital Credentials. Will cross that bridge when we get to it.  
* Sam:  
  * ‘Unification’ reconciles passwords and passkeys and social login. Digital Credentials don't yet have enough uptake, but will eventually reconcile that.   
  * Prototype on blink dev. [Immediate mode.](https://groups.google.com/a/chromium.org/g/blink-dev/c/zC13ioLIZ_E/m/P-P6B6gNCQAJ)   
* Tim:  
  * Background: I do not have a passkey on my device, can I fall back to something else e.g. FedCM or password.  
* Sam:  
  * Intent: choose interchangeably between credentials.   
  * [https://groups.google.com/a/chromium.org/g/blink-dev/c/zC13ioLIZ\_E/m/P-P6B6gNCQAJ](https://groups.google.com/a/chromium.org/g/blink-dev/c/zC13ioLIZ_E/m/P-P6B6gNCQAJ)  
* Wendy:  
  * Please tag issues for the next call.

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Emily Lauber (Microsoft Identity)   
* Nicolás Peña Moreno (Google Chrome)  
* Michael Knowles (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Phil Smart (Shibboleth/Jisc)  
* Natalia Markoborodova (Google)  
* George Fletcher (Practical Identity LLC)  
* Yi Gu (Google Chrome)  
* Theo \- [@thhck](https://github.com/thhck)   
* Alan Buxey (MyUNiDAYS Ltd.)  
* Tim Cappalli (Okta)  
* Emelia Smith  
* Suresh Potti (Microsoft)  
* Siddhartha Pandey (Microsoft Edge)
