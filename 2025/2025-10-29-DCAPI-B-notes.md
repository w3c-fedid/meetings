# FedID WG Telecon — DC API Series B, 2025-10-29

* Moderators: Heather Flanagan

* Scribe: 

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (5 minutes)  
* TPAC Planning (5 minutes)  
  * [Draft agenda](https://docs.google.com/document/d/1KWzykDBBfD67fQrJXFPlQGe6tWSblY6VDK3jmyMMfYY/edit?usp=sharing)  
* Ecosystem Updates (5 minutes)  
* DC API Issues & PRs (40 minutes)  
  * [Make user mediation implicit and always required \#392](https://github.com/w3c-fedid/digital-credentials/pull/392)  
  * [Add terminology section, merge in Model \#387](https://github.com/w3c-fedid/digital-credentials/pull/387)  
  * [Define Digital Wallet \#386](https://github.com/w3c-fedid/digital-credentials/pull/386)  
  * [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)  
* Any Other Business (AOB)


# Notes 

## Administrivia

* 

## Ecosystem Updates

* 

## TPAC Planning

* Heather: this is the main item I want to cover on this call, given the attendees  
* Lee: Biggest issue is the registry  
* Wendy: I want to hear more about the privacy considerations that would have otherwise been answered by reviewing the protocols going through the DC API  
* Tim: if clients are free to use items outside the registry, that’s still the main issue. Note that Simone submitted a comment on \- [https://github.com/w3c-fedid/digital-credentials/pull/376\#issuecomment-3412783300](https://github.com/w3c-fedid/digital-credentials/pull/376#issuecomment-3412783300)

* ## Simone: Our charter says protocol-agnostic, suggesting registry should be the way to do the sorting. Opportunity for a field in the registry to note privacy features. Use the implementation requirements and public shaming through a registry field to get privacy. 

* ## Ted: One of the problems with a registry with non-collision, non-duplication is you set things up for squatting, first-come-first-served invites squatters; other rules require lots of work and judgment calls. That’s an argument against using registry at all. 

* Tim: To Simone, EME has implementation requirements, no registry, and required-to-implement protocol.   
* Simone: we can’t use implementation requirements to gate the registry, but having them separately.  
* Wendy: Let’s write up our open points in the registry issue so we can tee up a productive TPAC discussion to reach conclusion and reasoned explanation. [Is a registry needed? · Issue \#345 · w3c-fedid/digital-credentials](https://github.com/w3c-fedid/digital-credentials/issues/345)	  
* Heather: We’re also talking to Web Payments, Ian asked for updates from chairs and group

## DC API PRs and Issues

With the group on the call, decision to go to discussion of registry.

### [Make user mediation implicit and always required \#392](https://github.com/w3c-fedid/digital-credentials/pull/392)

* 

### [Add terminology section, merge in Model \#387](https://github.com/w3c-fedid/digital-credentials/pull/387)

* 

### [Define Digital Wallet \#386](https://github.com/w3c-fedid/digital-credentials/pull/386)

* 

### [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)

* Tim: Simone, would you say the registry is a list of submitted protocol IDs, documentation, and self-attested requirement compliance?  
* Simone: Two different things, registry and implementation requirements, not explicitly connected  
* Nick: I was curious about the implementation requirements idea. Johann had written a pretty extensive section in regard to registry, which we could change to calling “implementation requirements,” but does that answer the problem? If the problem is that people don’t want reviews, changing the name doesn’t help. If we are going to require privacy and security reviews, I don’t care which it’s called.  
* Tim: In that case, we have a list of protocol IDs with links to specs; list of implementation requirements.   
* Nick: Are these going to be requirements that must be satisfied, or just written down?   
* Tim: It’s back to what are the enforcement mechanisms? Are they requirements or just guidelines/expectations? This could be done at the certification layer, as in FIDO.  
* Nick: My preference would be a requirement on UA implementers to use only protocols that satisfy the requirements. Barring that, we should be honest about what we’re able to do, and provide the documentation for someone else to make that decision.   
* Matt: In response to Nick, are we saying "if you’re going to evaluate protocols for use with DCAPI, here are the criteria you should use"? As distinct from, "we’ve done the evaluation."  
* Nick: “You should think about this but we know you won’t” is worse than being honest. If we have requirements on protocols, but know implementations won’t use them, that gives a false sense of what we’re providing  
* Tim: Who is the audience of this spec? Is it exclusively browser implementers, or like WebAuthn, 4 audiences? E.g., verifier or issuer deciding which protocols to support. Ecosystem deployment guidance?  
* Ted (from chat): "How to evaluate" results in a rubric, similar to [https://www.w3.org/TR/did-rubric/](https://www.w3.org/TR/did-rubric/). Every DID deployer has different priorities and requirements of the various attribute axes. The rubric just helps everyone evaluate their candidate DID methods.    
* Nick (from chat): my preference was a normative requirement on UAs ([https://github.com/w3c-fedid/digital-credentials/issues/288](https://github.com/w3c-fedid/digital-credentials/issues/288)), but if not that, we should be honest about whether protocols actually do satisfy those requirements (and part of that could be separately documented requirements that could be certified by some other body)  
* Matt: We may all have different assumptions about the audience. Evaluation and capturing within the spec seems too slow for the development and innovation. Rubric sounds great, as an external doc.   
* Wendy: We’re torn on the things we’d like to say and document elsewhere, and where the spec itself can have meaningful impact. We’ve heard how the UA might/might not use a registry, but if that’s not the enforcement lever, then we need to make sure the spec as it works is privacy preserving.  
* Nick: One of the things I thought we’d agreed on is that we’d do privacy and security reviews of each protocol. Is that something we think is too burdensome, still want to do?   
* Ted: There's also a liability concern to asserting something is secure if it turns out not to be.  
* Nick: We’ve been doing privacy and security reviews for decades and don’t think that incurs liability.  
* Tim: Can we come to TPAC with proposals, and come out picking one?   
  * E.g., drop registry, registry becomes a list of known protocols, ….   
* Heather: That would be helpful.

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan  
* Matthew Miller (Cisco)  
* Simone Onofri (W3C)  
* Tobias Looker (MATTR)  
* Nick Doty (CDT)  
* Tim Cappalli (Okta)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Bjorn Hjelm (Yubico)  
* Lee Campbell  
* Helen Qin  
* Brian Campbell