# FedID WG/CG Telecon, 2026-05-19

* Moderators:  Heather Flanagan

* Scribe: Ben, Heather

* Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

* Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * [FedID CG/WG process](https://github.com/w3c-fedid/Administration/blob/main/proposals-CG-WG.md)  
* Ecosystem Updates (10 minutes)  
* Discussion (40 minutes)  
  * [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)  
* Any Other Business (AOB)  
  * Use of .well-known \- [https://github.com/w3ctag/design-reviews/issues/1217\#issuecomment-4485020351](https://github.com/w3ctag/design-reviews/issues/1217#issuecomment-4485020351) 

# Notes

## Administrivia

* W3C Code of Conduct

## 

## Ecosystem Updates (10 minutes)

* Heather: Any implementers that want to chime in about interesting FedCM ecosystem updates?  
* Suresh: Would this apply to subdomain .well-known discovery?  We've made the changes and are reaching out to the 1P partner (Microsoft) to begin testing  
* Suresh: Christian, did you have questions regarding fallback?:   
* Christian: In what cases should the subdomain fallback to the apex domain?  
* Suresh: 1\) If there are network issues, 2\) if the response seems to be not correct  
* Christian: Agree we should fall back if the domain is missing or the file is missing.  But should we fallback if the file is invalid.  What does invalid mean?  
* Alex: And can we tell if the file is valid based on the limited context available.  For example, is DNS failure a missing subdomain or a temporary problem?  
* Christian:  Agree, but I think we should fall back in those cases even if its a transient problem because we can't tell.  But what about a malformed file?  
* Alex: What is the proposal?  
* Christian:  No proposal yet, but thinking it through.  The goal is to fallback from new location to old location for IDPs that have not been able to update yet.  
* Heather: And should an invalid JSON trigger fallback?  
* Christian:  Correct.  
* Alex: Who could answer the question of what’s proper?  
* Ben: Does this get into file schema versioning issues in the future?  
* Heather: I think we get to decide what is proper.  
* Alex: Sorry, I meant is there a large IDP that could give us a signal as to what they think is correct.  
* Heather: Good question.  Part of the issue today is that Google and Microsoft (two large IDPs) do things differently.  
* \<Pam from MS Identity joins, Christian summarizes issue, how do we define failure and what is the best thing to do here\>  
* Phil: Isn't there already a failure if the web identity file can't be found?  Wouldn't the same failure mode work the same for invalid JSON?  
* Christian: Let me explain my thinking.  If an IDP puts a file in a new location then they will probably want it to be used.  So there is no point in falling back to the old location.  That was my thinking, so maybe it doesn't make sense to fall back?  
* Pam: Maybe we need to model it because there might be some attack vectors.  For example, if the attacker can stand up a subdomain and its a evaluated as a replacement for a root domain, then perhaps that is a vector.  But I don't see a downside for falling back to the root.  If it was the other direction, though, that might be a concern.  But   
* Ben: What about old clients when the IDP had put a new file in a new location? Do IdPs have to keep the old stuff around?  
* Christian: yes, to the extent they care about old locations.  
* Christian: but old clients can't really we use FedCM, but its unclear to what extent this concern will happen  
* Pam: So would it be useful to talk through the use cases offline and bring back to the meeting?  
* \<consensus to look offline and bring back\>  
* Heather: Who wants to volunteer?  
* Pam: I'll take a first look  
* Suresh: I can create an issue for this  
* \<fin\>

## Discussion (40 minutes)

### [Enabling IDP Interception in FedCM Request \#815](https://github.com/w3c-fedid/FedCM/pull/815)

* Heather (from email to the list) PR \#815 proposes a mechanism that would allow Identity Providers to handle certain FedCM requests using a Service Worker-based mechanism. The motivating use cases include request signing / proof-of-possession patterns such as DPoP, operational failover, geographic or jurisdiction-specific routing, caching during outages, and integration with legacy identity systems. The discussion in the PR, which is extensive, has raised detailed questions across FedCM request processing, Service Worker dispatch, Fetch semantics, privacy, and IDP security expectations. Some of the detailed reviews appear to depend on higher-level direction from the WG.  
* Easier link for review (from chat) \- [https://github.com/w3c-fedid/FedCM/blob/main/explorations/identity\_handler.md](https://github.com/w3c-fedid/FedCM/blob/main/explorations/identity_handler.md)    
* Scribed minutes:  
  * Heather: This issue got very long and it's a bit confusing at this point.  It seems like we need to step back and consider the higher level issues.  I'm hoping we have the right set of people in the room to start this conversation.  Suresh, can you summarize?  
  * Suresh: Let me start with the need for the service worker.  Please open the [explainer](https://github.com/w3c-fedid/FedCM/blob/main/explorations/identity_handler.md).  
  * Suresh: Today, when the browser opens an endpoint the request is sent with serviceworker=none.  With service worker support this would help IDPs to authenticate by using different custom or more complex schemes.  \<Mentioned a protocol or standard I missed\>  Can handle cached responses.  If the IDP is not ready for FedCM, then the SW can act like an adapter/proxy for legacy IDP services.  
  * Suresh: So just flipping serviceworker=none to fetch won't work because the request does not come from a page (client).  So its not a subresource request.  
  * Suresh: The second approach, I made a bunch of infrastructure changes to route to fetch event handler.  When I proposed this to the SW WG this seems similar to foreign fetch.  This feature was not launched previously due to privacy concerns.  
  * Suresh: This last approach we are trying is like payment handler.  SW WG suggested maybe this use case is similar to payment request.  It will trigger a service worker handler and then the fetch can be sent, etc.  
  * Suresh: Now comes to the open design questions: 1\) How does IDP make a SW registration?, 2\) What should the event dispatch event be?  Should it be a FetchEvent?, 3\) On the security side, when the UA creates the request we can't compromise on the destination, origin, cookies, etc.  Should still hold these properties intact?  
  * Christian: Did we cover the concern with SW being able to set Sec-Fetch-Dest to "webidentity"?  
  * Suresh: Yes, this is necessary.  Normally this is set via the request constructor.  This changes a bunch of the security related issues like dest, origin, etc.  Therefore the request constructor will change the values automatically to things like destination none, etc.  This is an open question, though.  
  * Alex: Asking Ben a question.  We have a few properties that we staple behind the fetch and request API.  My recollection of how we wire things up is there are a bunch of properties that don't get sent to the server at all, but are not sent to   
  * Ben: When the request is put on the Fetch Event?  
  * Alex: yes, there are things we hide from you and things that only get put in when we make the request.  
  * Ben: There are things that are hidden but get passed through, like Fetch Priority, but destination that has an open SW issue around it. When you have a nav event and intercept it with a fetch event, the destination goes away or becomes none. That’s the same problem we have here.   
  * Christian: I find this important because, if you don’t send sec-fetch-dest identity, the IdP has no way to know this came from FedCM, and so the IdP can’t tell the difference between browser mediated API and something else. It’s a security property. The IdP doesn’t want to share the account list with random JS calls.   
  * Ben: The concern is that fetch is very multipurpose and so it has restrictions. But FedCM is a narrow use case that we want to permit. So we should create a new FedCM that doesn’t use fetch, but says “perform FedCM request that uses some token”. We would not expect fetch unless there’s a legacy adapter type use case. Legacy wouldn’t be looking for this destination, so that’s probably fine.   
  * Suresh: This is what I’ve come up with to say we will have a new API to support this event. That’s in the spec PR and was questioned. SW is a proxy for the IdP. Instead of relying on destination, can we use a different property to say this is FedCM via SW? Then we can still use fetch.  
  * Christian: I thought we were going with a new event?  
  * Ben: But what about not using the fetch API directly and using something dedicated to FedCM with guardrails on it. Asking fetch to look at random properties passed in may be dangerous.  
  * Alex: Are we asking for that, or are we asking to preserve the destination in a specific case regardless of what the SW does?  
  * Christian: Either way would work. We should make restrict sec-fetch-dest to same origin.  
  * Alex: Is it equivalent to have destination do this job, or a new sec header would suffice for compatibility?  
  * Dominic: Why is sec-fetch-dest required here? If it is same origin as the IdP server, what more evidence do we need?   
  * Christian: When we started FedCM, we had a dedicated header. That was for non SW requests; that was implemented a few years. We told IdP to check sec-fetch-dest for security reasons. We could not do this and tell IdPs to check for same site or sec-fetch-dest. The advice gets more complicated. Same site would only be used with SW.   
  * Will: I don’t think the two modes is that hard when the second mode is opt-in. When people are talking about not using fetch, though most browser APIs were built on top of fetch in some form. Are there other standards that are not fetch?  
  * Dominic: Yes, everything in browsers is built on fetch, but the caller of fetch can supply information that no other caller can override.   
  * Ben: we have a longstanding issue of navigation requests losing destination info when going through SW. I think there will be issues with passing through info through SW because it creates surface area for security issues in the future. is there concern about people using this outside a SW? If not, maybe it’s fine.  
  * Emelia: You are making fetch calls from a SW specifically for a FedCM event. Should all fetch calls in that context of that SW automatically get the sec-fetc-dest header because they are all related to doing an identity call?  
  * Ben: There can be overlapping events for an SW. Unless you trace through all the code, it’s hard to attribute specific requests to specific events unless you’re directly passing the vevent into fetch. We try to avoid implying that. Unless we create a new kind of SW that only does identity.  
  * Dominic: There are some SWs only called by IdPs.  
  * Christian: Does SW have to make a special request to fetch a DPoP thing, or do we already have that data and can annotate the request to pass it on.  
  * Will: It’s not quite DPoP, but similar. We need to make a request to the operating system, either through a browser extension or a proprietary API. It’s fully local. In Chrome, that’s a message to a browser extension which calls an EXE.  
    * [\[MS-OAPXBC\]: x-ms-RefreshTokenCredential HTTP header format | Microsoft Learn](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-oapxbc/9a1cba52-1de9-496c-9702-e64276d30fd2)   
    * [\[MS-OAPXBC\]: x-ms-DeviceCredential HTTP header format | Microsoft Learn](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-oapxbc/f6d4a084-4c7f-4d0c-8c47-9456a7debbe0)   
  * Dominic: is sec-fetch-dest required? Do we need to preserve that?  
  * Emelia: for DPoP, you essentially end up with a "preflight" request where the dpop-nonce in the DPoP token is empty, and then the server goes "actually, you need a dpop-nonce, here's a new one", and then you make the request again with the new DPoP token, resulting two fetch calls. Each request would probably want to carry the sec-fetch-dest header. This is only if the server is asserting nonces for DPoP. (it's this: [https://www.rfc-editor.org/rfc/rfc9449.html\#name-authorization-server-provid](https://www.rfc-editor.org/rfc/rfc9449.html#name-authorization-server-provid) )  
  * Alex: I have a preference to define what we do with fetch, even if we create something new. I have a concern that if we go with a different event and behavior, that we might lose alignment with fetch.   
  * Phil: Question on the use of DPoP \- it seems overloaded in that we’re not talking about proof of possession to use session cookies; we’re not talking about OAuth.  
  * Emelia: there are many different POP things out there; what I’m familiar with is OAuth, specifically DPoP and client assertions.   
  * Dominic: still don’t know if we need sec-fetch-dest preserved or not. If we don’t, this gets simplified.   
  * Christian: it’s ok to tell them to check either same site OR sec-fetch-dest   
  * Sam: it’s not a one-way door. We can always expose a FedCM-specific fetch in the future. If Will says Microsoft doesn’t need sec-fetch-dest, we can leave that for now and come back to it later if we have the need  
  * Will: I think of sec-fetch as a new way to do cross site forgery prevention. We may at some point enforce sec-fetch to have a second level of forgery prevention, but we’re not in a rush to get rid of our old protections that solve for this now.   
  * Christian: if you’re checking for same site, it’s not the same as cross site forgery prevention?  
  * Dominic: if we can resolve we don’t need sec-fetch-dest, what about the separate SW map?   
* Notes from Zoom chat  
  * 2026-05-19 17:41:10 From Emelia S. to Everyone: naive question: can fetch() not set sec-fetch-dest or similar headers?    
  * 2026-05-19 17:41:21 From Emelia S. to Everyone: Replying to "naive question: can fetch() not set sec-fetch-dest...": (I think the answer is no)  
  * 2026-05-19 17:41:50 From Alex Russell to Everyone: Replying to "naive question: can fetch() not set sec-fetch-dest...": it can't, because various consumers process things differently based on that sort of thing.    
  * 2026-05-19 17:42:00 From Alex Russell to Everyone: Replying to "naive question: can fetch() not set sec-fetch-dest...":  (certain image and SVG scenarios)  
  * 2026-05-19 17:42:34 From Emelia S. to Everyone: Replying to "naive question: can fetch() not set sec-fetch-dest...": alrighty, thought that was the case, but it's been a while since I've read the fetch spec  
  * 2026-05-19 17:43:40 From Alex Russell to Everyone: Replying to "naive question: can fetch() not set sec-fetch-dest...": same 😅  
  * 2026-05-19 17:43:58 From Dominic Farolino to Everyone: Yeah, these are considered forbidden request headers. See https://fetch.spec.whatwg.org/\#forbidden-request-header  
  * 2026-05-19 17:44:06 From Emelia S. to Everyone: Replying to "naive question: can fetch() not set sec-fetch-dest...": it may have been 2018 when I last read it fully 😅  
  * 2026-05-19 17:44:07 From Dominic Farolino to Everyone: JS cannot manually edit these headers^  
  *  2026-05-19 17:44:11 From Will Bartlett to Everyone: Replying to "naive question: can fetch() not set sec-fetch-dest...": that's more or less what sec- means, right? Can't set any sec- prefixed headers in fetch  
  *  2026-05-19 17:44:24 From Will Bartlett to Everyone: Replying to "naive question: can fetch() not set sec-fetch-dest...": The forbidden headers are: sec- prefixed, a bunch of things that predate the sec- prefix  
  * 2026-05-19 17:44:27 From Alex Russell to Everyone:don't we already have all the surface area for issues in Fetch today? I'm concerned with forking behaviour into a sub-section of a spec where fewer eyes are looki  
  * 2026-05-19 17:44:37 From Alex Russell to Everyone: Replying to "don't we already have all the surface area for iss...": \*looking  
  * 2026-05-19 17:45:00 From Alex Russell to Everyone: Replying to "JS cannot manually edit these headers^": effectively ignored, IIRC  
  * 2026-05-19 17:48:00 From Phil Smart to Everyone: Shame rfc8473 (Token Binding) was not successful, for all tokens (cookies, etc.).  
  * 2026-05-19 17:48:43 From Will Bartlett to Everyone: dpop-nonce \== server-signed timestamp  
  * 2026-05-19 17:48:48 From Will Bartlett to Everyone: so you can't produce dpop assertions in advance  
  * 2026-05-19 17:52:10 From Will Bartlett to Everyone: \[MS-OAPXBC\]: x-ms-RefreshTokenCredential | Microsoft Learn  
  * 2026-05-19 17:52:44 From Will Bartlett to Everyone: Microsoft Entra does not care about Sec-Fetch-Dest. We do not use it for anything today, as it's still a feature that isn't ubiquitous in browers.  
  * 2026-05-19 17:52:55 From Emelia S. to Everyone: You essentially have PoPs, of which DPoP is one, Client Assertions is another (currently), and I think token binding might be another  
  * 2026-05-19 17:53:03 From Will Bartlett to Everyone: We are discussing using it in the future as it's becoming ubiquitous, but so far, we just don't use it at all.  
  * 2026-05-19 17:53:13 From Will Bartlett to Everyone:  (Same with all the Sec-Fetch-\* family)  
  * 2026-05-19 17:53:19 From Alex Russell to Everyone: Replying to "Microsoft Entra does not care about Sec-Fetch-Dest...": will you care when it is ubiquitious? Or check an alternative header should we specify one?  
  *  2026-05-19 17:53:37 From Phil Smart to Everyone: Replying to "You essentially have PoPs, of which DPoP is one, C...": Yeah, thanks. I think a good idea, just trying to work out where it fits.  
  * 2026-05-19 17:55:36 From Will Bartlett to Everyone: How to Use Sec-Fetch Headers for CSRF Protection by sergiodxa  
  *  2026-05-19 17:56:39 From Will Bartlett to Everyone:  \[MS-OAPXBC\]: x-ms-RefreshTokenCredential HTTP header format | Microsoft Learn  
  *  2026-05-19 17:56:58 From Will Bartlett to Everyone: Replying to "\[MS-OAPXBC\]: x-ms-RefreshTokenCredential HTTP head...": This is probably the best summary of what Microsoft is trying to do  
  * 2026-05-19 17:58:12 From Will Bartlett to Everyone: Replying to "\[MS-OAPXBC\]: x-ms-RefreshTokenCredential HTTP head...": x-ms-RefreshTokenCredential is for user+device identity, if the user is signed into the OS. x-ms-DeviceCredential is device-only identity,if the uesr is not signed into the OS

## AOB

* Use of .well-known \- [https://github.com/w3ctag/design-reviews/issues/1217\#issuecomment-4485020351](https://github.com/w3ctag/design-reviews/issues/1217#issuecomment-4485020351) 

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Ben Kelly (Meta)  
* Christian Biesinger (Google Chrome)  
* Theo \- @thhck ( Solid CG )   
* Phil Smart (Shibboleth/Jisc)  
* Chris Needham (BBC)  
* Wendy Seltzer (co-chair)  
* Pam Dingle (Microsoft)  
* Will Bartlett (Microsoft)  
* Sam Goto (Google Chrome)  
* Bjorn Hjelm (Yubico)  
* Emelia Smith (funded by Bluesky / Decentralized Social Web)  
* Alex Russell (Microsoft)