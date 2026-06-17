# FedID WG/CG Telecon, 2026-06-16

* Moderators:  Wendy Seltzer

* Scribe: Emily

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
  * New proposal: [Identity Handler](https://github.com/w3c-fedid/identity-handler) related to [Issue 80](https://github.com/w3c-fedid/FedCM/issues/80), [PR 815](https://github.com/w3c-fedid/FedCM/pull/815)  
* Any Other Business (AOB)

# Notes

## Administrivia

* 

## Ecosystem Updates (10 minutes)

* Emily Lauber will be leaving Microsoft and Sindhoor Grandhi will be on point as Microsoft PM 

## Discussion (40 minutes)

* ### New proposal: [Identity Handler](https://github.com/w3c-fedid/identity-handler) related to [Issue 80](https://github.com/w3c-fedid/FedCM/issues/80), [PR 815](https://github.com/w3c-fedid/FedCM/pull/815)

  * Suresh: Got feedback from core community about Service Worker. Need to have discussions on the registration. Looking for feedback on proposal from Microsoft Identity team. Service Worker is all done with, at least.  
  * Sam: Done with means"solved all the open design questions"? Can you walk us through some of the things anchored?   
  * Suresh: Registration issue is whether the IDP or the UA should be handling registration. If UA does registration, there is an approach based on nonce. Ben also suggested another member available in Service Worker for registration. Feedback from the SW WG that nonce seems to be better in terms of implementation. Need feedback to confirm.   
  * Sam: To clarify, this is when the RP calls FedCM to the IDP silently without user notification? Are these mutually exclusive approaches?   
  * Suresh: ???   
  * Sam: Only do this when the user visits the RP.  
  * Sam: Feedback from Ben that the Service Worker implementation is expensive to run?   
  * Suresh: Some issues when many call the registration API. Two things: installation and activation. "Calling bias" is when activation is ahead of time. Not that expensive, if UA does registration ahead of time. Also, how could they recover from Service Worker? And well-known file updates and how that could happen quickly. Need some feedback though on proposal.  
  * Sam: Declaration of Service Worker happens at the well-known file?   
  * Suresh: Yes.  
  * Sam: How should we think about updates?   
  * Suresh: IDP cache and the IDP will serve from the cache. If the control cache puts a maximum of 30 mins, it looks for the file in cache time limit; otherwise, it picks from the server. Otherwise, question to the working group on whether there is any other control knob for updates?   
  * Sam: Will, have you looked at this?  
  * Will: No, have not.  
  * Suresh: Some discussion with Ajay offline about getting the needs met.  
  * Sam: Have you looked at implementation and how hard this may be?   
  * Suresh: Looked at most of it. Open questions on registration is the thing left to determine the level of effort for registration.  
  * Sam: Might have to change the code that intercepts the call depending on registration.  
  * Suresh: Going to get feedback from the Service Worker group. Going to make bite size seals (?) to push the code. There need to be new APIs to get the FedCM Service Worker pieces together.  
  * Sam: A few steps forward in implementation will give more feedback. Both on browser and IDP side. There is a lot you learn by building parts of the browser and having identity teams try the nascent flow.  
  * Nicolas: Thanks Suresh for putting up the explainer. Wondering if we've already made the decision on the questions in the issue that have been going with comments last week regarding the storage key for the Service Worker used with FedCM.  
  * Suresh: That’s what we were discussing of the two options: nonce and key. Nonce already exists in the storage key. If we go with a different member or a different key, it needs changes in the storage key spec. With the constraints, would prefer to go with nonce.  
  * Nicolas: Can we get guidance from Service Worker people before making the decision? Need Service Worker experts' guidance before going ahead with assuming the proposals are correct.  
  * Suresh: Service Worker expert (name?) liked the approach of nonce but relying more on (Mike West ) another expert from storage key to get opinion on that. Waiting on those folks.   
  * Nic: Mike West was waiting for a concrete explanation of the problem. Didn’t see that on the issue. Need that so we can get feedback.  
  * Suresh: Yes.  
  * Wendy: Are there other places looking for feedback or review within the group here?   
  * Sam: Suggest Suresh kick off a TAG review. Blink process will require TAG review and that could help. And then also file Mozilla and WebKit’s standards positions on whether or not this could be an acceptable position for them as well. It is kinda a checkpoint of finding enough of a baseline proposal to run with for TAG and other browsers' feedback. Potential next steps are that and implementation experience.  
  * Sam: Assume already sent an intent to prototype?   
  * Suresh: Yes, already sent.  
  * Sam: Blink next process is a dev trial behind a flag once there is some implementation. That’s a good time for TAG review and other browsers positions.  
  * Suresh: Regarding APEX domain changes of the discovery. The well-known discovery. The changes are in Chrome & Edge. Has the IDP team tested the path?   
  * Will: Not sure. Question for Ajay.   
  * Sam: That is an independent question from Service Worker?   
  * Suresh: Yes.  
  * Sam: Have we settled the prioritization of the requests? One after the other? In parallel?   
  * Suresh: First to subdomain well-known, and then fall back to APEX domain.  
  * Sam: That proposal seems reasonable but will have to convince existing IDPs to redeploy; otherwise, it can add latency to their existing calls, right? There isn’t an IDP today that has the subdomain in well-known file. So if this change is enabled today, it will add latency and retrograde performance, because these well-known files don’t exist today.  
  * Suresh: Correct.  
  * Sam: Action item to see whether this fallback order works for Google IDP and Shopify, since it requires a re-deploy of the well-known file.   
* 

## Any Other Business (AOB)

* TPAC joint session?   
  * Sam: Jesse, do you want to chat more while Emelia is here?   
  * Jesse: Within the Solid CG and Linked Web Storage WG, we've been planning TPAC sessions including where it would be relevant to have cross-cutting groups. Where it could be is Identity. Linked Web Storage is leaning on SIDs coming out of Decentralized Identifier (DID) Working Group. Seems to be a few groups focusing on Identity and authentication on the web. Proposed to have a joint session across those groups to increase visibility and ensure we aren’t doing things in silos. Discussion more long term is how we can more systematically work together across groups   
  * Emelia: Could introduce you to the Social Web (SWI) CG & WG. They run a joint meeting like the FedCM one. Two different meetings at Europe and US time.   
  * Jessse: Fantastic. After this call, will send an email to chairs of FedID, Linked Web Storage, Social Web, and Solid to propose a joint session before TPAC call for closed groups closes tomorrow.  
  * Sam: Usually the cross cutting sessions happen at breakout, but up to you.  
  * Jesse: We're sourcing a joint session, but breakouts are easier. So will have a chat about that.   
  * Ted: Breakout is generally smaller groups and shorter timespace and not so much planning in advance. Joint sessions between working groups can be very helpful for groups that didn’t realize they had that interaction/overlap, and makes it easier for cross-pollination to take place. (Jesse thumbs up) 

* ### UX modes working with the API

  * Emelia: Out of bounds A or B discussion is it seems like certain FedCM UX moves are not supported for matching any IDP based on types. Various UX flows didn’t support that for some reason. Seems like any UX flows should support all the sourcing.  
  * Sam: There is passive and active mode. Passive mode doesn’t require a user activation, is called on a page load. Active mode is intended to be used when user activation is required. Active mode doesn’t yet support multiple IDPs or registered IDPs. Haven’t figured out how to manage the UX of logging out, nor how to manage when there is no registered IDP at all, without revealing to RP what is signed in   
  * Emelia: Not following why the UX should change if there are multiple IDPs.  
  * Sam: For registered IDPs, one of the use cases we don’t know how to solve is when you call active mode, but there are no previously registered IDPs at all.   
  * Emelia: You’d have to bail out. Can’t do anything here without a registered account, unless there is some fallback way for IDPs to show a register button.  
  * Sam: Ran into the issue of revealing to RPs whether or not the user has a registered account at that IDP.  
  * Sam: Debated account picker also showing IDPs without an account or active session. with. It wasn’t so much that we didn't know what the UX looked like, but a lack of demand. The registered IDPs add an extra bit of UX complexity whereas passive mode doesn’t have that problem. Semantics: If you don’t have an IDP, we don’t resolve the promise.  
  * Nicolas: Registration suggestion is to start talking about what is the desired UX? And then can see that’s what we want, how do we achieve it, are there concerns with that? Don’t have active mode multiple IDPs for multiple reasons. Don’t think it’s as simple as a need to fit all UX modes into everything. And then adapt whatever API to achieve that  
  * Emelia: Don’t think it makes sense to focus on potential adopters who might be here, especially in a decentralized domain where people have many. Instead focus on where in the spec is the language to match this up.   
  * Sam: There is language in the spec that says multiple IDPs are not supported in active mode   
  * Emelia: Reject the promise, if it’s multiple IDPs or active mode. Doesn’t that disclose to the RP that they have multiple IDPs logged in?   
  * Nicolas: No, the number of IDPs is based on the RP’s request. It's not about how many the user is logged in to; it’s based on the call.  
  * Emelia: So it’s an instant rejection…

* ### [https://github.com/w3c-fedid/FedCM/issues/827](https://github.com/w3c-fedid/FedCM/issues/827) 

  * Will: The way vendor migrations work for every product on the internet is that you set up side-by-side deployments, and direct traffic from one to the other. FedCM makes that impossible. You can’t have multiple well-known files \*and\* direct traffic, it would be a hard cut-over of incompatible APIs, which is a hard engineering challenge. Don’t have solutions here apart from multiple well-known files in the APEX domains. Things that encourage vendor lock-in need to be fixed.  
  * Sam: Can you expand more? The well-known file is derived from the config file?  
  * Will: Example of Wal-mart. You are paying Fat Cow to do your email for you, and have [mail.walmart.com](http://mail.walmart.com). but then you change to Proton. You set up an IMAP, and change the CNAME to point to [email.walmart.com](http://email.walmart.com). The requirement to have something in the APEX (walmart.com) kills that because you can only have one file.  
  * Emelia: Wouldn’t multiple IDPs help with this migration scenario?   
  * Will: You can’t, because there is only one in the walmart.com well-known file. They would both be on Walmart's domain.  
  * Will: The way enterprise (B2B) works, you pay someone to operate an IDP for you, just as you pay someone to support mail, chatbot, etc., for you. The way you do that is you give an external entity a portion of your domain. You don’t set up a domain for each vendor that operates a portion of your business for you.   
  * Emelia: When I’ve done B2B, it has domains of auth.APEX. And you could register multiple IDPs to switch between.  
  * Will: FedCM does not allow you to have multiple auth's because it only allows you to have one in the well-known file.   
  * Wendy: I’m hearing you say difficult migrations when all are under the top level domain, but possible to use a different pattern with a second top-level (e.g., auth-migration.example) .  
  * Will: CNAMEs as being the common path where you pay someone to operate a service within your domain using CNAMEs. If you can’t operate two at once under   
  * Sam: Losing at email, because can’t you only have one email service provider at once?   
  * Emelia: Can only do it if one supports relaying to the other.  
  * Will: Common pattern to bridge the gap between the vendors you’re switching between.  
  * Sam: That is possible with existing structures where there are accounts pulled from multiple subdomains and get accounts from both. There is a single place that a server goes to send and receive email from the domain, because there is only one global record that comes from the APEX.   
  * Ted: That’s not accurate that you can only have one MX record or IP address per APEX.  
  * Will: Everyone did this recently with the on-prem to cloud migration for mail.  
  * Sam: Maybe I am misunderstanding how email works. Let’s schedule another time for CG call and we can go over it. If it works for mail, could we have a similar mechanism for FedCM?  
    Will: The requirement to have only one domain in the APEX means it’s not possible to have multiple vendors. Suggestion is to remove the limit of 1 and have a small number.  
  * Sam: Matter of entropy. Can tolerate a small number without adding too much entropy. Do think you can have a small number of entries while maintaining the privacy suggestions?  
  * Will: Similar to mail, if you can have a small number before it reasonably fails the DNS record pull.  
  * Sam: Happy to pick this up again.  
  * Will: Can do async as well.

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* Emelia Smith  
* Jesse Wright (Open Data Institute / Solid)  
* Phil Smart (Shibboleth/Jisc)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Emily Lauber (Microsoft Identity)  
* Sindhoor Grandhi (Microsoft Identity)  
* Sam Goto  
* Nicolas Pena Moreno  
* Isaiah Inuwa  
* Yi Gu  
* zahra
