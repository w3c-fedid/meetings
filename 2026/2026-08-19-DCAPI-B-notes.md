# FedID WG Agenda \- DC API Series B \- 19 August 2026

* Moderators: Heather

* Scribe: Nick

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

## Agenda

* Administrivia  
  * Scribe volunteer(s)?   
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [require in-context in-content explanation and an element for user-initiated presentation \#208](https://github.com/w3c-fedid/digital-credentials/issues/208)  
  * [clientData (26H2 edition)](https://github.com/w3c-fedid/digital-credentials/issues/574)  
  * [Add Credential Manager Chooser def and add clarity around differences with issuance \- \#561](https://github.com/w3c-fedid/digital-credentials/pull/561)  
  * [Privacy: Add Data Clearing and Credential Availability protections \- \#536](https://github.com/w3c-fedid/digital-credentials/pull/536)  
  * [Security: Expand Threat Model and mitigate malicious payloads \- \#533](https://github.com/w3c-fedid/digital-credentials/pull/533)  
  * [Add document origin to request context \- \#512](https://github.com/w3c-fedid/digital-credentials/pull/512)  
  * [Require support for both mdoc and signed OpenID4VP protocols \- \#454](https://github.com/w3c-fedid/digital-credentials/pull/454)  
* Any Other Business (AOB)

## Notes

## Administrivia

Heather: reminding us of our code of conduct. huzzah\!

## Ecosystem Updates (10 minutes)

* [GDC](https://globaldigitalcollaboration.org/gdc26?day=sept-1) is coming up  
* Lee: Kind of a win that DC is included in the regulation. But a question is coming up about the specification being a draft even though it isn’t supposed to point to drafts. Getting questions from legal folks about whether this spec changes, because the law "can’t" reference something that changes.  
  * Did we agree that we wouldn’t have stable versions, but would just modify over time?  
* Heather: Never really comfortable with living standard, but have to check our history.  
* Lee: Much more comfortable situation if we are out of this draft status, avoiding challenges about referencing   
* Marcos: Strange that they would have that problem, but understand it’s a different community. HTML and many other standards are "living" standards; software has bugs, gets changed, etc. I would oppose putting versions on documents, as it’s not …  
* John: Does the law reference it? or just the ARF?  
* Lee: Implementation acts based on the ARF include direct reference to OpenID4VP, which references the DC API. That's kind of what we wanted, but it is coming up. can’t delegate requirements in lawmaking. So the reasoning is that laws should point at final documents.  
* John: Does the law say that they must, or just that they may?   
* Lee: My understanding is that certified wallets must implement this, but could check.  
* Lee: Need a stable W3C link to quell these questions.  
* Marcos: Shortname/TR links are stable  
* Ted: But they really want a stable document, not just an unchanging URL. That's why such requests are often answered with a datestamped URL for which the words/contents will not change as time continues to pass.  
* Marcos: I think the ask is unreasonable.  
* Heather: I don’t see us immediately coming to consensus on that. Have noted the issue, to get to as quickly as we can, safely.


## DC API Issues & PRs (45 minutes)

### [require in-context in-content explanation and an element for user-initiated presentation \#208](https://github.com/w3c-fedid/digital-credentials/issues/208)

* Nick: My latest comment is one suggestion for a solution. This was one of a couple of options, put it on the site content in-context with what the user will be doing. Alternative was to put fields with enumerations, data describing categories of why the verifier is requesting data. The group closed that other one; this is the remaining option. In the sketch, we used declarative HTML; it’s one way to think of this. Verifiers would have to provide an explanation for requesting high-assurance identity documents. May not need to put this all into the CM since CMs aren’t experts on it.  
* Tim: It’s back to informational vs. enforceable. The site could put one thing and request another. The user agent is ultimately presenting and capturing the intent. The fact that this solution leaves things decoupled is unfortunate.  
* Nick: I agree, having something in web content can cause this disconnect. But having the site declare something could give security researchers, etc… clues to report a site’s misuse.  
* Tim: But enforcement can happen at the protocol level.  
* Nick: It seems unlikely that all CMs will enforce this.  
* Tim: Jurisdictions with government ID programs have to be approved for a use case, requests have to be signed over. It’s not a free-for-all.  
* Nick: I agree those jurisdictions exist, and arguably many more who don’t.  
* Marcos: I agree with Tim re: high-value credentials. But for email verification, for example, not going through the DC API channel, we might declare these things in a declarative form. So it might be use-case dependent.  
* Tim: But those are not what we’re defining in this spec.  
* Marcos: But those requests could go through similar paths.  
* Tim: But, for instance, a digital credential that exists in Android could … (hard to follow the example)  
* Lee: We had a debate about this in the EU, an enum for purpose, for example, and if we had purpose strings at the protocol level, it could at least get signed over. They gain some non-repudiation. But if left exclusively at the web layer it’s not enforceable. Maybe we say this gets handled at the presentation protocol level and it’s up to governments to decide what to do. If you request PII we might care, but something like a verified email?  
* Matt: If we’re going to explore a declarative purpose, the fact it’s not enforceable makes it feel weird. It may leave declarative breadcrumbs for a security researcher who could then report misuse, but defining that in the spec means the ultimate efficacy will be a “maybe someone will look.” If we can focus on more clearly indicating intent, that would be more helpful. We also don’t want to define this for non-DC API use cases.   
* Nick: When I raised this a couple of years ago, the response was “oh yeah this’ll be handled at the protocol layer.” When I looked into it, I didn’t see any evidence of this being solved there, and haven’t seen anything recently. It makes more sense to try and solve this at the web layer because that’s where the user is. But if someone will do something else at another layer then sure, fine. Perhaps we publish something saying something to this effect. Google UX researches published docs showing how this pattern could be used.  
  * [https://docs.google.com/presentation/d/1YwB-ocoI5Y7MWtMxh4eQVp1qm6SfUBKHoSt81E\_oRu8/edit?slide=id.g36ca344351d\_7\_14\#slide=id.g36ca344351d\_7\_14](https://docs.google.com/presentation/d/1YwB-ocoI5Y7MWtMxh4eQVp1qm6SfUBKHoSt81E_oRu8/edit?slide=id.g36ca344351d_7_14#slide=id.g36ca344351d_7_14)   
* Heather: “it’s happening here” vs “it’s happening somewhere else”  
* Lee: There’s some effort in the DCHP WG to try and define some purpose. “Intent to retain” is an initial stab at conveying one kind of this intent. This signal could lead to UI being shown.  
* Tim (chat) \- where this is documented in OpenID4VP \- [https://openid.net/specs/openid-4-verifiable-presentations-1\_0.html\#section-15.3](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html#section-15.3)  
* Nick (chat) \- OpenID4VP Section 15.3 indicates that the purpose should be shown to the user before reaching the wallet, like in the web content, like in the \#208 proposal. while normative, it doesn't seem to have any possibility for wallets to recognize or do anything about it.

### [clientData (26H2 edition)](https://github.com/w3c-fedid/digital-credentials/issues/574)

* Tim: Bringing back clientData with an update since Issue 95\. It borrows from WebAuthn ideas, but is designed for DC.  
* Tim: New things in here: stronger binding to request context. changes to PXP if a cross-device exchange has an error, which isn’t available today. TransportContext, generic for different vendors/implementations.  
  * DBSC KeyID is the way to harden the session: include those in the client context, so that it hasn’t been relayed or moved.  
  * Add a new optional top-level parameter to override the hash algorithm; problem in WebAuthn where hash is hardcoded, but a new good enough default if not overridden.  
  * Client data is generated by the browser and passed to the underlying platform, and injected on the way back by the browser to the verifier or the issuer, to verify that it matches what was signed over by the verifiable presentation.  
  * Would make changes to PXP, DCHP protocol,  
  * No changes to the existing protocols  
  * Illustrated with examples  
* Matt: Transport Context isn’t intended to communicate anything about the channel, like indicating whether it’s Apple’s proprietary mechanism, or a PXP channel; just to indicate that it was the two devices that brokered that interaction.  
* Tim: Once we have consensus, I will write up a PR. Need to decide whether to debate details in an issue or as a PR.  
* Marcos Hasn’t reviewed it yet.  
* Heather: Please review, we’ll bring back on the next 2 calls

### [Add Credential Manager Chooser def and add clarity around differences with issuance \- \#561](https://github.com/w3c-fedid/digital-credentials/pull/561)

* Tim: Conversation on whether issuance should be creation, with some caveats about what you get back. Clarifies what is different about issuance, and makes a definition for choosing a credential manager (not just a credential).   
  * Has some approvals, doesn’t seem controversial.  
* Matt: Is Credential Manager Chooser different from the pattern where the user chooses a credential and the platform figures out which credential managers are relevant? or is this chooser just for issuance context?  
* Tim: Choose a credential on get, and a credential manager on create, like in WebAuthn.

### [Privacy: Add Data Clearing and Credential Availability protections \- \#536](https://github.com/w3c-fedid/digital-credentials/pull/536)

* Mohamed raised, but Tim hasn’t reviewed yet. Tim will review.  
* Nick: Summary makes sense, but I haven’t reviewed the text yet.

### [Security: Expand Threat Model and mitigate malicious payloads \- \#533](https://github.com/w3c-fedid/digital-credentials/pull/533)

* Heather: Update to the threat model seems straightforward.  
* Marcos: Mostly fine, but wanted to recheck larger text.  
* Tim: LGTM.

### [Add document origin to request context \- \#512](https://github.com/w3c-fedid/digital-credentials/pull/512)

* Request reviews.  
* Nick: User should probably see both, although it’s confusing. But does the wallet see both?  
* Marcos: Protocols don’t support receiving both origins/sites.  
* Lee: Given response encryption, the top-level document might not ever see the data. Maybe the most important thing for the user is the embedded/calling origin.  
* Marcos: The embedded origin could just decrypt and pass it on.  
* Lee: Get a lot of pushback when there are multiple origins, especially when the embedded ones are awkward.  
* Tim: WebAuthn recommends showing both, and most implementations don’t.  
* Lee: And sometimes we show RP ID, not origin.  
* Marcos: Storage Access is an example that shows both (and needs to).  
* Lee: In reality, whenever you give your data to one entity, you are probably giving it to others…  
* … but if you’re sharing it with Organization X, you have to trust them.  
* … you already know what web page you’re sharing it with.  
* Marcos: Our privacy people pushed back on those arguments strongly.  
* Nick: Disagree that users know what webpage they are on, but the top-level document is more familiar to the user, something they might remember or not be scared by.  
* Lee: Authenticated friendly verifier name is another field, and it seems especially tricky to show the user all three pieces of information in a friendly way.  
* Tim: We could, like WebAuthn, recommend it, and know that probably no one will do it, but at least some implementer could.  
  * maybe Client Data could help, at least with the platform, if not the wallet. Marcos to come back to this after reviewing a new client data proposal.

### [Require support for both mdoc and signed OpenID4VP protocols \- \#454](https://github.com/w3c-fedid/digital-credentials/pull/454)

* Tim: Still prefer Brian’s argument, but abstaining, rather than fighting it.  
* Lee: Mandate all protocols better than "one of".  
* Heather: will note for future.

## Any Other Business (AOB)

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Matthew Miller (Cisco)  
* Nick Doty (CDT)  
* Tim Cappalli (Okta)  
* John Schanck (Mozilla)  
* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Lee Campbell (Google)  
* Helen Qin (Google)  
* Marcos Caceres (Apple)

