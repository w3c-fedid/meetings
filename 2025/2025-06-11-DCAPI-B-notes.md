# FedID WG Telecon — DC API Series B, 2025-06-11

* Moderators: Wendy Seltzer

* Scribe: Helen, Matt Miller


Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
    * Helen Qin  
    * Matthew Miller  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Upcoming meeting schedule  
    * summer meetings  
    * meeting during IETF 123  
* Ecosystem Updates (5 minutes)  
* DC API PRs (10 minutes each)  
  *  [Add guidance on how to handle multiple presentation request entries \#249](https://github.com/w3c-fedid/digital-credentials/pull/249)  
  * [Add a11y guidance for user agents \#238](https://github.com/w3c-fedid/digital-credentials/pull/238)  
  * [Add clientAllowsProtocol static method \#221](https://github.com/w3c-fedid/digital-credentials/pull/221)(related issue: [Add isProtocolSupportedByClient static method \#219](https://github.com/w3c-fedid/digital-credentials/issues/219)0  
* DC API Issues (10 minutes each)  
  * [privacy review for registry inclusion \#226](https://github.com/w3c-fedid/digital-credentials/issues/226)  
  * [Write privacy considerations \#183](https://github.com/w3c-fedid/digital-credentials/issues/183)  
* Any Other Business (AOB)

# Notes

## Administrivia

* 

## Ecosystem Updates

* Marcos:  
  * Apple WWDC announced Digital Credentials API operating on MDOCs  
    * Video: [https://developer.apple.com/videos/play/wwdc2025/232/](https://developer.apple.com/videos/play/wwdc2025/232/)   
  * Tim: Way to play & test with apple wallet?  
  * Marcos: There will be some documentation  
  * Nick: Availability?  
  * Marcos: You need to apply and request a certificate with Apple. There is a test certificate too. Can also make your own app to issue mdocs.  
  * Lee:   
    * Is the Apple business certificate only to request mdoc from apple wallet or any wallet?  
      * Marcos: Need to get clarity on that. *Think* it’s for all wallets but not sure.  
    * Did you wire up all the hybrid stuff   
      * Marcos: Yes.  
  * Rene: Plan for SD-JWT support?  
    * Marcos: Not at this point  
  * Christian: Does the OS need to understand protocol and format?  
    * Marcos: Yes. We parse the whole request and would strip away unknown parts of the request.  
  * Matt: Safari doesn’t support oid4vp so wallets can’t support that on Apple. Is there a higher bar for apps to become a wallet?  
    * Marcos: Will gather the requirements  
  * Rick  
    * Is raw request also parsed and filtered by webkit? It’s not what the verifier originally sent?  
      * Marcos: Yes. It is (re)structured.  
      * Lee: I thought the raw request is just the raw data  
      * Marcos: That’s right  
    * How does this impact extensibility? What happens if a new field is added  
      * Marcos: it needs to be added support by webkit and the OS  
      * Lee / Rick: Just webkit?  
      * Marcos: The standardization process governs this too  
      * Rick: But what is the latency after the standardization makes a change? Does that require waiting for another OS release? So the raw request doesn’t seem to be truly a raw request.  
    * What happens to a desktop Safari request that contains protocols unsupported by Safari? Does it allow cross-device?   
      * Marcos: We drop it  
  * Tim: Implementation is different from the published protocol. Previous one was dash and the latest is period.   
    * Marcos: Should be updated.  
  * Rene: At the beginning of the video, requests from a Mac would be automatically received from an IOS device without going through hybrid. How does that work?  
    * Marcos: Need to check, but I think if there’s a known wallet with a known credential it automatically shows up. QR should always show when there’s not a known device.  
    * Tim: Is this just a hybrid prelink?  
    * Marcos: Not sure. Need to find out.  
    * Rene: For a followup, When a DC API request originates from a Mac and gets automatically picked up by an iPhone, is it an automatic hybrid pre-link? If not, would it be possible to have a well documented explanation of the implementation’s security properties of the transport used to connect the two devices to field the request?

DC API PRs and Issues

* DC API PRs (10 minutes each)  
  *  [Add guidance on how to handle multiple presentation request entries \#249](https://github.com/w3c-fedid/digital-credentials/pull/249https://github.com/w3c-fedid/digital-credentials/pull/249)  
    * Matt: Need guidance on how to make requests with multiple protocols especially for annex-c and oid4vp  
    * Lee: Isn't this already defined as OR? You can put annex-C for Apple and Oid4VP for Android.  
    * Matt: Couldn’t find it  
    * Lee: We implement it as OR. Maybe it’s not explicitly defined. We have intended this and aligned on this.  
    * Matt: Yeah, this is the PR to add the text  
    * Nick: Are different requests all intended to be semantically the same? Or can they ask for totally different pieces of data?  
    * Lee: Both. You could request an mdl over Annex-C and an SD-JWT using Oid4VP. It’s also valid to say I’ll take the exact same mdl using Annex-C and OID4VP.  
    * Nick: seems confusing and could cause over asking if you could ask for different things.  
    * Lee: Even just with openid4vp, you could ask for multiple things. Also, another problem is that you can be requesting the same credential, e.g., mdl over 2 different protocols and they can have different privacy properties. Unsure how we should handle that.  
    * Matt: It’s hard to programmatically decide what’s semantically the same.  
    * Tobias: Supportive of treating this as explicit OR to reduce complexity. Also, what happens on Safari? Would it error out or drop the request?  
    * Marcos: We need to collectively make a decision here and do it on Safari. It might drop now.  
    * Lee: Aren’t XOR and OR basically equivalent?  
    * Tobias: What’s the benefit of having this at both the request level and dcql level?  
    * Lee: We may just mean the same. What will happen is the system will show all options, and the user will pick only 1 and get it returned. XOR imo means the system will only show results from 1 request.  
    * Tobias: Agreed, sounds like we have alignment.  
    * Lee: To be clear, we are only returning 1 result from 1 \`request\` entry. This request could be an OID4VP request and allow the 1 result to contain multiple credentials.  
    * Matt: This sounds like platform behavior and can we specify platform behavior here? I was only thinking about it at the user agent level.  
    * Lee: This is just the DC level requirement.  
    * Matt: Sounds good.  
  * [Add a11y guidance for user agents \#238](https://github.com/w3c-fedid/digital-credentials/pull/238)  
    * Matt: Waiting for review.  
    * Marcos: Thanks and left comments. Our API doesn’t present the UI; we hand it to the Credential Management API. We need to look at the Credential Management API to see if it provides the proper guidance. We need to layer it correctly and may defer to other spec. Also, whether QR code is in scope and what’s the accessibility property for that  
    * Tim: QR code isn’t in the web API layer. Also QR code has proven to have good accessibility   
  * [Add clientAllowsProtocol static method \#221](https://github.com/w3c-fedid/digital-credentials/pull/221)(related issue: [Add isProtocolSupportedByClient static method \#219](https://github.com/w3c-fedid/digital-credentials/issues/219))  
    * Tim: Last time, some didn’t like the name, so I renamed it and removed the async  
    * Nick: PR looks good. Wondering if extensions can participate in (change the value of) the capabilities?  
    * Tim / Rick: No. Or rather, they will just capture/inject/overload the method to return a different value. (Nick: which will insert some privacy risks there as well.)  
    * Marcos: Looks good to me.  
    * Rick: Will land this in Chromium soon after this PR merge  
    * Tim: Can Safari have this soon?  
    * Marcos: We need to make a test first.   
    * Marcos & Rick: Can’t test about a random (banana) protocol since Chrome will support that. Let’s add a test about the string rules.  
* DC API Issues (10 minutes each)  
  * [privacy review for registry inclusion \#226](https://github.com/w3c-fedid/digital-credentials/issues/226)  
    * Johann: [https://github.com/w3c-fedid/digital-credentials/issues/255](https://github.com/w3c-fedid/digital-credentials/issues/255) is similar issue to this one. The proposed review process differs from what we have today. So we should tighten up our definition to not deviate as much.   
    * Nick: Both the process steps, and also substantive details need to be addressed. Not sure we have consensus, though, that protocols should be in the registry before they’re supported. Chrome will support every protocol; Safari will support the ISO protocol, whether or not it’s in the registry. If implementations don’t care about what’s in the registry, then it’s questionable whether it’s important for the protocols to be in the registry before they’re supported.  
    * Johann: Feels like a reasonable path to take   
    * Lee: What do we do about OID4VP? It’s going to go out before v1 is finalized. It’s not as if we won’t put 1.0 in the registry.  
    * Mike Jones: OID4VP vote has not started. You can email the membership to vote No.  
    * Lee: Window is closing soon, a month or so  
    * Johann: At the DC layer, there’s a limited amount of influence we have over user privacy. Realistically, the only thing we can do is put requirements on protocols for their inclusion in the registry. We should define the requirements to encourage protocol authors to consider the requirements when continuing their work.  
    * Lee: Annex C is done, limits our ability to influence it. It’s unclear what we should do in situations like this if we want to encourage changes.  
    * Christian: We have one month for OID4VP 1.0, we can still make changes to some degree. We should try to use this   
    * Tim: We have nothing in the registry, should that be a blocker?  
    * Johann: Probably not.  
    * Tim: The alternative is none of this matters because everyone is using custom schemes.  
    * Nick: Assuming things will be addressed in the protocol, but things don’t shift or aren’t addressed in the protocol, then we should admit and say we have to address privacy issues in alternative ways.  
    * Johann: Protocols can’t necessarily fix all the privacy issues, so DC API also has a limited ability to address privacy issues. To Tim’s point, Annex C support is already shipping so we can’t really do anything there. Doesn’t seem viable.  
    * Lee: OID4VP wraps in a month, they need to reference DC API FPWD.  
    * Rick: We’re already seeing wallets in Europe implement custom schemes.  
    * Tim: Do we have a clear understanding of blockers for FPWD? Can we focus on this in the next meeting? We need a check-in on where we are for all of the privacy work.  
    * Johann: Not advocating for blocking the FPWD. We’re trying to do the work of meaningful privacy considerations. FPWD should mention this work but not block.  
  * [Write privacy considerations \#183](https://github.com/w3c-fedid/digital-credentials/issues/183)  
    * 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer  
* Helen Qin (Google Android)  
* Lee Campbell (Google Android)  
* David Waite (Ping Identity)  
* Matthew Miller (Cisco)  
* Rick Byers (Google Chrome)  
* David Moore (IBM)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Johann Hofmann (Google Chrome)  
* Nick Doty (CDT)  
* Rene Leveille (1Password)  
* Simone Onofri (W3C)  
* Christian Bormann (SPRIND)  
* Tobias Looker (MATTR)  
* Mike Jones (Self-Issued Consulting)  
* Sandor Major (Google Chrome)  
* Tim Cappalli (Okta)