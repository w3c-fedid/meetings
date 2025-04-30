# FedID WG Telecon — DC API Series B, 2025-04-30

* Moderators: Heather Flanagan

* Scribe: Wendy

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)? Wendy, …   
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API PR (FPWD Blocker) (5 minutes)  
  * [Include Digital Credential Issuance in the Spec](https://github.com/w3c-fedid/digital-credentials/pull/204#top) \#204  
* DC API Issues (10–12 minutes each)  
  * [Add isProtocolSupportedByClient static method \#219](https://github.com/w3c-fedid/digital-credentials/issues/219)  
  * [Support for multiple requests in a get call \#220](https://github.com/w3c-fedid/digital-credentials/issues/220)  
  * [Handling Multiple Credentials from Different Wallets in DC API Presentation Responses \#222](https://github.com/w3c-fedid/digital-credentials/issues/222)  
* Any Other Business (AOB)

# Notes

## Administrivia

Heather: This is the DC API. Membership, Code of Conduct. 

## Ecosystem Updates

* Lee: Android blog saying we support DC API; Chrome blog on cross-device support, CTAP.  Samsung, 1Password, Amazon, Uber, CVS using or about to go into production.   
  * [https://android-developers.googleblog.com/2025/04/announcing-android-support-of-digital-credentials.html](https://android-developers.googleblog.com/2025/04/announcing-android-support-of-digital-credentials.html)  
  * [https://developer.chrome.com/blog/digital-credentials-cross-device-ot?hl=en](https://developer.chrome.com/blog/digital-credentials-cross-device-ot?hl=en)  
  * [https://blog.google/products/google-pay/google-wallet-age-identity-verifications/](https://blog.google/products/google-pay/google-wallet-age-identity-verifications/)   
* Matt: Will be curious to see how these vendors in early announcement will communicate to people, terminology  
* Lee: Depends a bit on what credentials they're asking for. Early ones are asking for a US driver's license. Why they’re asking: KYC, “to validate who you are”. Google is using it for age verification flow; one of the options is to present your mobile driver's license. Amazon has an account recovery flow. The language depends on context. Not like a passkey, with a logo.   
* Nick: I asked during demos, for sites explaining what the data is being used for, where it goes. Do any sites now do that?   
* Lee: Not having seen the fully launched sites, not sure. Google’s site says what they’re requesting, why and how they’ll use the data. At least with US MDLs, there’s no policy around it.  We’ll share examples as we see them go live. We have the opportunity to offer guidance to early adopters.   
* Nick: It would have been preferable to do that prior to launch (as I previously requested), but I am willing to do that now as well.  
* Heather: How will we do the review? In an issue?   
* Lee: I can report back as I see examples. Can even try to get folks on calls?  
* Heather: Can we get folks on calls even before they go live?  
* Lee: Maybe.  
* Bjorn: With the change to WG, did the charter of the CG also change? It seems the heads-up would be a fitting topic for CG  
* Heather: The FedCM CG didn’t change; the WICG DC topic group is basically closed

## DC API PR — Issuance: [Include Digital Credential Issuance in the Spec](https://github.com/w3c-fedid/digital-credentials/pull/204#top) \#204

* Tim: This is the last thing before we can cut the public working draft  
* Sam: Blocked by Marcos who wanted to take another pass? There are some approvals already  
* Lee: We should probably wait until Mohamed gets back to land it  
* Heather: Confused about what’s left to act on  
* Tim: Just noted some nits, but otherwise waiting for Mohamed to hit Merge button  
* Sam: Would it be cool to sync with Rick to address the changes and merge the PR?  
* ***Action Item:** Someone please chase down Mohamed to get this back on his radar*

## DC API Issues

* [Add isProtocolSupportedByClient static method \#219](https://github.com/w3c-fedid/digital-credentials/issues/219)  
  * Tim: I thought we had agreement on this at the F2F  
  * Lee: We need Marcos here to discuss this  
* [Support for multiple requests in a get call \#220](https://github.com/w3c-fedid/digital-credentials/issues/220)  
  * Matt: Right now, the API is set up to allow multiple requests, but if you try to do so, it errors out. It would be great to allow a verifier to specify both an AnnexC and OID4VC in the same request, and then act on what comes back. Because of AnnexC, we should try to divine behavior here. Related to \#222 from Mohamed. Also, multiple presentations seems underdefined in API  
  * Tim: The latter, we should split out separately  
  * Matt: I’m asking for or, i.e., multiple requests, but only one yields a response.  Would also be beneficial, when we have upgraded protocols, to accept one of several versions  
  * Tim: Should it be an exclusive or, i.e., you can get only one  
  * Matt: If you allow multiple requests and it’s either/or, there should be meaningful enforcement that it’s the same set of claims requested across protocols.   
  * Tim: Should be limited to one request per protocol-identifier  
  * Matt: Would it be desirable across those examples, for it to be the same request?  
  * Lee: It could be different credentials, there could be some requests that could be satisfied in only one, e.g., you could say I want European credential *or* US driver license  
  * Matt: Where the credentials don’t line up, no meaningful enforcement?  
  * Lee: I think I’d even be ok with multiple requests per protocol.   
  * Tim: The multi-trust-framework example  
  * Matt: Seems it’s a matter of browsers catching up to the intent  
  * Sam: I think the browser just passes everything to the OS  
  * Lee: There was a bug in Chrome, now fixed, that only passed the first element of the array  
  * Sam: As far as Chrome is concerned, you can put whatever you want in the array  
  * Matt: I’m looking for anything in the current spec that discusses multiple requests..   
  * Tim: That was my mistake, not in there.   
  * Matt: I don't know that I have a strong preference, just want to see expectations laid out. If multiple requests are either/or, should the verifier expect only one response?  
  * Sam: Yes. Different wallets may handle different protocols, respond with one or the other  
  * Matt: My issue is that we consider defining that behavior in the spec, so the verifier knows what to expect. If that sounds right, happy to try  
  * Tim: Does that belong in digitalcredentials.dev?  
  * Sam: I don’t think that’s normative  
  * Lee: Today, the API allows you to return multiple credentials in a single response. A single wallet could return, say, a passport and a driver’s license. Where there’s an API limitation is if you need to get creds from multiple wallets, then you’d need to return an array of multiple responses.   
  * Tim: Given the split among specs, a verifier can’t realistically implement from only one spec, so that’s deployment guidance  
  * Helen: When there are multiple requests, does that have to be enforced by the browser? Maybe the array should be in order of preference? That kind of makes sense to be in the spec  
  * Matt: Where I’m coming from, a verifier who hears that parties are accepting digital credentials, will come looking for a W3C spec. Can we add an editorial note along the lines of "DC API can do only so much. You also need to look at X, Y, Z"  
  * Sam: Editorial notes in the spec sound reasonable to me. Don’t we have similar issues between WebAuthn and FIDO?   
  * Tim: Not really  
  * Sam: I empathize with the question. There’s something that needs to be normative, but we don’t have a place for the norm  
  * Tim: If the list is ordered, and order has meaning, that belongs in the spec; but “here’s what you can expect”, not necessarily  
  * Lee: You can write the behavior of multiple entries in the spec. You can only get results from one. In any one of those queries, you could get multiple credentials.   
  * Matt: That makes sense, so an editorial note describing that.   
  * Matt: I think we should include the normative guidance: "*if you put multiple requests, the processing order will look like this.*"  
  * Lee: Or normative, the responses can contain multiple credentials.   
  * Heather: Matt, can you propose text?  
  * Matt: Yes  
* [Handling Multiple Credentials from Different Wallets in DC API Presentation Responses \#222](https://github.com/w3c-fedid/digital-credentials/issues/222)  
  * Matt: let’s wait for Mohamed  
  * Lee: You can get a response, which may contain multiple credentials, from a single wallet. Mostly because the protocols support response encryption, provided by the wallet. It’s a limitation of the OS/platform, that if there are responses from multiple wallets, each will be separately encrypted, and cannot  be returned together. So different proposals of what to return: array of credential objects, or an object with an array inside. My preference is to return an array at the top level. Gives more flexibility.   
  * Sam: I think we should return multiple digital credentials. Con is that it’s more work.   
  * Tim: We also have to consider the schema for a hybrid response.   
  * Sam: I just don’t know about use case demand. Why and how urgent?  
  * Lee: There are a few asks. EU wants payment \+ ID; others want telephone number \+ other ID; and phone numbere is always its own response. Hybrid needs support because you can’t expect multiple taps, even if on the web you could make multiple calls.  
  * Matt: There wouldn’t be an intent to allow credential representations that are not explicitly requested?  
  * Lee: Right, only if the request asks for multiple things from multiple wallets.   
  * Matt: If DC API currently returns a credential where the response would be an array…  
  * Nick: It doesn't seem beneficial to the user to be able to provide multiple documents in a single response. Anti-feature to hand over my driver's license and passport at the same time.  
  * Lee: At the airport, passport and boarding pass; alcohol payment and proof of age. On the web, one-click account creation with email, proof of age… Today, lots of calls and consents.   
  * Nick: Great example. Websites want lots of information, and they want a single-click request, that’s exactly where we have concern. We don’t want to ease the provision of multiple credentials without individualized consent.   
  * Sam: \+1 to Nick’s intuition around account creation. Better off having the user accept each thing independently. Doesn’t this architecturally break the layering with openid4vp?   
  * Lee: Don’t think custom schema can do this  
  * Sam: Then how does it degrade gracefully?   
  * Lee: There are some use cases that only work with DC API  
  * Tim: We can continue this debate around multi-use digital ID government credentials, but probably useful for an age-only credential.   
  * Helen: Autofill-equivalent, we’re trying to recreate one-click experience  
  * Wendy: Sympathizes with Nick, we’re not trying to reduce the friction of asking for credentials, it’s important to think about how consents and appropriate amounts of friction are left in  
  * Heather: Definitely want to come back to questions of “what are valid multiple presentations in a single tap?”

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Tim Cappalli (Okta)  
* Helen Qin (Google Android)  
* Lee Campbell (Google Android)  
* Wendy Seltzer  
* Matthew Miller (Cisco)  
* Nick Doty (CDT)  
* Monty Wiseman (Invited Expert)  
* Sam Goto (Google)  
* Björn Helm (Yubico)