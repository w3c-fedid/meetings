# FedID WG Telecon — DC API Series A, 2026-06-01

* Moderators: Heather

* Scribe: 

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Relax transient activation requirement for DC API requests\#486](https://github.com/w3c-fedid/digital-credentials/pull/486)  
  * [Spec doesn’t enforce encrypted response requirement \#519](https://github.com/w3c-fedid/digital-credentials/issues/519) & [Specify protocol validation \+ enforce encryption \#520](https://github.com/w3c-fedid/digital-credentials/pull/520)  
  * Issue Triage (starting with issue 263, oldest to newest)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (5 minutes)

* Christian: Deadline for GDC sessions was last Friday. There will be a joint talk of the DC API and  how the different protocols work together. Also sessions on the layers & FIDO CTAP/PXP

## DC API Issues & PRs

### [Relax transient activation requirement for DC API requests\#486](https://github.com/w3c-fedid/digital-credentials/pull/486)

* Mohamed: The main motivation for this issue was that payment credentials were blocked and in a partnership project, the result was that this currently blocks the whole experience. The embedder would state that this iframe is allowed to do DC API calls. The current plan is to experiment with DC API delegation and see whether that would unblock the current UX problems. Further optimizations for other use-cases could happen later. This would not be restricted to payment, but be general for DC API. The embedder would be allowed to delegate this to the iframe. Will be shipped behind an experimental flag in Chrome for testing to gather further insights. [\[DC\] Implement capability delegation for Digital Credentials](https://crrev.com/c/7837482)

### [Spec doesn’t enforce encrypted response requirement issue\#519](https://github.com/w3c-fedid/digital-credentials/issues/519) & [Specify protocol validation \+ enforce encryption pull\#520](https://github.com/w3c-fedid/digital-credentials/pull/520)

* Heather: The core question is whether we should require response encryption and a general discussion on pros/cons. There was no consensus on the last call.  
* Christian: OpenID is designed to allow choice of encryption. For bigger deployments, there is the High Assurance profile which requires response encryption. But there are implementers who want the option of unencrypted responses. If we want to change that and only allow encrypted responses, we need to let the OpenID spec writers know.  
* John: Main concern is with signed requests that are not encrypted. Example: an issuer that is the only one allowed to read the credential, such that the verifier cannot see into the credential. There are other places that could offer this protection, but it seems cleanest to do here.  
* Christian: In OpenID4VP, you have an array called *expected origin,* and those are signed as well. The wallet can detect whether something is coming in from a different origin.  
* John: That’s great. We might differentiate between same-origin and cross-origin requests. I think we always want cross-origin requests to be encrypted. So, being able to identify same- vs cross-origin in this spec would be good. Not sure the UA can say a request is potentially cross-origin.  
* Brian (in chat): What is a cross-origin request here?  
* John (in chat): A request that is signed by a party other than the site making the DC API call.  
* Martijn: Always encrypting the response is not really expensive while always identifying whether it is required or not is hard and implementations would probably get it wrong. It is important for all components to have certainty that all identifiable data is encrypted.   
* Simone: I would take a step back and define general requirements/invariants on the DC API. If the requirement is that the response should not be exposed to certain elements, then it can be achieved using different mechanisms. Let’s discuss the general requirements and then how to solve them. Is the invariant that credential responses must not be exposed to verifier-page JavaScript, extensions, third-party scripts, or intermediaries before reaching the intended verifier/receiver?  
* John: If we mandate response encryption, then we have to get rid of unsigned requests. If you don’t sign the request, then the encryption key is not protected and doesn’t make sense.  
* Christian: \+1.   
* Martijn: I agree that signing requests is great and response encryption has value in those cases. There is a pretty significant difference between being able to passively see the response and actively attacking a request (e.g., by changing the encryption key). Response encryption still provides some benefit, especially given that response encryption is not that expensive.  
* John: Struggling to see the point of response encryption if the request is not signed. Response encryption is also aimed at preventing the user agent from seeing the response and that might even be harmful. Who are you trying to keep the message confidential from?  
* Martijn: The attack is detectable, but you have to make an active attack. For signed requests, that attack is fully prevented; for unsigned, you have less certainty. It is not as good, but there is still some value to response encryption.  
* John: You effectively rely on the TLS channel for unsigned, but who is on path that the data might be exposed to? If the request is not signed, there seems to be very little benefit.  
* Simone: The protection should be signing \+ encryption. There are some statistics from OONI on scenarios in which TLS is manipulated, and we cannot rely on it completely. There is also the danger of Man-in-the-Browser, and there are papers on similar attacks running on WebAuthn. We will not get to 100% security (it is normal), but we can increase attack complexity and/or its impact and/or detectability. This can also help simplify signals to the user about what guarantees to expect.  
* Christian: When we talked about OpenID4VP, we talked about signing and response encryption, but there were use cases of no-PII/low-assurance use cases. So, you can have signed or unsigned requests, and encrypted or unencrypted responses.  
* Simone: Curious to learn about the use-cases where unsigned request & un-enrypted response would be used.  
* Martijn: It is somewhat unclear what exactly PII is, and it is pretty hard to decide and impossible to enforce that. The wallet should be able to decide whether or not it encrypts, since it is in a better situation to decide whether encryption is required. Encryption is a very cheap operation compared to signing, so there is no reason to not mandate it.  
* Wendy: How do we bring this issue to conclusion? This is a big chunk of work in the spec and we need to make a decision. We need to make a choice.  
* Mohamed: Either we allow it or disallow — if we allow unencrypted responses, it makes everything a bit fuzzy. If we mandate response encryption, then it must at least be a malicious browser to get access to PII — we get somewhat good guarantees by default. The big question is whether it harms adoption of the DC API. If it doesn’t, we should mandate it.  
* John: The bigger issue is if we mandate signing as well. The simplest story would be signed requests & encrypted responses for everything.  
* Christian: From my perspective, I believe response encryption is expensive at a really big scale, but if you think about regulated scale, it’s a must anyway. The cost is acceptable.  
* Brian: What exactly is the security concern that we are trying to mitigate, especially now that we are discussing signed requests as well? What exactly is the real threat?  
* John: To give a concrete example: the payment use-case. The payment processor would provide a signed payment request. The user can then encrypt their payment details directly to the payment processor and no one else gets access to the payment information.  
* Brian: So the presumption is that the invocation with the payment provider will pass through them? Sounds like a use-case that is not supported by this API?  
* Mohamed: Question to John — For signed requests, is it fair to mandate response encryption?  
* John: Yes, for signed requests, we should mandate response encryption. Assuming that identifying cross-origin requests is a hard problem to solve, we should mandate response encryption. No value in mandating response encryption for unsigned since it can be manipulated during transport  
* Heather: There seems to be some preference towards requiring encryption, but it also doesn’t seem to be fully clear what exactly we are protecting against  
* Simone: A lot of attacks go against unsigned communication and history has shown us that there will be attacks against unsigned requests. This allows anyone to change the request  
* Brian: You’ve compared this to *http vs https* and *xmlsignature* attacks — those are not good comparisons. Everyone uses TLS every single day in multiple aspects and there are things like compromise of the Browser that are not unique to this scenario.  
* Wendy: Asks Brian about what exactly he would like to see.  
* Brian: Is requesting the rationale for these things, when they seem unnecessary for a large number of legitimate use-cases of this API. The examples given so far seem to not be sufficient for the requirements being discussed.  
* Wendy: Otherwise, we seem to be adding encryption in most protocols nowadays and that seems to fit the current discussion.  
* Brian: You want to get the dance right about providing the appropriate security by default, but that is not always achieved by layering on more security. We already have some guarantees by TLS.  
* Martijn: Providing response encryption provides some protection against seeing the response and possibly modifying what is in the response. That in itself is a good goal. How much of it is real, and what is the cost?  
* Heather: Will spend some time with Wendy and Simone to figure out how to best proceed and see if we can find a proposal. Will come up at the next call again and get to a conclusion at the next series A call.

### [Issue Triage](https://github.com/w3c-fedid/digital-credentials/issues/) (starting with [issue 263](https://github.com/w3c-fedid/digital-credentials/issues/263), oldest to newest)

* 

## Any Other Business (AOB)

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Wendy Seltzer (co-chair)  
* John Schanck (Mozilla)  
* Christian Bormann (SPRIND)  
* Mohamed Amir Yosef (Google Chrome)  
* Tara Whalen (W3C)  
* Ryan Watkins (Mastercard)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Simone Onofri (W3C)  
* Brian Campbell (Ping)