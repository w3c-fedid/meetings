# FedID WG Telecon — DC API Series B, 2026-02-18

* Moderators: Heather Flanagan

* Scribe: 

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia (5 minutes)  
  * Scribe volunteer? Helen  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
  * Warning: DST Clock skew is coming up\! 8-29 March 2026  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Add openid4vci-v1 issuance protocol and enumeration \#465](https://github.com/w3c-fedid/digital-credentials/pull/465)  
  * [Editorial: Add structure and Introduction to Security Considerations \#424](https://github.com/w3c-fedid/digital-credentials/pull/424)  
  * [Mandate one presentation protocol MUST be supported \#454](https://github.com/w3c-fedid/digital-credentials/pull/454)  
  * [Security Considerations: Secure Context \#426](https://github.com/w3c-fedid/digital-credentials/pull/426)  
  * [Presenting with CTAP \#456](https://github.com/w3c-fedid/digital-credentials/issues/456)  
  * [Protocol registry: Reviewing is not sufficient \#255](https://github.com/w3c-fedid/digital-credentials/issues/255)  
  * [privacy review for registry inclusion \#226](https://github.com/w3c-fedid/digital-credentials/issues/226)  
* Any Other Business (AOB) 

# Notes 

## Administrivia

* 

## Ecosystem Updates

* 

## 

## DC API PRs and Issues

### [Add openid4vci-v1 issuance protocol and enumeration \#465](https://github.com/w3c-fedid/digital-credentials/pull/465) 

And [Security Considerations: Structure and Introduction](https://github.com/w3c-fedid/digital-credentials/pull/424) \#424

* Heather: Ready to go? Any concern?  
* No concern from the group  
* Heather: Marcos, please go ahead and submit this

### [Mandate one presentation protocol MUST be supported \#454](https://github.com/w3c-fedid/digital-credentials/pull/454)

* Nick: Just an idea: there were some concerns / formal objections going through about citations to 18013-7. Wonder if there’s a way to recognize or address this concern. LIke a note where we have concerns about access issues.  
* Marcos: Be careful with the wording here. It’s behind a paywall. Not encumbered?  
* Marcos: The recommendation is MUST implement one, SHOULD implement all others. There’s more than one for OpenID4VP. Hand it over to Tim for how to handle that.  
* Tim: There’s one protocol, just three variants. I think they should both be required to be supported, at minimum cross-platform. That’s how you get cross-ecosystem interoperability.  
* Ted: Usually in this situation the MUST is the lowest common denominator that everybody can access with the lowest barrier. The MAY is the $$$ specs or something much more complicated to implement. Not everyone is going to figure everything out. The MUST is the thing that gives you interop. Other stuff is gravy.  
* Marcos: Ted summed it up nicely. On the WebKit side, there's nothing much we can do given that the platform doesn’t give us the ability to do OpenID4VP. Or until that changes. I want to double check — if we do support OpenID4VP, do we support all the variants?  
* Lee: Yes. It’s just unsigned versus signed. Not significantly different, just a single spec.  
* Marcos: Will make the grouping clearer.  
* Tim: In order to have cross ecosystem interop, you must support both.   
* Lee: Agreed, it’s OK to say browsers must support it, and for platforms that can’t do it yet this is a signal to nudge the implementers to add the support for it. This should be a signal to the browsers to do everything you can (cross-device, local support). At minimum, cross-device is needed for interop.  
* Marcos: This puts OpenID4VP at risk since unless/until Mozilla implements it, there’s only one implementation.  
* Tim: I’d rather this spec not get wrecked in the short term and have OpenID be required.  
* Lee: Mozilla is pretty close  
* Marcos: Let’s clarify whether Mozilla is doing it, and if they are, then let’s put a must in there. WebKit will violate it until we get the code that’ll allow us to do it.  
* Nick: Question about the detection, for the website to know what’s going to work. If we say it’s mandatory but actually it fails, it’s a bad situation where the site won’t know what to do.  
* Marcos: For now, the API answer won’t change, but maybe we should deprecate it.  
* Lee: We should have two versions: one for local and one for hybrid. Or, we get the hybrid to always work for all protocols, and have the current API focus on local support.  
* Marcos: Agree, if you can do cross-device, you should definitely return true. I need to think about it a little more.  
* Nick (from chat): I just wanted to avoid a complicated sniffing situation. I'm fine with everyone supports everything, and just sometimes it's going to fail, because that's always the case, no guarantees about what the user has set up.  
* Matt: I agree, the ideal state is we don’t need this API. But given that we know user agents are going to differ on the same platform and for hybrid. It seems still useful to have this method around.  
* Marcos: Yeah, does provide a means for legacy browsers to support checking.  
* Tim: We shouldn’t get developers hooked on this method.  
* Heather: No consensus. We will follow up with discussion and with Mozilla.

### [Security Considerations: Secure Context](https://github.com/w3c-fedid/digital-credentials/pull/426) \#426

* Simone: The structure is merged. Now the idea is to create many requests for adding security mitigations for threats identified in the model.  
* Nick: Secure Context only protects against network tampering, right? Does it protect against cross site scripting? Say you’re using some wifi and you go to an http page and you get redirected to a page that looks like another page that asks for your id.  
* Marcos: Primarily protects against tampering through http.  
* Simone: Good point. Can leave a comment around the localhost scenario.  
* Simone: Posted the scenario in the chat: [https://securityonline.info/androids-secret-tracking-meta-yandex-abused-localhost-for-user-data/](https://securityonline.info/androids-secret-tracking-meta-yandex-abused-localhost-for-user-data/)  
* Nick: certainly issues with localhost that will keep being discussed at W3C settings. Don’t think we need to solve that in this context, but should listen to WebAppSec on any future updates to SecureContext.  
* Heather & Simone: no new concern from the group. 

### [Presenting with CTAP \#456](https://github.com/w3c-fedid/digital-credentials/issues/456)

* Marcos: There may be other ways to do cross-device (in the future). Today, CTAP is the way to go. However, that may change. The proposed text gives that freedom.  
* Tim: Protocols are one layer removed. The protocols are delegating to the DC APIs that just like WebAuthn API uses CTAP to do cross-device. Apple can choose to do something proprietary between their own devices; that’s their choice. This is a well established pattern from WebAuthn. We should mandate CTAP. They are paired effectively.  
* Marcos: Today, we aren’t doing CTAP.  
* Tim: You are doing CTAP today  
* Marcos: Right, cross device platform.  
* Lee: Yes, it’s totally fine to do something different in a closed ecosystem. We should say, MUST support CTAP across ecosystems.  
* Lee: …  
* Tim: That’s the only way to achieve interop.  
* Nick: How will this change the API?  
* Lee: Not really, potentially to the feature detection. More importantly, this is for people reading the specs having the expectations to know how the entire DC API will be supported. The government for example gave us feedback on this.  
* Marcos: If the government is already mandating, what’s the point of pointing it here as well.  
* Heather: should be separate problems.  
* Tim: We are not pleasing the regulators. Regulators are in agreement that there needs to be a secure proximity protocol for the whole solution to work.  
* Marcos: Why is it not in the mdoc or OpenID?  
* Tim: It’s the wrong layer.  
* Marcos: That doesn’t touch our code.  
* Tim: That’s very specific to the way Apple does things.  
* Lee: Safari just happens to be shipping on a platform that supports this. If it shipped on Windows, it would have to do it. This is to tell all the browsers what they need to do.   
* Marcos: We need Mozilla input here. Putting this whole CTAP requirement on them seems cruel.  
* Lee: Windows does provide a way of doing it. Mozilla already has to do this for passkeys.  
* Tim: Just as an example, Firefox makes passkeys on Linux unusable, and that’s not what we want. That’s why we need this.  
* Heather: No consensus. Will come back to this.

### [Protocol registry: Reviewing is not sufficient \#255](https://github.com/w3c-fedid/digital-credentials/issues/255)

* 

### [privacy review for registry inclusion \#226](https://github.com/w3c-fedid/digital-credentials/issues/226)

* Nick: Previously, in order for a protocol to be included, we’d do a privacy review. If we are going to say there’s not a registry, there’s nothing we can do. I don’t think we can say we’ve ensured all of these. So we can either delete all of these. Or we can describe all of the normative requirements and we would have a means to do a review for a new protocol. Have a process that allows us to open issues and highlight in the spec this or that isn’t satisfied.  
* Heather: I think Lee mentioned that any new protocol being added, given that we don't have a registry, would have to be reviewed by the group. I think it would actually be useful to help with the future working group what they need to look for.  
* Marcos: I think we should definitely document how we include things even if it’s not in the spec. It’s been a learning process but I don’t think the things we’ve included are bad. And it would be nice to document the security and privacy aspects to look for a new protocol.   
* Tim: I think that should be a separate document, e.g., it’s WebKit's choice to parse the protocol. It’s an implementation choice. It will be better to be a separate document. It’s weird to document, "here’s how to add a new protocol to the spec" inside of the spec.  
* Nick: It’s useful for future consideration. Some of these can be documented outside of the spec. It sounds like the implementers have done some of this work. I can’t do it all so maybe you can share your experience.  
* Simone: We have the same issue with security. One option is to define criteria for protocols treated as black boxes. Another is to do it for the downstream protocols. We can also activate the liaison for this. LMK  
* Tim: Question. There’s other APIs that deal with different content types. What’s the precedents? Can we look at how they deal with this?  
* Nick: I don't think file content type is a good analogy.  
* Tim: It’s higher assurance than a file potentially but end of the day it’s a general purpose API picking essentially a file type.  
* Nick: I think our goal is to provide higher assurance data. Therefore, it matters quite a bit.  
* Tim: Right. Not saying we shouldn’t do this. Just saying can we look at how this has been done in the past.  
* Nick (chat): that this API is a function that has a parameter, that doesn't mean that every function with parameters is going to be a useful analogy

Next

* Lee: Next call, we want to revisit the wallet binding issue with the goal to land a PR for it.

## AOB

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* [Lee Campbell](mailto:leecam@google.com) (Google)  
* Helen Qin (Google Android)  
* [David Waite](mailto:dwaite@pingidentity.com) ([Ping Identity](https://www.google.com/maps/place/Ping+Identity/data=!4m2!3m1!19sChIJh8iuAzJ5bIcR_-rl_NqQ8iU))  
* Matthew Miller (Cisco)  
* Nick Doty (CDT)  
* Simone Onofri (W3C)