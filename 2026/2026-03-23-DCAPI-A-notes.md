# FedID WG Telecon — DC API Series A, 2026-03-23

* Moderators: Heather

* Scribe: 

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)? Mohamed👏  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Warning: DST Clock skew is here\! 8 March through 5 April 2026  
* Ecosystem Updates (5 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Add Unauthorized Cross-Origin Access and mitigation \#480](https://github.com/w3c-fedid/digital-credentials/pull/480)  
  * [Add API Flooding security considerations \#481](https://github.com/w3c-fedid/digital-credentials/pull/481)  
  * Privacy status or issues  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (5 minutes)

* Heather: Any updates? Hearing nothing

## DC API Issues & PRs

### [Add Unauthorized Cross-Origin Access and mitigation \#480](https://github.com/w3c-fedid/digital-credentials/pull/480)

* Simone: We are adding mitigations to different threats. RPs that are friends to another RP cannot collect DCs. We defined a permission policy to address this.  There is a "residual threats" document, and I suggest some of those should be included in the spec.  
* Heather: I will take silence as no immediate concerns. Marking it OK to merge.

### [Add API Flooding security considerations \#481](https://github.com/w3c-fedid/digital-credentials/pull/481)

* Simone: This is another threat when an abusing RP starts firing repeated requests to the user. This can degrade the user experience and result in prompt fatigue. As a mitigation, on the browser side, transient user activation is required, and user mediation is required on the platform side. We may also suggest to UA to implement other mechanisms such as rate limiting. This is connected to another issue about user activation.  
* Lee: We need to make sure we can open all use cases (including opening iframes and directly call the API) upon interaction in the embedder. At the moment we cannot do that. I don’t think there is a risk to the user. We can offer one freebie request (without user activation)and then do exponential backoff, or require only a top-level interaction. But the first call should be allowed without user activation requirement (at least in iframes).  
* Simone: As discussed with Mohamed, maybe we can identify different use cases and have different requirements for each.  
* Lee: This is hard. DC API is use-case agnostic by design. It’s quite hard to include that in the request. We should do this in a request-agnostic fashion. My proposal: You can do it on the top-level without user activation requirement \+ exponential back-off, it won’t be harmful for users, but will unlock some user cases such as payment users in an iframe.   
* Christian: I agree, it will be really fuzzy if we start filtering upon the request, and it doesn't scale (for example, we might want to filter based on the RP). We should find a mechanism that doesn't depend on what is happening.  
* Lee: It is hard, for example, to know it is a payment request. We cannot write spec formal language to do this for payment or phone number for example. We should expect the layering, and offer one freebie. Webauth started like that, and then they changed along the same lines.  
* Christian, what would be the user flow without this?  
* Lee: Without this, Master Card will have to add a button saying “Click here”, but for SPC or passkeys, they don’t have this problem.  
* Mohamed: Payment Request API also offers one freebie request.  
* Christian: Should offer this as browser configuration to the user?  
* Lee: We should leave this out of the spec, it’s up to the browser to define this.  
* Simone: We should check with Nick from privacy, we had a similar discussion about this for Webauthn.  
* Lee: Nothing is shared when you make this call, and the website learns nothing by design. The only issue I see is the user being anonymous, but if it’s only one freebie, it should be fine\!  
* Heather: I don’t think that Nick thinks we have clarity on the layering when it comes to privacy, and that we always delegate this to other layers.  
* Lee: I agree, but I think for any user case, it should be fine to allow one request from a privacy point of view. We can debate that, but I find it reasonable.  
* Simone: The UA has a responsibility to protect the user even in a dump-pipe architecture. So it makes sense to discuss it.  
* Lee: We aren’t a dumppipe anymore, but the protocol still has many layers and we are still passing through arbitrary credentials and hence we cannot do this based on the doctype.  
* Christian: To do this properly, we should understand everything about the trust in the ecosystem, not scalable and not the responsibility of the UA, e.g., some issuers might register certain verifiers.  
* Lee: Offering one freebie request in the spec, is this reasonable or any objections?  
* Simone: an issue to discuss is the right way. Even if we allow one freebie, with exponential backoff, this is effectively a mitigation and hence worth discussion.  
* Mohamed: two proposals: either to offer one freebie, for that don’t need exponential backoff. The other option is to lift those activation requirements and then do exponential backoff. Which one are we talking about?  
* Lee: The first one meets the need. Any reason to do the latter?  
* Mohamed: The first option might also be less disruptive.  
* Mohamed: I will write this proposal up and file an issue.  
* Heather: So what to do with this PR? Does this change anything?  
* Mohamed: Yes, assumptions are changing.  
* Heather: Alright, we will keep it for longer then\!

## Privacy status or issues

* Heather: Please read the B call [minutes](https://github.com/w3c-fedid/meetings/blob/main/2026/2026-03-18-DCAPI-B-notes.md#privacy-considerations), I have spoken to Rick Byers to ask about getting more resources to help with that. We won’t be able to get to CR with the current shape of the privacy considerations section.  
* Windy: I advise people to speak-up on open privacy issues, so when we reach the conclusion, we have factored in all opinions since we aim for consensus. We can move forward without it, if necessary, but we cannot short-cut the discussion.  
* Simone: Let me know if I need to talk to Tara (W3C Privacy lead).  Maybe we should follow the same approach as security. If you file a privacy threat, remember also to provide a suggestion for the addressing part (or what can make you happy on addressing it). 

# AOB

* Heather: Any other business? None\!

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Helen Qin (Google Android)  
* Mohamed Amir Yosef (Google Chrome)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Wendy Seltzer  
* René Léveillé (1Password)  
* Ryan Watkins (Mastercard)  
* Christian Bormann (SPRIND)  
* Simone Onofri  
* David Waited  
* Brian Campbell  
* Bjorn Hjelm  
* Michael Jones  
* George Fletcher  
* Lee Campbell