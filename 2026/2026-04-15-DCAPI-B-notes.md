# FedID WG Telecon — DC API Series B, 2026-04-15

* Moderators: Heather Flanagan

* Scribe: Helen

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Protocol Integrity Requirements for Request/Response Tampering \#494](https://github.com/w3c-fedid/digital-credentials/issues/494)  
  * [Define "present credential requests" algorithm.\#419](https://github.com/w3c-fedid/digital-credentials/pull/419)  
  * [Relax transient activation requirement for DC API requests\#486](https://github.com/w3c-fedid/digital-credentials/pull/486)  
* Any Other Business (AOB)  
  * Planning sessions for IIW (April 28-30)  
  * [Web Engines Hackfest](https://www.w3.org/events/conferences/2026/2026-web-engines-hackfest/) hybrid 15-17 June 2026  
    * "we have the opportunity for having W3C Team representation on the program, as well as for a few W3C Working Groups to meet there face-to-face for free and we’ve communicated to W3C group chairs that this opportunity is open until **April 30th, 2026** (same deadline as the event’s call for papers)."

# Notes 

## Administrivia

* 

## Ecosystem Updates

* 

## 

## DC API PRs and Issues

### [Protocol Integrity Requirements for Request/Response Tampering \#494](https://github.com/w3c-fedid/digital-credentials/issues/494)

* Heather: Related to security requirements. Opened last week. I’d love to get thoughts on how we want to handle this?  
* Lee: Does it matter at this API level? We already mandate that it’s in a secure context. Is the threat that the request got modified outside of the secure context?  
* Heather: The main concern is whether the modification ever happens at this layer?  
* Lee: The request is in the secure context, and our API can only deal with it at this layer.   
* Tim: Don’t think we can require signing. Signing infrastructure is complex, expensive. Many use cases that it’s completely unnecessary. Don’t think we can mandate it at this level.  
* Nick: Was wondering if the threat was cross-site scripting?  
* Marcos: Yeah that could happen. Signed requests are protected against that. Unsigned ones can be taken and potentially shared. Who’s benefiting from this? Developers or users? What’s our focus?  
* Lee: It’s not that tooling is hard. It’s that not every single ecosystem has the infrastructure to do it. Self-signing can be effectively unsigned if there’s not an infrastructure to give out PKIs to sign and validate the request. Should we just acknowledge that the request can be unsigned?  
* Nick: Agreed on the signing problem. But I’m worried about cross-site scripting attacks. Fixing that seems more valuable than mandating the signature.  
* Lee and Marcos: It is possible to have that attack.  
* John: Want to push back on the idea that the WebAuthn is the same. The assertion only makes sense to the caller.  
* Lee: But WebAuthn also has use cases like PRFs, where the attack does matter.  
* Marcos: I’m hearing the main concern of having an unsigned protocol is developer / RP convenience. Is that a good enough justification? If there’s more, can we add more context?  
* Tim: It’s not just about convenience. It’s about the infeasibility of aligning all the parties to agree on a signing infrastructure on certain use cases. This is not the right layer to enforce signing, and it’s better to enforce this (and it’s happening) at the further layer.  
* Heather: I know it’s happening in the EU. Not sure if it’s happening elsewhere.  
* Tim: Yes. It’s happening with certification programs and the EU may use that.  
* Heather: Who’s doing that?  
* Tim: The certification requirements are being defined in Fido.  
* Marcos: If unsigned is an option, then would people tend to use that for convenience?  
* Lee: The request signing is more about RP authentication and less about request integrity. In the US, MDLs are doing unsigned requests because they don’t think the use of the MDLs should be vetted and allowlisted.  
* Brian: Yeah, request signing is a form of gatekeeping. Let’s not get caught up in it being more secure, because that’s sort of a false promise.  
* Marcos: It’s good to educate ourselves on these additional contexts.  
* Nick: Unsure why this falls to the issuer layer.  
* Tim: Ultimately, it’s about the credential type and claims in it that dictate whether the request should be signed or not. We decided a long time ago that we are one layer removed from what the credential type is and what the scheme is. We don’t have a place to enforce it.  
* Marcos: Webkit does check the signature.   
* Lee: How would the browser know which certificate to check against? You can validate that the signature is correct, but you need to also validate that the certificate is trusted. Otherwise, the attacker can just self-sign it.  
* Marcos: We check against the Apple Wallet program. Especially for high value credentials.  
* Lee: But you can’t do that for every credential. Or expect every platform to do that.   
* Lee: Propose us to close this issue and say the request integrity is protected by secure context. That’s the case for other web APIs. Signed requests are not for tampering; they are for RP authentication. If we are focusing on pro-user, then it’s actually not good for the user to mandate an ecosystem that is locked down to only certain players.  
* Marcos: Please add all the contexts to the issue.  
* Tim: This comes back to us removing the concept of a second user agent from the spec. We could describe the separation of the responsibilities better if we have the concept. We should put back the two user agents: one being the browser, the traditional user agent; the other, the credential manager, which the user also has to choose and trust just like a browser. iOS might do it all together, but that doesn’t happen everywhere.  
* John: The second user agent is nice if there’s only one other piece of software, like one other wallet, but we may be talking about multiple different wallet applications at once, and someone needs to mediate between those, if there’s a disagreement. I think the browser is the correct place to do that.  
* Tim: It’s fine to have multiple wallet user agents.  
* John: For the issue discussed, I think transparency is more important than integrity.  
* Tim: Agree, but we’re starting over again. It will fundamentally change the whole spec.  
* Heather: John, if you’d like to write this a bit more. Like Tim said we might choose not to go that route, but it’s nice to see what it can look like.  
* Tim: We have to scope better to continue these conversations.   
* Tim, Heather, Marcos: Multiple issues are brought up during this discussion and we should track them separately.

### [Define "present credential requests" algorithm.\#419](https://github.com/w3c-fedid/digital-credentials/pull/419)

* Marcos: I believe this is done. John, please give feedback. Others too.  
* Heather: Let’s give people time to review it and go through the official approval process before merging.

### [Relax transient activation requirement for DC API requests\#486](https://github.com/w3c-fedid/digital-credentials/pull/486)

* Marcos: A couple of specs have run into this issue. Happens in payments. When you click on something, the activation is tied to the document. You can’t then do that from a different iframe. One proposal is a freebie for an iframe. Another proposal is through delegation where the button frame delegates the permission to the other iframe. It’s also capability specific. Transient activation is a time window allowed to invoke the API when a user click happens. I don’t think the freebie model is as amazing as it can be, and we could use a global solution for this for all use cases.  
* Nick: iframe case seems different from the navigation case. It is concerning if I click on a link, and I end up on another page, and that page immediately gets the ability to launch the request. It will be less harmful for iframes. Can we clarify the scope?  
* Lee: The use cases are for iframes. Don’t think we need it for re-direct. At least that is what motivates the issue. It’s reasonable to ask for an activation after a navigation. The case for the iframe is, for example, like payment use cases, which are the main driver, and age use cases. The iframe is a third party provider that provides the payment / age solution. That’s not visible on the merchant website. You just click on the pay button and then the iframe makes the call for the digital credential. This has been widely deployed and it’s going to be hard to make every merchant make the change to make the call themselves.  
* John: I’d like to hear the real use cases / large deployments.  
* Marcos: We did hear real issues with on, e.g., the payment sides, with, e.g., Stripe and other large handlers.  
* Lee: We also get this issue from Visa and Mastercard that are stuck on this issue.  
* John: I’m not sure they are blocked or just unwilling to add friction to their flows.  
* Lee: It's reasonable that they don’t want to add friction. It also doesn’t really add any risk.  
* Marcos: It’s nice having details and seeing what benefits the user.  
* Lee: It does help the user with, e.g., Fraud. Think of online shopping today where we can stop a fraud transaction by verifying their digital credentials. If we add so much friction that the banks and merchants can’t use it, then they have to fall back to OTP, raw credit card numbers, etc., which can be more risky to the user. Happy to work on the exact solution. Want to note there is real user value.

## AOB

Planning sessions for IIW (April 28-30)

[Web Engines Hackfest](https://www.w3.org/events/conferences/2026/2026-web-engines-hackfest/) hybrid 15-17 June 2026

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Wendy Seltzer  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* John Schanck (Mozilla)  
* David Waite (Ping Identity)  
* Helen Qin (Google / Android)  
* Lee Campbell (Google / Android)  
* Tim Cappalli  
* George Fletcher  
* Brian Campbell (Ping)  
* Nick Doty (CDT)  
* Marcos Caceres  
* Bjorn Hjelm (Yubico)