# FedID WG/CG Telecon, 2025-07-08

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
  * Meeting schedule  
    * FedCM-related call on 15 July is cancelled  
    * Full WG meeting proposed during [IETF 123](https://datatracker.ietf.org/meeting/123/agenda) Tuesday, 22 July, 11:30–13:30 CEST, please agenda+ topics  
* Ecosystem Updates (5 minutes)  
* Issues  
  * [Status of CR Blockers](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
* Any Other Business (AOB)

# Notes

## Administrivia

* Wendy:  
  * Reminders about the WG/CG.  
  * Reminders about the W3C code of conduct  
  * No call in the regular slot next week, proposal for a full WG on Tuesday in sync with the Madrid IETF meeting. Would people like to **Agenda+** tag items for discussion? (Please do)  
  * Any ecosystem updates?  
    * None

## CR Blocker Issues 

* No specific Agenda+ issues in the repo. So, go through the CR blockers of issues: [https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-(Consensus-Blockers-for-CR)](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))  
  * How do we make progress on the issues that have stalled, what can we mark resolve  
* Issue 317 ([concerns about email in Accounts List · Issue \#317 · w3c-fedid/FedCM · GitHub](https://github.com/w3c-fedid/FedCM/issues/317)):  
  * Christian and Nicolás:  
    *  It looks like it has been closed. Or should be closed.  
  * Wendy:   
    * Question about requiring email in accounts list  
  * Christian:   
    * No longer require email in accounts list  
  * Ben:  
    * This addressed my concerns, but Ted has some concerns, and does it satisfy Ted’s concerns?  
  * Ted:  
    * I will take a look  
* Issue 319 ([https://github.com/w3c-fedid/FedCM/issues/319](https://github.com/w3c-fedid/FedCM/issues/319)):   
  * Wendy:   
    * larger issue and opened a multi-idp proposal ([https://github.com/w3c-fedid/multi-idp/issues/2](https://github.com/w3c-fedid/multi-idp/issues/2))  
  * Nicolás:   
    * Adding ‘active’ mode support is required. Supported in ‘passive’ mode right now, but we can add this for ‘active’ mode on button click. Need to think about how to handle multiple get requests. But once ‘active’ mode support has been added we can close this as a CR blocker  
  * Wendy:  
    * Does active mode have its own issue…(Nicolas) This is the issue…there is an issue, Issue: [https://github.com/w3c-fedid/multi-idp/issues/5](https://github.com/w3c-fedid/multi-idp/issues/5)  
* Issue 407 ([https://github.com/w3c-fedid/FedCM/issues/407](https://github.com/w3c-fedid/FedCM/issues/407))  
  * Wendy:  
    * Possibly a duplicate of [https://github.com/w3c-fedid/custom-requests/issues/1](https://github.com/w3c-fedid/custom-requests/issues/1). Which was closed as merged with PR 662\. Does this address the issue in 407?  
  * Nicolás:  
    * I do not think it does. But, I do not know why this is a blocker. Was tagged by Mozilla.   
    * Request to add scopes the RP requires  
    * Phil: Is this addressed by params API, in which you can send scopes?  
    * Nicolas: you’d still show the accounts   
  * Ben:  
    * Tagged as Mozilla by Sam, but I think this is OK to untag.   
  * Wendy:  
    * Will contact Achim to see if he still needs this.  
    * Maybe OK to take this off the priority path  
* Issue 488 ([https://github.com/w3c-fedid/FedCM/issues/488](https://github.com/w3c-fedid/FedCM/issues/488))  
  * Nicolás:  
    * That was closed.  
  * Wendy:  
    * Good, need to update status page  
* Issue 511 ([https://github.com/w3c-fedid/active-mode/issues/3](https://github.com/w3c-fedid/active-mode/issues/3)):  
  * Christian  
    * This could be done.   
    * (Nicolas) Can be closed.  
* Issue 578 ([https://github.com/w3c-fedid/FedCM/issues/578](https://github.com/w3c-fedid/FedCM/issues/578))  
  * Wendy:  
    * Allow IdPs to return JSON objects over Strings  
  * Nicolás:  
    * No progress. Still a blocker, Sam was regarded as a blocker. Nice thing to have, but not a priority  
  * Suresh:  
    * We have made some progress on a proposal. We will  update so people can chime in if needed.   
* Issue 585 ([https://github.com/w3c-fedid/idp-registration/issues/1](https://github.com/w3c-fedid/idp-registration/issues/1))  
  * Wendy:  
    * Allow IdP registrations and RPs to match on a type  
  * Nicolás:  
    * Not many updates, some related privacy issues like \#700 (https://github.com/w3c-fedid/FedCM/issues/700). Need to be considered alongside the API.  
* Issue 587 ([https://github.com/w3c-fedid/FedCM/issues/587](https://github.com/w3c-fedid/FedCM/issues/587))  
  * Wendy:  
    * Why must \`SameSite=None\` ?  
  * Nicolás:  
    * No progress  
  * Christian  
    * Confused as to the issue, but no progress. We only send ‘strict’ right now.  
  * Nicolás and Christian:  
    * We only send SameSite=None but could it be ‘Lax’  
  * Ben:  
    * Need to ask browser security folk, but that has not happened yet  
  * Wendy:  
    * More discussion at: [https://github.com/w3c-fedid/meetings/blob/main/2025/2025-04-22-FedCM-notes.md](https://github.com/w3c-fedid/meetings/blob/main/2025/2025-04-22-FedCM-notes.md)  
* Issue 616 ([https://github.com/w3c-fedid/custom-requests/issues/3](https://github.com/w3c-fedid/custom-requests/issues/3))  
  * Wendy:  
    * Once params are in the spec, deprecate the separate nonce param. Looks done…  
  * Nicolás:  
    * Params is merged, but the ‘nonce’ is still in the request  
  * Christian:  
    * Backwards compatibility concern about removing it.  
  * Nicolás:  
    * Still plan to do that, but not yet  
    * If somebody wants to volunteer for removing that from the spec via a PR, please do.  
    * Has Firefox implemented nonce in the prototype?  
    * (Ben via nod) Firefox have implemented and needs to remove. In Zoom chat “It’s been there since the first prototype”  
  * Wendy:  
    * If you want to try spec editing and want to try a PR, please do.  
* Issue 618 ([https://github.com/w3c-fedid/FedCM/issues/618](https://github.com/w3c-fedid/FedCM/issues/618))  
  * Wendy:  
    * Chained authentication flows  
  * Nicolás:  
    * No progress  
  * Phil: Still interested, tried to flesh out comments, if you were going to send params on the login; first hop (IdP the FedCM communicates with) may not be responsible for the user session.  
  * Nicolás: Why the login URL? By design, doesn’t send anything to the RP  
  * Ben: In the chrome UI, you’re clicking something saying "log in with this RP", so seems reasonable  
  * Phil: That was my take  
  * Nicolás: You’re saying we should allow login URL to contain RP information? \[nods\]  
  * This would tell the IdP that the user has visited the RP. That might require changing the \`.well-known\`. Seems odd to have a login URL there if it’s customizable to the RP. Could also send query parameters, but seems convoluted  
  * Phil: In the R\&E space, typically log in to the IdP to go to a particular resource. If you go to FedCM to sign in with this IdP, you consent/click. Seems logical to send the entire request, so you end up at the RP. Make the flow more straightforward if possible  
  * Nicolás: In this scenario, you don’t show accounts at the beginning?  
  * Phil: No. Show choose IDP rather than choose account.   
  * Nicolás: Is this with active mode? We want to understand desired UX better.  
  * Phil: Potentially one way to use registration API. Register, call FedCM, then sign in with IdP.  
  * Nicolás: Registration isn’t quite that  
  * Phil: If you call the registration API without logging in. At the university portal, register IdP. Then at RP, send over to IdP with the full request, and continue on.  
  * Nicolás: Does the user understand they’re passing everything to a third party? Up for debate. Also seems an edge case where the user visits but doesn’t log in. In the usual case, where a user logs in, use continuation API, which would also need these parameters.   
  * Phil: Pass on from assertion endpoint  
  * Yi: Seems like a big change to add information to the login URL. How does it work in the \`window.open\` case?   
  * Ben: Page calling \`window.open\` can contain opener relationship and any URL parameter  
  * Yi: IdP can trigger on behalf of RP? Will have first party credential and user permission  
  * Nicolas: Not so used by trackers because very visible, many popups are blocked, unreliable.  
  * Yi: In active mode, still user gesture, visible  
  * Nicolas: Active mode has concern that it’s a way to bypass popup blocker. Seems bad.   
  * Yi: There’s browser UI behind, empty-ish  
  * Nicolas: Proposal is to add parameters to login URL. I think from chrome, we’ll have to ask around. Is that the only blocker?  
  * Phil: A few other issues. Adding parameters would help the experience, but also if the IdP that FedCM is calling isn’t responsible for the user account, it can’t respond, but needs to make an additional FedCM call. You can possibly do for assertion but can’t do for accounts endpoint. If you call accounts endpoint, it has to respond. If IdP needs to fetch that info from an upstream IDP, it doesn’t seem to have a way to do that. If IdP authority for your session isn’t the first in the chain, and FedCM calls the accounts endpoint on the first hop. If IdP needs to ask upstream IdP if active session, it doesn’t seem to have a way (in standards) to contact the upstream IdP. Gets stuck in a loop, I don’t know accounts, can’t contact upstream, and then have to respond ‘no accounts’.   
  * Nicolas: To determine accounts, do you need cookies from all chained IDPs?  
  * Phil: Yes  
  * Nicolas: That seems tough. Regarding trackers and attack scenarios. How do we differentiate this from an attack? A challenging problem.   
  * Phil: Maybe it’s on me to try to write that up better. We currently have lots of proxies that do this. Need a story that works as we try to change to FedCM. Was thinking about chaining FedCM calls  
  * Ben: It’s happening after the user gets a dialog and clicks on it.   
  * Nicolas: Not the case in button mode in chrome  
  * Ben: Especially in passive mode, sounds like a strong case for being able to do it with browser UI mediation  
  * Nicolas: If we did enforce that any popup needs to be gated by browser UI, could be reasonable.   
  * Phil: I’ll try to make a better description.   
  * Alan: \[from chat\] Can we have a demonstration of this issue (the chained authentication flow and the issues leading to getting stuck in a loop — as we cannot have this for end users)?   
* Many thanks to Phil for scribing and Wendy taking over scribing when Phil was trying to provide input/comments   
* Nicolas: Please add 700 (privacy issue) as a CR blocker. 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (independent)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Phil Smart (Shibboleth/Jisc)  
* Ben VanderSloot (Mozilla)  
* Parth Bhatt (An Individual/Independent)  
* Mike Jones (Self-Issued Consulting)  
* Nicolás Peña Moreno (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Erica Kovac (Google Chrome)  
* Alan Buxey (MyUNiDAYS Ltd.)   
* Siddhartha Pandey (Microsoft Edge)  
* Brian Daugherty (Google Identity)  
* Suresh Potti (Microsoft Edge)  
* Bjorn Hjelm (Yubico)  
* Emily Lauber (Microsoft Identity)  
* Simone Onofri (W3C)

# Regrets

*  Heather Flanagan