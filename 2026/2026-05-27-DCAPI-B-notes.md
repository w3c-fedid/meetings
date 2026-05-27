# FedID WG Telecon — DC API Series B, 2026-05-27

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
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Relax transient activation requirement for DC API requests\#486](https://github.com/w3c-fedid/digital-credentials/pull/486)  
  * [Spec doesn’t enforce encrypted response requirement \#519](https://github.com/w3c-fedid/digital-credentials/issues/519) & [Specify protocol validation \+ enforce encryption \#520](https://github.com/w3c-fedid/digital-credentials/pull/520)  
  * Issue Triage (starting with issue 263, oldest to newest)  
* Any Other Business (AOB)

# Notes 

## Administrivia

* Admin reminded

## Ecosystem Updates

* \[none\]

## 

## DC API PRs and Issues

### [Relax transient activation requirement for DC API requests \#486](https://github.com/w3c-fedid/digital-credentials/pull/486)

* \[skipped, waiting for Mohamed\]

### [Spec doesn’t enforce encrypted response requirement issue\#519](https://github.com/w3c-fedid/digital-credentials/issues/519) & [Specify protocol validation \+ enforce encryption pr\#520](https://github.com/w3c-fedid/digital-credentials/pull/520)

* Marcos: I was reading privacy and security considerations, and saw the possibility that OpenID might not encrypt responses, where P\&S considerations say you can require encryption. Mdocs does not have that issue, as all responses are default encrypted.   
* John: Can we go over the rationale for mandating encrypted responses?  
* Tim: It’s a non-normative recommendation, not a requirement. There are plenty of use cases where encryption is not required, such as loyalty cards.  
* John: A loyalty card is the most pervasive tracking identifier I have in my wallet. Request comes in; without encryption, you have no protection against a middle attack. How does anyone check that the site is trusted to handle the response, unless it’s encrypted to the site? I assume a protocol that has an encryption key and signs over the response.  
* Marcos: Do we want to weaken the thing for everybody  
* Heather: Chair hat off, when we’re talking about making encryption optional, only needed for “important” things, my mind goes back to the IETF document, "encrypt everything so as not to leave pointers to where the important bits are." The counterpoint is that encryption still has some cost.   
* Tim: At scale, the cost is real.  
* John: I think encryption is mandatory. We can rely on the TLS channel where that works, but not for all of the current protocols. E.g., Issuer is communicating through [example.com](http://example.com)  
* Tim: 2 or 3 challenges: WG consensus that UA doesn’t need to parse the requests, normative requirement for encryption is new; we’d effectively be treating different elements of the same protocol as different protocols.   
* John: Someone has to check that the identifier matches what’s in the request.  
* Helen: We have use cases where encryption happens but not at the protocol layer, e.g., for phone number, the carriers have to encrypt it, and that’s different from other things that might be in the same request. The single request could be composed for different use cases and receivers. Is this the right level to say “must”?   
* Marcos: I think the P\&S considerations should be normative  
* \[discussion on the possible normative use of S\&P considerations: they can be either normative or non-normative\]  
* Ted: We should take spec authors at their word. If they say text is non-normative, treat it that way.  
* Heather: We seem to have gotten away from the core question, answering 519, 520\. How would we make a requirement here without pretty massive changes?  
* Marcos: Changes are rather small: check if requires encryption; check if response is encrypted.  In OpenID, check for JWT, reject everything else.  
* Tim: I’ll check. It would require UAs mandated to understand the request, which is a change from prior WG consensus.   
* John: A variety of possible flows between UA, wallet, platform. I think it should be possible to implement everything in the browser. If there’s a platform API available, I might be happy to dispatch, but I want to get to a state where everything can happen in the browser.  
* Tim: Where we landed, a UA *can* parse, but is not required to. I fear a world where this is all in the browser and gets trapped there, as with passkeys right now in many cases. I’m confused about where this change came from.  
* Marcos: I was reading the text as a mismatch between requirements and implementation. I think this is going to come up in review.  
* Tim: You have protocols that have been reviewed & implemented.  
* Marcos: We should have had a deeper review of protocols by PING or SING before putting them into the spec. This is sensitive information that requires a high level of scrutiny.  
* Wendy: As a matter of W3C practice, I’m not aware of a requirement for review of outside protocols that a spec interacts with.  
* Heather: I recall being told that the browser implementers had done privacy and security reviews of the protocols.  
* John: The question of encrypted responses gets to what this API is. I think the API needs to check for a secure context. I personally would like it to do more.   
* Tim: My frustration is that we seem to be returning to items that had consensus.  
* John: Do we need a place where the platforms talk about?  
* Tim: That’s FIDO.  
* John: Then my feelings have shifted, I don’t care about encrypted responses.  
* Tim: I’m frustrated that we keep revisiting items where it took us a long time to reach consensus.  
* Heather: We’ll bring this back to the "A" call Monday. I’ll start closing some of the issues marked pending-closure.  
* 

### 

### [Issue Triage](https://github.com/w3c-fedid/digital-credentials/issues/) (starting with [issue 263](https://github.com/w3c-fedid/digital-credentials/issues/263), oldest to newest)

* 

## AOB

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Wendy Seltzer (co-chair)

* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* John Schanck (Mozilla)

* Tim

* Marcos

* Helen