# FedID WG/CG Telecon, 2026-06-02

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
* Discussion (45 minutes)  
  * [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)  
  * [FedCM facilitates vendor lock-in \#827](https://github.com/w3c-fedid/FedCM/issues/827)  
  * Moving IdP Registration to Phase 2?  
* Any Other Business (AOB)

# Notes

## Administrivia

* W3C Code of Conduct

## 

## Ecosystem Updates (10 minutes)

* Heather:  
  * Any updates of FedCM in the wild?  
* Sam:  
  * Stuff being pushed out in Chrome:   
    * 148 in Chrome stable has Agentic Federated Login proposal (Origin Trials)  
    * 150 will contain EVP, as an extension of FedCM (end of June, for Origin Trials)  
      * Version already working in Chrome Canary  
    * After 150, native IdPs. Connecting FedCM to Android apps for verified phone numbers  
* Bjorn  
  * How does verify by phone number work?  
  * Maybe a link?  
* Sam:  
  * We do not know yet, prototype stage  
  * Called [Native IdPs](https://github.com/fedidcg/native-app-idps). Android specific integration, would need iOS version too.  
    * Uses FedCM continuation API. Allows an IdP to open a popup window after account choosing. Usually used for OAuth scope consent from the user.   
    * Rather than a browser popup window, open an Android Intent instead. So the native app could get access to a verified phone number and pass it back to the RP.  
      * (Which it gets from the SIM card?)  
* Bjorn  
  * The only one that knows the number is the phone network, not directly the device—it could be out of date.  
    * Possible window for stealing phone number  
* Sam:  
  * Browser responsibility is only to open the Intent. The IdP then has to do the right thing after that.   
* Bjorn:  
  * Phone receives a copy, you can not rely on it as a truth  
* Sam:  
  * Working with Apple, together. (Telcos also have to change.)  
* Heather:  
  * Maybe a side conversation on that if required.  
* 

## 

## Discussion (45 minutes)

### [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)

From last meeting \- Next Steps

* Suresh to update GitHub issue with agreed decisions  
  * Document security property resolutions  
  * Capture redirect handling changes  
  * Note service worker partitioning decision  
* Investigate Microsoft IDP requirements  
  * Check re-authentication frequency patterns  
    * In Microsoft Entra, sign-in frequency defaults to 90 days unless a tenant overrides it. So, if the security posture has not changed, Entra generally does not ask the user to provide credentials again within that 90-day window.  
  * Determine existing service worker usage  
  * Clarify fallback scenario handling  
* Design fallback mechanisms for service worker failures  
  * Bad deployment recovery process  
  * Eviction scenario handling  
  * Best effort vs guaranteed service worker operation model  
* Update from Suresh:  
  * Followed up on asking MS IdP a few questions  
  * Discussions on best course and fallback would be a good start to the meeting  
* Heather:  
  * Any thoughts on fallback mechanisms  
* Suresh:  
  * Now we have an IdP from MS, they could help us on best course. In case the service worker approach does not work  
* Ajay:  
  * Concern: user authenticates, the sign in frequency for Entra is 90 days, the user might not see sign in page for another 90 days (unless policy defined). So if user authentications once, the IdP then does the Service Worker registrations, FedCM calls token endpoint afterwards, so might not visit service worker page again—so how do we prevent it from becoming stale and out of date?  
  * A staged rollout might be possible.  
* Sam:  
  * AJay, are you using passive mode or active mode?  
* Ajay:  
  * Combination, but same problem in either  
* Christian:  
  * With active mode, if no accounts list, we go to the login page, where you could install the service worker  
* Nicolás:  
  * Thought the SW endpoint was specified somewhere?  
* Christian  
  * No, IdP installs it.  
  * Problem with specifying SW in FedCM config, it adds complexity in the FedCM process.   
* Nicolás:  
  * How often are SW evicted. How often do we need to install the SW  
* Ben:  
  * Another case, if you rollout (staged) and you want to revert that, how do you do a quick change, how do you trigger that flow?  
  * The update can happen in the background, on a lag, but something faster than 24 hours may need a different mechanism  
* Ajay:  
  * This sits on a critical path, all requests to get a Token would go through the SW. So it needs to be reliable 100%.  
* Ben:  
  * In the non FedCM case with Fetch event, a broken fetch event could block the SW. In the FedCM case, there could be a fallback to a webpage that installs it?  
    * Timeout, 500 errors etc.  
* Nicolás:  
  * When it is doing the regular fetch?  
* Ben:  
  * Fallback is a page that can run JS that can change SW if needed.  
  * Or a header based mechanism of install  
  * Would need to be specified either way  
  * And timing would need to be thought about  
  * If FedCM works as it should, user will not often see an IdP page, so less chance to explicitly update SWs, relies on passive mechanism.   
* Suresh:  
  * (did not catch)  
* Ajay:  
  * Perhaps a header mechanism that there is an update could work to signal to FedCM?  
* Suresh:  
  * Same problems around timing?  
  * Takes time for the SW to register  
* Ben:  
  * We could have a well-known file that says there is a SW. When SW works there is an API that says this is the version of the SW I am installing, so FedCM can make a decision about whether to use it or not. IdP could then convey a new version to FedCM via the well-known file, and FedCM would stop using the legacy path.  
    * A coordination channel  
    * IdP will would need to support the legacy path  
    * Maybe easier, but more complexity.   
    * Well-known sounds better here because you are already reading it  
* Nicolás:  
  * Is there a native SW update mechanism? Does that not already exist  
* Ben:  
  * When SW sends a functional event, it does a soft update in the background  
    * Asynch in the background, does not complete until current SW shutdown  
      * So the new SW script is not active until the current SW is shutdown. So a best-effort kind of update  
    * No real concept of SW version numbers, so evict what is there, not based on some kind of semantic version number  
* Ajay:  
  * In this case, the IdP would play around with the well-known file if they wanted to update a SW. FedCM would then take care of the installation part?  
* Ben:  
  * Was suggesting well-know would do one or two things:  
    * (not sure how to do staged rollout without cookies)  
    * Do not want users to go through a web page to register a service worker  
    * Fast eviction mechanism, only route through SW if valid version   
    * Normal update mechanism, no waiting for it, no guarantees it was up to date, but things need to work even if the latest version is not installed.  
      * FedCM could perhaps trigger it, but not wait for it  
    * Maybe a mechanism that a SW tells FedCM which version it is  
  * Do we need, next request definitely requires a service worker or not?  
* Christian:  
  * Has to go through a service worker or fail? (PS. not 100% that was the logic suggested. CHECK)  
* Ajay:  
  * Would not roll out updates to well-known to all instances at once, so they might have different versions until gradually rolled out. But FedCM would need to handle installation  
  * How do we update the config.json file?  
* Nicolás  
  * Can not do this in a gradual fashion, that would break things?  
* Sam:  
  * Well-known only reference to config and accounts endpoints  
  * So if changes, you must support old and new until full rollout.   
  * So SW URL could be in there too, but IdP needs to respond to both old and new URL  
* Emelia:  
  * Usually SW URL would be content hashed, so not sure SW URL in config or well-known makes sense as build during the application build  
* Christian:  
  * Could build SW then deploy well-known file  
* Emelia:  
  * Two step update. Build assets then update config file.   
* Ben:  
  * Expectation is that people do no hash the script URL  
    * If you do, you can not have automatic updates from the SW system  
    * Only manual updates  
    * SW specs update based on the same URL, does limit HTTP cache.   
    * SW request is made with cookies, so could use user identity at SW level  
* Heather  
  * Well-known is interesting but might not have all the properties we need  
  * (another, sorry, missed)  
* Ben:  
  * Needs evicted path  
  * Staged rollout path  
  * Other use cases and scenarios that need documentation. How do SW meet these use cases.  
  * Do we need predictable behaviour based on SW version  
* Heather:  
  * Suresh can you add that to the i[n progress docs?](https://github.com/w3c-fedid/FedCM/issues/833)  
  * (Response) Suresh said yes, and Ajay said he can help.  
* Sam:  
  * Alex Russell in MS is a SW expert, perhaps ask with him  
* Heather:  
  * Should we have another call on this in the week  
  * (Response)   
    * Suresh: discussion could happen in the docs in the issues link  
    * Ajay: could we have another next week, will try to get everything together next week  
* Ben:  
  * Before the whole document is written, float the list of use cases to be considered with the group. 

### [FedCM facilitates vendor lock-in \#827](https://github.com/w3c-fedid/FedCM/issues/827)

* Hold for call on June 15

### Moving IdP Registration to Phase 2?

* Heather:  
  * How close to phase 2 are we for IdP registration?  
  * Sam, you said not quite ready yet?  
* Sam:  
  * A bit fuzzy, but the bar was an end-2-end prototype and everybody is happy.   
    * Browser has it working behind a flag and an RP has it working  
  * Stage 2 we tried to write a spec, but not sure of the formulation of the UI and the shape of the API.  
    * These are not anchored yet unless we have a prototype.  
* Emelia  
  * Thought further along  
  * Experiments that have registration mechanism  
  * Open issue was the config URL needing to be set to ‘any’ ([GitHub issue 26\)](https://github.com/w3c-fedid/idp-registration/issues/26), needs resolving.  
  * As for UX, not got anything soon. Hard to get prototypes for this in a distributed system. Hard to test.  
  * Spec text looks about correct.  
  * IdP should register first before using the status API  
* Sam:  
  * Open question, whether the widget mode is fine?  
* Emelia:  
  * Steering toward auto-fill for the UI. Not sure on integration yet.   
* Sam  
  * If you need auto-fill that would require active development  
* Emelia  
  * Start with active mode  
* Sam  
  * We do not support multi-idp in active mode, so do not support registration API  
* Christian:  
  * UI challenge, if you are not logged in, how do you pick an IdP to log in with  
  * Active mode lets you log in if you’ve not logged in  
* Emelia  
  * I think we would steer toward active mode if we can not get auto-fill  
  * The reference document I have on modes that Sam and I have been working on: [https://docs.google.com/document/d/1wwrSo\_shxWpsiqmQ8wDt9oUAIGh3-dWqpwfjzOFmy\_g/edit?pli=1\&tab=t.0](https://docs.google.com/document/d/1wwrSo_shxWpsiqmQ8wDt9oUAIGh3-dWqpwfjzOFmy_g/edit?pli=1&tab=t.0)   
* Nicolás:  
  * That would need the explainer to be updated. Thought this was passive mode.  
  * We need to understand the user flow we want to achieve, as that (acvtive mode) is not in the explainer  
  * Open questions around what gets fetched when  
  * Agree not close to stage 2 yet  
    * We can work on it, but we did not support active mode for multi-idp  
* Heather:  
  * Not ready for stage 2, but open questions that need more discussion. Going back onto the agenda for the 15th.   
* Emelia  
  * Thought active mode was support.

## AOB

* 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Wendy Seltzer (co-chair)  
* Nicolás Peña Moreno (Google Chrome)  
* Pamela Dingle (Microsoft) \- partial attendance  
* Phil Smart (Shibboleth/Jisc)  
* Sam Goto (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Ajay (Microsoft IDP)  
* Alan Buxey (MyUNiDAYS Ltd.)  
* Emelia S. (funded by Bluesky / Decentralized Social Web)  
* Theo \- @thhck ( Solid CG )  
* Ted Thibodeau Jr (he/ him) (OpenLink Software)  
* Ben Kelly (Meta)  
* Bjorn Hjelm (Yubico)  
* Suresh Potti (Microsoft)   
* George Fletcher (Practical Identity LLC) 

# Regrets

* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* 

