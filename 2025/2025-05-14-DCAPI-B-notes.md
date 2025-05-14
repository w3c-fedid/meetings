# FedID WG Telecon — DC API Series B, 2025-05-14

* Moderators: Heather Flanagan

* Scribe: Matthew Miller, Nick Doty

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?   
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues (10 minutes each)  
  * [\[spec\] write privacy considerations \#183](https://github.com/w3c-fedid/digital-credentials/issues/183)  
  * [Add isProtocolSupportedByClient static method \#219](https://github.com/w3c-fedid/digital-credentials/issues/219)  
* DC API PRs (10 minutes each)  
  * [Link to registery inclusion criteria definitions \#236](https://github.com/w3c-fedid/digital-credentials/pull/236)  
  * [Fix links to request field to use the new format in the register inclusion criteria \#235](https://github.com/w3c-fedid/digital-credentials/pull/235)  
  * [Add isProtocolSupportedByClient static method \#221](https://github.com/w3c-fedid/digital-credentials/pull/221)  
* Any Other Business (AOB)

# Notes

## Administrivia

* Heather: Thank you to Matt and Nick for scribing! Also, usual administrivia reminders. 

## Ecosystem Updates

* Marcos: A patch to WebKit includes the validation side of mdoc, stubs for other validations. No UI yet, but this should get close to Google’s implementation for future interop  
* Nick: Would be helpful to test, see how DC API is being used in the wild. Are there any insights that can be shared on this? Some people want to test but aren’t in regions where governments are issuing such credentials?  
  * Rick: No issuer in Canada either, but there are some test apps that let you issue self-signed credentials  
    * [https://apps.multipaz.org/](https://apps.multipaz.org/) (OWF)  
    * [https://digital-credentials.dev/](https://digital-credentials.dev/)  
  * Nick: In Chrome can I use this test wallet?  
    * Rick: Can’t speak to the Android side but there’s nothing in Chrome that’s wallet-specific. Early days of DC API may have whitelisted a specific APK name, but that’s not longer the case  
* Heather: EIC was last week. Relevant OIDF working groups met, there may be meaningful insights in their meeting notes  
* Rick: Regarding testing ZKPs, Google is working on landing support in the Multipaz wallet above. Not yet landed, but there’s a path to granting people access to a preview build

## DC API Issues (10 minutes each)

### [\[spec\] write privacy considerations \#183](https://github.com/w3c-fedid/digital-credentials/issues/183)

* Rick: There’s a lot of work to fill out these sections. Need to get the Chrome team to help out more here. Johann has graciously agreed to step in and help move this forward.  
* Tim: We agreed we could move forward with the outline, this feels like an 11th-hour reveal. Manu helped get the identified issues into the outline.  
* Marcos: It would be useful to get a discrete list from Martin to then talk with Johann about.  
* Nick: These issues have been raised for quite some time. It was useful to have the headings at the CG level. But for TAG review, etc., it would be better to have these sections spelled out.  
* Wendy: As co-chair, I don’t feel like we’re being blindsided here. Consideration in the WG is different than in the CG; the audience is different. It’s our obligation here to address concerns whenever they come up. Our hope as chairs is to work through these issues so there’s a WG reference point for horizontal reviewers to review.  
* Johann: It’s necessary to have these sections written out.  
* Ben: Trying to have the context in the FPWD is important before seeking review. If the goal is for the FPWD to be more formally referenced outside W3C, it should at the very least acknowledge the issues, even if it doesn’t try to fully solve them. Otherwise, it’s leaving a potentially dangerous thing out there for people to misuse.  
* Heather: Just a reminder that security and privacy sections aren’t normative.  
* Marcos: For the privacy side, we can make them normative. Let’s work on this stuff and get the content into the spec.  
* Rick: The big challenge with the privacy and security stuff is that it’s not mature enough. For a lot of the threats, we’re seeing them happen in other parts of the ecosystem. There’s a bit of a chicken and egg thing here.  
* Simone: The W3C process says the group needs to agree on the content of the FPWD. We can send the FPWD, then five days later cut a new WD and continue working on that for asking reviews. Procedurally our target is to have a good draft. For Security we also received a DC API formal verification.  
* Nick: Maybe privacy and security issues will go beyond the one spec. One option is to adopt a separate deliverable that identifies all of these issues, then reference this separate document in the DC API spec. Certain implementers wanted to move more quickly on the API than to define such a doc. If that’s right then we can open all the issues in the spec and try to find places for such guidance.  
* Rick: Main concern is there are many groups analyzing the security and privacy in this space. OIDF, Europe, W3C VS group…it may not make sense for one more group, especially one without as many stakeholders present, to jump into the fray here. These are hard, complex problems and five separate docs from three standards groups won’t help especially if there is conflicting guidance across the docs.  
* Marcos: Procedurally we have registration of the protocols when we’d check what’s going on at that layer. It would be better to keep things in a single place, with security and privacy requirements asserted at the time of registry submission. Fewer groups is better.  
* Heather: DC API needs to cover issues with the API, not with the wider ecosystem. However I can see the WG committing to reviewing docs describing threat modeling as being considered by other groups. Can we make that a work item?  
* Tim: Work items are great, but not if it blocks other work items.  
  * Heather: Yes, if we have that as a work item, I’d be more willing to unblock the FPWD because we can’t get out of doing it.  
* Simone: Expressing support for adopting the document described in the charter and in chat  
  * *Nick (via chat): I'm fine with broader analysis in Privacy WG / Security Interest Group, and work through all the relevant issues in digital-credentials API…charter includes "A Threat Model of Digital Credentials-related technologies concerning security, privacy, and human rights." if this WG wants to*  
* Nick: I was trying to get us to commit to filling these sections out to get the spec through TAG, horizontal reviews.  
* Heather: Wendy and I will confer to discuss the best path forward, aim to have something for the group to consider in the next day or two.

### [Add isProtocolSupportedByClient static method \#219](https://github.com/w3c-fedid/digital-credentials/issues/219)

* What else is needed?  
* Tim: reflection of agreement at f2f.  
* Matthew: 2 competing approaches given multiple protocols in the wild. useful for developers to know when to use one protocol over another. currently have two options:   
  * isProtocolSupportedByClient – developer can test whether the UA supports it, before making the request  
  * alternative (via Marcos), static property `knownProtocols` (a list, but maybe needs a special glob “\*”) [https://github.com/w3c-fedid/digital-credentials/issues/168](https://github.com/w3c-fedid/digital-credentials/issues/168)   
* Marcos: for developer ergonomics, a set that the developer can filter using JavaScript set operations. But the goals are the same. that the UA can pass it through to the wallet picker.  
* Tim: third proposal of getClientCapabilities, which would allow other forms of developer detection, which we didn’t do but learned to enjoy in WebAuthn. list doesn’t work for Chrome because of returning ‘anything’/\*  
* Matt: prefer the boolean test pattern because of the need for asterisk/magic value, more ergonomic for developers to test specific protocol identifiers.  
* Lee: \+1. Maybe the name is a bit weird.  
* Marcos: return a list but only things that are in the registry (so that Chrome doesn’t need to use special \* value).  
* Nick: I’m fine with the basic test approach, questions on the PR.  
* Lee: some things won’t be in the registry, especially when evolving. Currently there’s nothing in the registry.  
* Rick: black box that passes things through, but Chromium also has a risk evaluation and potential ways to intervene. registry will have an impact on risk calculation, UI, prompts, etc. but won’t block protocols from reaching wallets. can offer clues to the user about safety based on the registry, but have an escape hatch.  
* Marcos: static list doesn’t have to be what’s in the registry, just the things that the browser knows about.  
* Lee: But in some cases the Chrome browser won’t know about it.  
* Marcos: you won’t support open hacked protocols that haven’t been built? Rick: Yes, we would pass through even if we’ve never heard of it.  
* Marcos: What's the point of having this API at all? The site can just send multiple simultaneous requests and only one will go through anyway.  
* Matt: not sure we have defined behavior if multiple requests are sent simultaneously.  
* Heather: I don't want to repeat earlier conversation, not sure what new information.  
* Marcos: what do you do if you have multiple is an important issue, which could also help with this problem. ready to propose text for that alternative.  
* Heather: do you have a specific use case for needing to send both versions of a request?  
* Matt: these approaches are a stopgap for semantically identical requests for claim across different protocols; the developer should just throw in what they want.  
* Tim: still value to have this, there’s a cost in crafting and signing both versions of the request, rather than detecting the version and just choosing which.   
* Marcos: Yes, potentially important to know ahead of time. Transient activation timeout could be a problem if you fetch to get a signed response from the server.  
* Tim: early problem in passkeys, for sites to check for capability until it reaches a certain fraction of usage before they actually turn on the functionality for that workflow.

## DC API PRs (10 minutes each)

### [Link to registry inclusion criteria definitions \#236](https://github.com/w3c-fedid/digital-credentials/pull/236)

* ran out of time

### [Fix links to request field to use the new format in the register inclusion criteria \#235](https://github.com/w3c-fedid/digital-credentials/pull/235)

* ran out of time

### [Add isProtocolSupportedByClient static method \#221](https://github.com/w3c-fedid/digital-credentials/pull/221)

* ran out of time



## Any Other Business (AOB)

Heather: please review the PRs that were marked for agenda today.  
Heather and Wendy will get back to the group with a proposal regarding privacy considerations.  
Heather will clear out agenda+ tags for the items we discussed today. Add the label if new things come up later this week. Conflict for FIDO people for Monday; will figure out via Slack.

Heather and Wendy will share thoughts on scheduling; in Northern hemisphere summer there will be people unavailable.



# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting)  
* Nick Doty (CDT)  
* Rick Byers (Google Chrome)  
* Ketan Mehta (NIST)  
* Wendy Seltzer  
* Matthew Miller (Cisco)  
* Johann Hofmann (Google Chrome)  
* Simone Onofri (W3C)  
* Bjorn Hjelm (Yubico)  
* Brian Campbell (Ping)  
* Tim Cappalli (Okta)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Helen Qin (Google Android)  
* Lee Campbell (Google Android)  
* Marcos Caceres (Apple)
