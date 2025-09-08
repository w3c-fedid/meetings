# FedID WG Telecon \- DC API Series A, 2025-09-08

* Moderators: Heather Flanagan

* Scribe: Wendy, Helen

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?   
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (40 minutes)  
  * [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)  
  * [Redo security considerations \#360](https://github.com/w3c-fedid/digital-credentials/issues/360)  
  * [Add a11y guidance for user agents \#238](https://github.com/w3c-fedid/digital-credentials/pull/238)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (10 minutes)

* Tim: update on [digitalcredentials.dev](https://digitalcredentials.dev/). Starting to get lots of good content, will be looking for help in this open source work. Please reach out\! 

## DC API Issues

### [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)

* Tim: I want this to stay on the agenda until we reach consensus. Given the points raised by Nick and others, if it’s not enforceable then why are we doing it? Let’s discuss.  
* Heather: Any thoughts?  
* Brian: A registry can serve a lot of different purposes from governance on S\&P, conflict avoidance on protocols, discoverability of what might be available.   
* Tim: I am in favor of dropping the registry as it is defined today. I agree with Brian there are many different ways to do registries (and don’t necessarily disagree with others)  
* Nick: I thought last time we discussed, we suggested we could document which privacy considerations we could address through protocols and which we can’t. If we get rid of that, where do we address those privacy issues? Or we can keep registry, make it meaningful, and decide which privacy issues are addressed at web level.  
* Heather: Hearing some values for registries; we need to revise text to what we think registry can do. It’s not about enforcement, but about signaling.   
* Joe: I think it wouldn’t be in our interest to have a one-time review of a protocol and have an analysis that says it respects privacy, as protocol/usage may change over time. WHen do we re-review?  
* Tim: Beforehand, what do those designations mean? Carry weight, or just an informational document?  
* Nick: At W3C generally, I agree we need ongoing processes for evaluation, not just for registries, but also APIs and protocols, i.e., not just when there happens to be a new spec version. What I see in notes and hear from Tim, we should have implementation requirements of what we expect from protocols. Write it down, don't just make assumptions. Maybe our work is implementation requirements.   
* Tim: To be very concrete, implementation requirements on whom? UA?   
* Nick: I think what we’re talking about is requirements for exchange protocols, e.g., does it support selective disclosure, communicate privacy information, make sure verifiers are authenticated? They’d be reviewable things.  
* Christian: I fear it would be hard to do that in terms of requirements on the protocol level, e.g., openID for VP and ISO ... general-purpose protocols, privacy depends on the ecosystem  
* Nick: I think John summarized in last meeting, registry can say this could be privacy preserving if all layers do their thing  
* Christian: So it’s describing availability, not necessarily how it’s used?  
* Matt: Lots of this convo seems centered on whether or not a protocol allows for abuse of PII contained in these systems, when it might be about the wallet. Are the privacy concerns the same for punch cards at your local coffee shop as for a driver’s license? If we think forward, what are the majority of use cases we see coming down the pipe? High-privilege documents like mDL and PID, or low-privilege like punch cards? Different needs and privacy concerns for different use cases. If the registry is focused on the PII heavy use cases, it may convey very different signals. Whereas the common use case may not be these PII heavy examples.  
* Nick: Current privacy considerations section has several subsections relating to the exchange protocol [https://www.w3.org/TR/digital-credentials/\#exchange-protocol-considerations-for-user-privacy](https://www.w3.org/TR/digital-credentials/#exchange-protocol-considerations-for-user-privacy) Probably especially concerning regarding govt-issued. In other sections, we note the spectrum of privacy.  
* Matt: Is this registry aiming to document the whole spectrum of privacy?  
* Nick: Exchange considerations can cover a broad range. There’s functionality you can use in some cases and not in others.  
* Ryan: One of the concerns I might have is that we have two presentation protocols and one issuance protocol that exist today. Much depends on how the ecosystem implements. A privacy-preserving implementation for OpenID for VP is possible, but little transparency into whether it is in use. Does it give value if we say these protocols might be able to offer privacy but we don’t know because we don’t have visibility?  
* Christian: Tons of options in OpenID4VP, and we have HAIP (the high assurance interop profile) that focuses on those high assurance use cases — which would you put into the registry?  
* Nick: That comes up often, the objection of a false sense of security. We do privacy and security reviews on all W3C specs, and even if we do a solid review, we can’t cover all use cases and abuse possibilities, but I don’t think the answer is to throw up our hands and skip reviews.  
* Matt: Nick, I think I agree that not talking about it isn’t the solution. These are real privacy concerns that will exist for all protocols, now and in future. Feels like a long-term user-education journey. Would our time be better spent helping to educate people on what to look for in their own evaluations?  
* \[from chat: Ryan: I also want to be clear that there are clear issues we need to address but I don't know that a registry is necessarily going to produce a result that is truly impactful if there is no real enforcement mechanism.\]  
* Joe: There’s a difference between what I think is a moral and ethical obligation to profile our own work, and reviewing someone else’s work, as we might be in this registry.  
* Matt: Reviewing implementations is pretty good as a name-and-shame tactic, better if we can get out ahead of the violations of privacy  
* Nick: Sometimes we get into a situation where, because there are many moving pieces, everyone can say “it’s someone else’s responsibility to fix that,” and the likely outcome is that the user doesn’t get protected and they pay the price. That’s what I’m trying to avoid. Trying to write down which things are being addressed where. No guarantee that protocols or implementations will provide the capability, but better than just finger-pointing to an unknown elsewhere.  
* Ryan from chat: I would argue that there are a lot of jurisdictions (EU) for example that will state that this is their responsibility and they are taking action on it.  
* David: Elsewhere, e.g., IETF privacypass, you have a complete system for specific purposes. If you really want to have privacy guarantees, it has to be about the whole system.  
* Tim: If we can answer the question of whether this is enforceable or not, it helps inform whether we should do this registry in the spec versus somewhere else.   
* Lee: Agree with Tim. Pragmatically there are 2 protocols out there (openid4vp and annexc) that are already v1 and already supported. Whether they end up in the registry or not, browsers are probably gonna support them. We are also not gonna have much saying about its specification in this group, and pragmatically we the browsers will have to support it. Pragmatically speaking, the registry isn’t enforceable. It doesn’t stop the W3C group from making reviews and recommendations though.  
* Heather: Everything I’m hearing sounds like things we need to capture, that it’s an ecosystem-level challenge, that we, as part of the ecosystem, need to do what we can. That doesn't sound to me like a registry-shaped problem. Privacy considerations. Elsewhere, there’s a standards-level document series, and then another set of documents about different ways to implement those standards, e.g., NIST 800 and 1800\. I’d like to say we put this info into our privacy considerations, recognizing that some things end up in their own profile, and suggest that unless something changes, we’re not going to do a registry. I’ll put that proposal to the list to include those who come to the series B call.   
* Ryan from chat: I think the non-normative privacy analysis with defined pathways to the owning entities could be more valuable.  
* Nick: our experience has been that spending all of our work on non-normative privacy guidance doesn't have significant impact. Maybe the EU will take some responsibility for implementations regarding the subset of European government-issued identity documents. some users live outside of the EU, or use credentials other than EUDI ones

### [Redo security considerations \#360](https://github.com/w3c-fedid/digital-credentials/issues/360)

* Wendy: Simone proposed discussion with SING at TPAC; let’s keep discussing it in the issue to do work in the interim. 

### [Add a11y guidance for user agents \#238](https://github.com/w3c-fedid/digital-credentials/pull/238)

* Matt: Already discussed in the previous meeting. Ready to move forward.

## Any Other Business (AOB)

* Heather: Back to registry, I’ll write up my thoughts and send around  
* Lee: (to Nick’s concern around non-normative privacy analysis not having significant impact) There are normative requirements elsewhere. As to layering, maybe we point there, not make normative fixes here. Those specs can also be worked on and normatively influenced.   
* Ryan from chat: And I think if an analysis here finds a recommendation they can engage with those other SDOs to drive a result. There is sufficient overlap that it seems like a real privacy issue could be driven and have positive outcomes in those other bodies. They also do care about these issues.  
* Matt: Do we need to start exploring conversations around verifier authentication? Could that help drive privacy? Not entirely on the browser, e.g., external legal systems. How can we incorporate strengths elsewhere into these convos?  
* Tim: Right, it’s not on the browser at all. It’s on the (e.g., openid4vp) protocol layer  
* Christian: We can’t prevent over-asking on the protocol level, but could consider something like certificate transparency that allows detection and monitoring of abuse  
* Lee: I think if you went to the DCP group and asked the same question, you’d get engagement

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Wendy Seltzer (co-chair)  
* Ryan Galluzzo (NIST)  
* Marian Harbach (Google Chrome)  
* Helen Qin (Google Android)  
* Lee Campbell (Google Android)  
* Tim Cappalli (Okta)  
* Christian Bormann (SprinD)  
* Bjorn Hjelm (Yubico)  
* Matthew Miller (Cisco)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Nick Doty (CDT)  
* Ketan Mehta (NIST)  
* Marian Harbach  
* Ryan Watkins  
* Rene Leveille  
* Joe Andrieu  
* David Waite (Ping Identity)