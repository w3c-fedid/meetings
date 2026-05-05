# FedID WG/CG Telecon, 2026-05-05

* Moderators:  Heather

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
* Ecosystem Updates (5 minutes)  
* Discussion (45 minutes)  
  * [Allow IDPs to delegate well-known file hosting via DNS TXT record \#821](https://github.com/w3c-fedid/FedCM/pull/821)  
  * [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)  
* Any Other Business (AOB)

# Notes

## Administrivia

* W3C Code of Conduct

## 

## Ecosystem Updates (5 minutes)

* Heather:  
  * Any updates?  
* Sam:  
  * New Chrome stable features starting today, agentic AI login, and ambient UI  
    * Flags: chrome://flags/\#fedcm-ambient-ui  
* (No others)

## Discussion (45 minutes)

### [Allow IDPs to delegate well-known file hosting via DNS TXT record \#821](https://github.com/w3c-fedid/FedCM/pull/821)

* **Latest PR:** [https://github.com/w3c-fedid/FedCM/pull/823](https://github.com/w3c-fedid/FedCM/pull/823)   
* Heather:  
  * Latest?  
* Sam:  
  * BlinkOn, Microsoft, and Chrome teams met.   
  * Ajay and Will. Ajay is implementing the endpoints.   
  * Unblocked from DNS and Service Worker changes?  
* Ajay:  
  * The major blocker is hosting the well-known file in the apex domain.  
  * No approvals on PR yet.  
    * Want to merge if consensus.  
  * Need a conclusion on this; once implemented this would unblock us.  
* Sam:  
  * Seems like you are blocked on this.  
  * Best proposal so far was Will’s proposal to have a well-defined subdomain, something like [`https://web-identity.contoso.com/.well-known/web-identity`](https://web-identity.contoso.com/.well-known/web-identity)  
  * The browser would fetch it with HTTPS, same as other well-known files.  
    * Fetch this new one first?   
      * So far, it's fetching the new one first.  
  * Suresh had the bandwidth to implement this, so put an implementation behind a flag.   
    * MS should be able to change Chrome and MS IdP to change locally to test this.  
* Ajay:  
  * Will follow up with Suresh in implementation, but when will PR be merged?  
* Heather:  
  * Wants to check in with other implementing concerns on using subdomains.  
* Bjorn:  
  * *Web-identity* naming is not necessarily a good choice, not specific enough.  
* Aaron:  
  * Not convinced on specific name, but general idea could work.  
* Phil:  
  * Better than apex.  
* Emelia  
  * Do we need both CNAME and TXT records?  
* Sam:  
  * Two different PRs for both.  
  * So need to clean up PRs.  
  * No need for TXT record if using the well-known subdomain.  
* Emelia:  
  * (PS, sorry, did not catch)  
* Sam:  
  * Will picked a subdomain of a subdomain.  
  * The same argument made for subdomains can be made for paths. This is in a well-known subdomain and a well-known path.   
* Emelia:  
  * Still see inconsistent examples in the PR.  
* Sam:  
  * Having control of which to use could be an option, but looking to pick one as the default and then fall back to the other.  
  * Will’s intent was to pick an order of resolution and choose the subdomain first.  
* Heather:  
  * Agreement in principle.  
  * Naming needs review.  
  * Need to clean up the PR.  
* Ajay:  
  * Confirms the proposal, which has been noted not to be in PR\#823  
  * Does it need to be a CNAME record?  
* Sam:  
  * CNAME or A record  
* Ajay:  
  * Does it need to be web-identity or some other name? Can you add that to the PR, please?  
* Sam:  
  * (Ajay) We can learn from implementing some of this. Merging this into the Chromium code base.   
  * Should not be blocked on spec PR to try this out.  
* Emelia (from chat):  
  * *‘I'm still inclined to suggest that this resolution behavior should be opt-in, rather than default, since it's more complicated for smaller deployments vs larger deployments’*  
* Ajay:  
  * We can try to implement this behind a flag.  
  * This can inform the spec.  
* Sam:  
  * From a Blink perspective, send an intent to prototype.  
  * Using the subdomain approach, more people can try this themselves.   
  * Pick a name for now, and try it out.  
* Ajay (from the chat):  
  * ‘*As discussed we will go with implementation behind a flag. so for now we would go with [https://web-identity.well-know.apexdomain.com/.well-known/web-identity](https://web-identity.well-know.apexdomain.com/.well-known/web-identity).'*  
* Heather:  
  * WG process document shared earlier.  
  * Ajay, feel free to play around with this.  
* Sam:  
  * Need guidance from the IETF on reserving subdomains?  
* Heather:  
  * Checking with the DNS folk about this.  
  * (Has a TAG issue for this already.)

### [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)

* Currently waiting for review and feedback from the Service Worker WG.   
* Heather:  
  * Suresh is still waiting for feedback from the service workers group.  
* Ajay:  
  * Suresh is working with the service workers WG.  
  * A few things on how to specify the service worker … (PS, not sure what is being specified)  
* Heather:  
  * The service worker reviewer is on holiday this week.  
* Sam:  
  * Also, Ajay, do not worry about the spec PR. Work behind a flag and try to implement.  
  * Can improve the spec PR from the implementation experience.   
* Ajay:  
  * If we have feature flags for subdomain and service worker, if it looks good, how long does it take to get consensus for the implementation, and when does it become the default in Chromium?  
* Sam:  
  * All the way to origin trials without merging spec PR.  
  * Implement behind the flag, then all the way to Origin Trials, and then developers give us real feedback from production use.  
    * Most of the hard questions come from the Origin Trials.  
  * Chrome releases features, getting implementation experience first.   
* Heather:  
  * There are other browsers and other implementers who do not follow the Blink process. So take the Blink process as guidance, but not an absolute.  
* Emelia:  
  * Is there a tracking issue in general for FedCM Core? (Other than [https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-(Consensus-Blockers-for-CR)](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\))?)   
    * Trying to figure out blockers on the IdP registration side to get into FedCM core.  
* Heather:  
  * There is something similar for the DC API: [https://github.com/orgs/w3c-fedid/projects/1](https://github.com/orgs/w3c-fedid/projects/1)  
    * Could be an interesting model for FedCM.  
* Emelia:  
  * GitHub Projects would be perfect for this.  
  * Want to figure out how to land IdP registration.  
* Heather:  
  * Next meeting May 19th.  
  * (Heather in EIC in Berlin).

## AOB

* 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Phil Smart (Shibboleth/Jisc)  
* Christian Biesinger (Google Chrome)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Emelia Smith (she/her)  
* Yi Gu (Google Chrome)  
* [bumblefudge.com](http://bumblefudge.com) (NLNet)  
* Achim Schlosser (Bertelsmann)