# FedID WG Telecon — DC API Series B, 2026-03-18

* Moderators: Heather Flanagan

* Scribe: Wendy

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
  * Warning: DST Clock skew is coming up\! 8 March – 5 April  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Order of serialization vs protocol filtering \#475](https://github.com/w3c-fedid/digital-credentials/issues/475)  
  * [EUDI Wallet functional conformance testing \#471](https://github.com/w3c-fedid/digital-credentials/issues/471)  
  * [Addressing Request Tampering \#426](https://github.com/w3c-fedid/digital-credentials/pull/426)  
  * Privacy considerations  
* Any Other Business (AOB)


# Notes 

## Administrivia

* 

## Ecosystem Updates

* Tim: As of yesterday, Hybrid in CTAP is now called proximity exchange protocol, a separate protocol from the CTAP spec. 

## 

## DC API PRs and Issues

### [Order of serialization vs protocol filtering \#475](https://github.com/w3c-fedid/digital-credentials/issues/475)

* Marcos: Mohamed sent a PR. [https://github.com/w3c-fedid/digital-credentials/pull/477](https://github.com/w3c-fedid/digital-credentials/pull/477)  Originally we thought it was a good idea to check all the data before proceeding, but in Copilot review, we thought it made sense to not check data that we would be filtering out anyhow. Chrome was already doing that; WebKit was doing the opposite, but I’m OK to align with Chrome.   
* Tim: Makes sense.  
* John: I haven’t checked which order we’re using, but it sounds fine to me.  
* Marcos: We’ll have full test coverage.   
* Heather: Any concerns? Sounds reasonably un-contentious. Good to merge when you’re done.

### [EUDI Wallet functional conformance testing \#471](https://github.com/w3c-fedid/digital-credentials/issues/471)

* Tim: There will be tests in OpenID, WPT, but I don’t know who will be bringing them together. The challenge will always be automating a real EUDI wallet.  
* Marcos: We have a fairly complete solution, but formats need special origin-bound signatures, which makes it complicated. We currently use fake domains, like wpt.local. We generally don’t leave our local network in testing. We might need them to give us something with a long-lived signature for testing.   
* Tim: I think we should support EC if they want to build one.   
* Marcos: How could you automate, with all the clicks?   
* Tim: The definitions of what you’re testing are important. Plumbing, or full system?   
* Tim: This might be a one-off conversation under GDC with W3C, FIDO, EC.  I’ll ping Oliver.

### [Addressing Request Tampering \#426](https://github.com/w3c-fedid/digital-credentials/pull/426)

* Heather: Looks ready to go.   
* Nick: thought this just talked about network-level secure contexts. What about other layers?   
* Marcos: Think we need to spin off more bugs related to this, e.g., require that the formats are tamper-proof.  
* Tim: Another rabbit-hole, we have real problems in the passkey ecosystem of extensions hijacking navigation. UX and security issues.  
* Marcos: We did some experimentation, got close. Tradeoff, because unforgeable means you can’t add properties, polyfill.   
* Tim: It will be less than 2 years before this becomes a problem. Often a compounding problem of claims of a security hijack  
* Marcos: You’d have to do all of credman, navigator.credentials becomes unforgeable.   
* Nick: Is there some compromise, like a specially-labeled extension point?   
* Tim: 1Password doesn’t want to force users to install a native app. Some of these technologies are browser-centric because of history. If we were to do something like this, we’d want a coordinated deadline to bring the browser extensions on-board, e.g., 1 year. Would have to have some level of feature detection for platforms without the APIs. There’s no way for a web-based credential store. We’ve talked about it but nothing yet.    
* John: not opposed, but want to think about. Get an entitlement from the wallet to use the API. Difficult because of the PKIs, lots of wallets.  
* Marcos: We’d have to figure out a mechanism for WebAuthn, transfer to digital credentials.  
* Tim: I don’t think preserving the extension model for digital credentials is the right path. You leave credentials trapped in the browser. Our goal should be getting a non-native app credential manager talking to the platform.   
* Heather: What do we do with 426, where are we documenting other things?  Where are we talking with WebAuthn? Web Extensions group?  
* Marcos: happy to be part of the conversation  
* Tim: Coordination challenge, No one wants to go first. And have to address the “open web” concern.  
* Heather: Merge the PR, more work to do. 

### Privacy considerations

* Nick: suggest we start with 3 areas in particular.  
  *  Exchange protocols, update from references to registry. I put a suggestion into one issue re normative requirements and reviews..   
  * Second, a cluster of issues about indications of purpose, where that should be exposed, UX research, EU requirements  
  * Linkability, 279\. A proposal re distinguishing linkable and unlinkable requests. Make sure we can satisfy it.   
  * I was hoping we could find some volunteers for these issues.   
* Heather: I have a query to Rick at Google for resources  
* Marcos: Where the responsibility lies between API, platform, We can’t put normative requirements on things outside the browser  
* John: think there is a desire to have some friction at the browser level if overtly demanding. Difficult if you have a bundle of request and you don’t know which will be sent to the wallet. I have a proposal I’ll send about request transparency, how much friction to impose at the browser level. Transparency log where sites log in advance what kinds of requests they’ll send.   
* Nick: Very interested to see that proposal. Gets to other issues I hadn’t raised here about accountability. On what layer will satisfy the purpose display,  If we had a direction, it would make it easier to start.  
* Marcos: Multiple requests, is it and or or. I hope we can resolve it to or.   
* Tim: If we continue to revisit core ecosystem decisions, . Currently, the ecosystem sees the wallet as a second user agent, and avoids bringing the browser into all these trust frameworks. We need to be able to reason about 2 UAs, and the primary responsibility of the browser is to make sure you have permission to get to the wallet.   
* Heather: Are we not being clear enough in the spec?   
* Nick: It’s not yet settled in implementations.   
* Tim: It was removed because of no weight without trust framework and legal authority. That’s being enforced on the wallet. The browser isn’t the place to do that.   
* Marcos: we have browsers here, not all the wallets.   
* Tim: Wallets aren’t interacting with this API   
* Heather: and that brings us to the end of the call, though not the issues. 

## AOB

* [EUDI Wallet functional conformance testing \#471](https://github.com/w3c-fedid/digital-credentials/issues/471)

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Wendy Seltzer  
* John Schanck (Mozilla)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Tim  
* Nick  
* Marcos  
* Bjorn  
* 