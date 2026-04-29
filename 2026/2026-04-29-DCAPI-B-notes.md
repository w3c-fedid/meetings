# FedID WG Telecon — DC API Series B, 2026-04-29

* Moderators: Wendy Seltzer

* Scribe: Tim

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
  * [Define "present credential requests" algorithm.\#419](https://github.com/w3c-fedid/digital-credentials/pull/419)  
* Any Other Business (AOB)

# Notes 

## Administrivia

* WG membership and Code of Conduct

## Ecosystem Updates

* Mohamed: successful demo at IIW of PXP using offline BLE for a VDC presentation ([link](https://photos.app.goo.gl/nPkB928pv4QgX9uR7))  
* Helen: Google shipped verified email on Android which uses the DC API similar to the phone number verification. Represents your verified Gmail account: [Retrieve a verified email using digital credentials | Identity | Android Developers](https://developer.android.com/identity/digital-credentials/email-verification). Currently native only, web soon. OID4VP \+ SD-JWT VC. 

## 

## DC API PRs and Issues

### [Define "present credential requests" algorithm.\#419](https://github.com/w3c-fedid/digital-credentials/pull/419)

* Confirmed only one origin.  
*  \[discussion of the name\] execute or run? Initiate?  
* Marcos: When this is merged, unblocks us on the JS, getting ready to move to CR. There will be a few tweaks as we review security, privacy, but the algorithms should be set.  
* Tim: added approval pending name change.  
* Tim: We need to think about whether we want to bring client data back. 

Ventured into next steps discussion:

* Wendy: TPAC coming up. We should think about what we can do ahead of that in terms of issue triage and preparing for CR or Rec.  
* Tim: First step is triaging issues.  
* Lee: Two big breaking changes: clientData, and returning multiple responses.   
* Helen: Also wallet token binding.   
* Marcos: clientData might not be as big of a change. Don’t think it’s blocking for CR.  
* Mohamed: Need to address backwards compatibility, cross-device, etc.  
* Tim: Where do we draw the line on versioning with a living spec?  
* Mohamed: CR is a top priority, focus on what gets us to CR.  
* Marcos: To get to CR, need horizontal review. Need to have good answers for PING, etc.  
* Marcos: May get together for an interop in June with Mohamed.  
* Wendy: What issues get closed when we close 419?  
* Marcos: List of threats addressed by XYZ. Can very explicitly map these out, address security considerations, gaps, etc?  
* Wendy: Do we have people identified who can do that mapping?  
* Marcos: Need volunteers and coordinator.  
* Wendy: Will ask Simone to help with that.  
* Marcos: We meet weekly re: security. Need someone with privacy background.

ClientData

* Tim: Are we OK with clientData now? Don’t want to do it again just for it to be dropped.  
* Lee: Need to return clientData in the response (not just hash).  
* Tim: To make it valuable, we’d need to change the protocol to sign over. Step 1, return it, then determine whether it’s signed.  
* Marcos: If it’s just an additional property that appears…  
* Tim: …then it’s optional  
* Lee: Probably always return it, but you wouldn’t have to use it  
* Marcos: Think about the implications, requirements. Detail that in the issue, including potential breakage, backwards compatibility…  
* Lee: I think it’s non-breaking at the DC API level, have to look at the other protocols. Up to protocols to decide whether to use it.   
* Tim: I think we need to change PXP, a fairly minor change.  
* Lee: Probably.  
* Tim: And think about whether we have to allow ignoring unknown members…   
* Wendy: Is that the last major change?  
* Lee: Wallet binding.  
* Tim: Returning multiple responses, requires changing the text and writing up backwards compat. Do we have a wallet-binding proposal that can be standardized?

Wallet Binding

* Lee: Talked to Hicham about it. Change the language in what we have now. Instead of calling it “key”, use a nonce from the wallet that gets mixed with platform authenticator. Takes a challenge and returns back something platform-dependent.   
* Mohamed: Then RP has to deal with both.  
* Lee: Response is always platform-dependent. Someone would have to define each of these. We probably don’t want it in the spec. WebAuthn has attestations, and we regret putting that in the spec. I think we want to put non-normative references in the spec instead.   
* Helen: How the binding-token is generated is left to the platform.   
* Tim: We should probably do an explainer and get a TAG review. Can Lee and Hicham write that up?   
* Lee: Yes, we will.

Multiple responses

* Lee: For multiple responses, we basically want an array.  
* Tim: [Handling Multiple Credentials from Different Wallets in DC API Presentation Responses · Issue \#222](https://github.com/w3c-fedid/digital-credentials/issues/222)   
* Lee: I think it has to happen at the DC API level for aggregation.  
* Tim: Data is a JSON-serialized string.  
* Lee: One more potentially breaking change. Base-64 creates overhead. A good chance that the new harmonized protocol could be CBOR. Annex C’s top-level encoding is CBOR. 30% overhead for Base64. This is a big deal when taken over hybrid. Let me think about whether there's a reason to return raw bytes rather than a JSON string.   
* Wendy: Please raise an issue for that thinking.  
* Tim: Is that potential v2?  
* Lee: Yes.  
* Mohamed: How does that affect PXP?  
* Lee: I’ll think about it offline, raise an issue. Most of the time, it’s not going to be an array, only one element. Do we have guidance?   
* Helen: A bunch of use cases rely on encrypted responses. Some want even errors to be encrypted. E.g. RP isn’t the real caller and knows its a successful response, and could derive information and proceed. Just knowing there’s an encrypted response can be enough to bypass billing and other things.   
* Lee: Has to be handled one layer below. One of the presentations could be for another party. Difficult to solve, but different layer problem (could be credential format).  
* Helen: Tricky that you have errors cascading across layers (e.g., DC API has platform errors, protocol layer has its own errors). May need to be more restrictive about errors at the DC API.   
* Tim: There aren't that many at the DC API layer, are there?  
* Helen: On Android, could technically return even DOM errors; the platform could still return errors that make sense.  
* Lee: Feels like it can’t be a DC API problem. Already don’t leak any info at the DC API level.  
* Marcos: The catch-all is an operation error.  
* Helen: Maybe requires some guidance to the wallet.  
* Marcos: Part of the learning will be what the wallets send back.   
* Wendy: Will work with Heather and W3C team to roadmap the steps to CR (testing, reviews, issue triage)


## AOB

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Tim Cappalli (Okta)  
* Lee Campbell (Google)  
* Helen Qin (Google)  
* Mohamed (Google)  
* Marcos Caceres (Apple)  
* Caryn Van Exel (GS1 US)   
* 