# FedID WG Telecon — DC API Series A, 2026-07-13

* Moderators: Heather

* Scribe: Isaiah

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
  * Cross-device issues  
    * [Add details about the Cross-device experience for the Digital Credentials API \#369](https://github.com/w3c-fedid/digital-credentials/issues/369)  
    * [Add a signal of whether presentation occurred locally or cross-device \#527](https://github.com/w3c-fedid/digital-credentials/issues/527)  
  * [Privacy: Define expectations for Private Browsing (Incognito) Mode\#534](https://github.com/w3c-fedid/digital-credentials/pull/534)  
  * [Security: Prevent opaque origins from interacting with the Digital Credentials API \#535](https://github.com/w3c-fedid/digital-credentials/pull/535)  
  * [Add verifier hardening guidance for script injection\#539](https://github.com/w3c-fedid/digital-credentials/pull/539)  
  * [Add Internationalization Considerations section\#541](https://github.com/w3c-fedid/digital-credentials/pull/541)  
  * [Expand Accessibility Considerations section\#542](https://github.com/w3c-fedid/digital-credentials/pull/542)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (5 minutes)

#### European Commission Feedback Pending

Simone: European Commission is working on providing feedback for this WG as soon as possible; still waiting, will ping tomorrow. No specific details on what aspect of the API.  
Heather: Do we ever reach out to other governments for their input?  
Simone: Not specific countries. Got some feedback from Italy. If someone would like, I can organize more this week.  
Heather: I’m not so concerned with individual EU countries, since we want this to be global. Individual EU country feedback is great, but we want it to match other legislative bodies.  
Wendy: We should send out an impact document/outreach to users of the spec. If we think that government contact is valuable, we should do outreach to them. GDC\[?\] sounds like a good place to do that.  
Heather: GDC is a month before we want to go to CR, unfortunately.  
Heather: If anyone has contacts, please reach out. I might be able to find contacts in the UK and Australia.

## DC API Issues & PRs

### Cross-device issues

#### [Add details about the Cross-device experience for the Digital Credentials API \#369](https://github.com/w3c-fedid/digital-credentials/issues/369) and [Add a signal of whether presentation occurred locally or cross-device \#527](https://github.com/w3c-fedid/digital-credentials/issues/527)

* Marcos added agenda+, Mohamed tagged the issue  
* Mohamed: The spec doesn’t list anything as cross-device. We should mention this to talk about, for example, the proximity binding when using CTAP2. This is part of the value proposition of this API over other approaches, so we should mention it. I don’t think we need to go into details, since that’s in FIDO CTAP2/PXP. That is in PR \#[538](https://github.com/w3c-fedid/digital-credentials/pull/538).  
* Matt: I can talk about [\#527](https://github.com/w3c-fedid/digital-credentials/issues/527).  
* Matt: authenticatorAttachment is in WebAuthn. There aren’t hard guidelines on how RPs should use it, and it’s unsigned, but it can be a signal about how comfortable the user is to use cross-device ceremonies. Can we bring a similar signal to the DC API for verification? I am pretty sure that RPs are going to want these for various use cases, so if there are no privacy issues, I think it is beneficial to include this upfront.  
* Tim: I think we need this long-term, but I don’t think we need it right now. WebAuthn uses it for this, but the DC API doesn’t have the same user interactions. (Most DC API will be cross-device on desktops because issuers)  
* Mohamed: I agree, I don’t think this needs to be in the first version.  
* Matt: How might this break in the future?  
* Mohamed: Anything that can wait, I would like to push it back to later.  
* Matt: I disagree.  
* Christian: I see the general ask, but I think it will be a few years rather than now. I assume that for the coming year, very few will use this, so we should wait until we have more feedback to understand it better.  
* Matt: Are there any possible gains from knowing that the presentation occurred on the same device?  
* Tim: This can be derived (implied), if I did this from a desktop, it’s obvious that this came from a phone, because there are no wallets on desktops right now.  
* Tim: From what I understand, the people that really want this want it for a security purpose, so it should be attested.  
* Matt: I was kind of thinking of this as a risk signal, for example for RPs that are sensitive to CTAP2/PXP proximity issues.  
* Tim: People are going to want it in the protocol response. That’s what people want for WebAuthn, but we haven’t done it for fragmentation issues.  
* Matt: Maybe we don’t need to follow WebAuthn.  
* Tim: Maybe this goes in a session transcript or something.  
* Simone: I see that it’s useful for WebAuthn because it depends on the provenance of the key. It can be used to see that the presentation was on the same device. For DC API, it may make sense. But I think we need to understand the use cases.  
* Matt: I don’t have compelling use cases.   
* Matt: I learned that some people are requesting this is signed in the response, which seems very useful.

* Mohamed: re: [369](https://github.com/w3c-fedid/digital-credentials/issues/369). I’m just putting an acknowledgement of the complete security story regarding cross-devices. A signed request would be more secure.  
* Heather: Any concerns with merging?  
* Christian: Should we point to CTAP 2.3 since it’s final?  
* Tim: Yes.  
* Mohamed: I will make the change.  
* Heather: Go ahead and merge and close the issue afterward.

### [Privacy: Define expectations for Private Browsing (Incognito) Mode\#534](https://github.com/w3c-fedid/digital-credentials/pull/534)

*From the July 8 call:*  
*Nick: I think it would be very useful if we could describe the difference between inherently linkable and not presentations, e.g., full driver’s license, vs over-18. Is the over-18 able to be presented in unlinkable form?*  
*Lee: We can’t make a statement of unlinkability. Wallets can use different keys for different origins, then unlinkable across origins; but currently, linkable within the same origin. We could imagine a flag for “please use a different private key”. Fair point about the same-origin linking between different modes.*

* Lee: User expects that two presentations private/not-private browser mode would not be linkable by the RP, if the claims you send are unlinkable. Wallets don’t give that assurance. All presentations that are not ZKP are potentially linkable.  
* Lee: I think that what Nick was suggesting is that the browser should provide a signal that this has happened (new browser session/private mode) \-\> wallet. So the wallet would be able to respond to it. But browsers would probably always set it to true, so we wouldn't get any benefit from it.  
* Christian: Wouldn’t it be our recommendation to use a different key?  
* Lee: Yes, but wallets don’t. Google, maybe doesn’t, Apple definitely doesn’t.  
* Lee: Maybe we should say for non-identifying presentations, always use a separate key.  
* Lee: But this is going against private browsing: the user is explicitly providing identifying information.  
* Christian: This is a general problem.  
* Lee: Agreed.  
* Tim: Similar with WebAuthn related origins: any data from outside the browser, it can’t make any assurances about it. Browsers are free to provide extra prompts, just like with saving files in private browser sessions. Due to the layering, I don’t think we can do much more.  
* Heather: It seems that this PR doesn’t address what we need. Is there someone that can write the text that addresses this discussion?  
* Tim: I can do it.  
* Mohamed: I can close this one.  
* Brian (from chat): Dunno if it'd be helpful for the text for the last issue but [https://www.rfc-editor.org/rfc/rfc9901.html\#name-unlinkability](https://www.rfc-editor.org/rfc/rfc9901.html#name-unlinkability) has some treatment of the concept

From chat:  
Brian: dunno if it'd be helpful for the text for the last issue but [https://www.rfc-editor.org/rfc/rfc9901.html\#name-unlinkability](https://www.rfc-editor.org/rfc/rfc9901.html#name-unlinkability) has some treatment of the concept

### [Security: Prevent opaque origins from interacting with the Digital Credentials API \#535](https://github.com/w3c-fedid/digital-credentials/pull/535)

* Heather: No objections from last week’s call, and it’s been reviewed. Any objections?  
* Christian: Is this about DC API, not OS-level APIs that use the same interface? The OS API might have a need for opaque APIs.  
* Tim: Yes, only the input to the JS API.  
* Mohamed: What do you mean OS-level?  
* Christian: App calling another app.  
* Mohamed: So the origin would be the app, right?  
* Christian: Oh, yeah.  
* Matt: Do we have the same limitation that web extensions can only request origins from their extension ID?  
* Tim: Yes, the workaround is popping open a new browser tab.  
* Rene: It’s still a problem on some browsers for WebAuthn.  
* Rene: I don’t think this is an issue with VCs, since they’ll be primarily used for account recovery/onboarding, as far as I understand. It won’t be a daily operation. So we can pop open a browser tab for this flow. Different from WebAuthn, where the operation might be multiple times a day, so a smoother UX is desirable.

### [Add verifier hardening guidance for script injection\#539](https://github.com/w3c-fedid/digital-credentials/pull/539)

* Matt: Probably the best we can do. We should recommend CSP where we can, but browser extensions aren’t subject to CSP. There are other scenarios that this wouldn’t address, so this would be good to add.  
* Tim: Since we haven’t formally moved forward on protecting the DC API JS interface, we should call that out.  
* Heather: Tim, Marcos, Mohamed should do a full preview and approve or not.

### [Add Internationalization Considerations section\#541](https://github.com/w3c-fedid/digital-credentials/pull/541)

* Heather: No concerns on the previous call or this one. Mohamed and Tim, once approved, this can be merged.

### [Expand Accessibility Considerations section\#542](https://github.com/w3c-fedid/digital-credentials/pull/542)

* Heather: No concerns on the call or this one. Mohamed and Tim, once approved, this can be merged.

## Any Other Business (AOB)

* The WBS for our poll on response encryption is now live: [https://www.w3.org/wbs/154550/fediddcapienc/](https://www.w3.org/wbs/154550/fediddcapienc/) . Poll is open from July 13-27; for organizations with multiple representatives, the last person to respond from that organization will be recorded as the only vote from that organization.   
  * Tim: “The specification recommends that the user agent encrypts the response”: the user agent doesn’t encrypt, it’s the client.  
  * Heather: I’ll drop a note to the mailing list to note that this is primarily for the DC API. Any WG member is welcome to respond, but they’ll need to read the context.  
  * Wendy: For context, we tried to reach consensus in other ways, but we could not achieve it, so we’re going to a vote  
  * Tim: Can we link to the issues and discussions in the email to make sure people have the right context?  
* Meeting Minutes  
  * Matt: Is there a central place to view links to all the meeting minutes?  
  * Heather: GitHub [https://github.com/w3c-fedid/meetings](https://github.com/w3c-fedid/meetings)  
  * Heather: We also link to the related issues in GitHub so they’re visible.

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Wendy Seltzer (co-chair)  
* Helen Qin (Google Android)  
* Lee Campbell (Google Android)  
* Brian Campbell (Ping Identity)  
* Tim Cappalli (Okta)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* John Schanck (Mozilla)  
* Christian Bormann (SPRIND)  
* Mohamed Amir Yosef (Google Chrome)  
* Ryan Watkins (Mastercard)  
* David Waite (Ping Identity)  
* Rene Leveille  
* Bjorn Hjelm  
* George Fletcher  
* Isaiah Inuwa  
* Matthew Miller (Cisco)  
* 