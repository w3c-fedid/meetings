# FedID WG Telecon \- DC API Series A, 2025-08-25

* Moderators: Heather Flanagan

* Scribe: 

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)? [Matthew Miller](mailto:mattmil3@cisco.com)  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (40 minutes)  
  * [Editorial: make digital wallets out of scope \#338](https://github.com/w3c-fedid/digital-credentials/pull/338)  
  * [Define Coordinator and Client \#306](https://github.com/w3c-fedid/digital-credentials/pull/306)  
  * [Add request validation \#156](https://github.com/w3c-fedid/digital-credentials/pull/156)  
  * [Proposal to Add Comprehensive Testing Support for the Digital Credentials API \#357](https://github.com/w3c-fedid/digital-credentials/issues/357)  
  * [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (10 minutes)

* Rick  
  * **Chrome DC API Usage Statistics:** [https://chromestatus.com/metrics/feature/timeline/popularity/4826](https://chromestatus.com/metrics/feature/timeline/popularity/4826)  
    * Likely age verification use cases driving production use of DC API in the UK and US  
    * (Note something is wrong with this data at the beginning during experimentation \- Chrome investigating)  
  * **Custom Schemes Usage:** [https://chromestatus.com/metrics/feature/timeline/popularity/4948](https://chromestatus.com/metrics/feature/timeline/popularity/4948)  
* Mohamed  
  * [Plan](https://issues.chromium.org/issues/440387001) is to use interstitials for custom schemes (e.g., “do you trust this device”) starting in Chrome 142

## DC API Issues

### [Editorial: make digital wallets out of scope \#338](https://github.com/w3c-fedid/digital-credentials/pull/338)

* Heather: This PR is probably at a good place, any concerns within the group?  
* Tim: This should be fine to go. When we add terminology like “credential manager,” we’ll update this text to clarify things like “holder.”  
* Heather: I’ll note that in the PR so it can be merged.

### [Define Coordinator and Client \#306](https://github.com/w3c-fedid/digital-credentials/pull/306)

* Heather:   
* Mohamed: Discussed this with Marcos, we agreed to make the line between platform and user agent. An important thing in the spec is to draw the line at the platform, and then it doesn’t matter what we call the browser.  
* Tim: I still think it’s over-defining in the spec, but won’t block.  
* Mohamed:   
* Tim: One request at a time is   
* Mohamed: We won’t mention threads, and assume everyone implements this similarly.  
* Matt: In terms of terminology and using that across multiple specs, drawing the line at platform makes sense. Is there a reason to NOT call the stuff that happens in the actor offering the DC API to not call that a UA the way it is in other specs? As a web developer comes across these specs, could we offer consistent terminology across specs that refer to the browser? Is there a more consistent terminology so we don’t have to introduce something new?  
* Mohamed: We talked about just using User Agent where we can.  
* Matt: As long as the WG has an opportunity to talk about terminology, I’m OK with that.  
* Mohamed: User agent works for this, Client works for CTAP  
* Tim: “Client” is important because it’s very helpful in describing that it’s not a web platform implementation. In WebAuthn, the “WebAuthn client” is the user agent or other implementation. I think this is where we disagree the most. Native APIs are outside the scope of the web platform, but we at least have terminology to describe them.  
* Heather: Any objections to merging these changes?  
* Rick: We should wait and see Marcos’ changes to the PR.

### [Add request validation \#156](https://github.com/w3c-fedid/digital-credentials/pull/156)

* Heather: This one is tough without Marcos because he’s the only one who wants this.  
* Lee: We’ll just end up agreeing with each other.  
* Tim: Yes.  
* Matt: Putting Mohammed on the spot as editor. Are you in agreement?  
* Mohamed: Agree it shouldn’t be in the spec, and Marcos is the one that closed the issue, so I think we’re OK that we’re not including this.  
* Tim: Sorry, didn’t realize this was already closed.

### [Proposal to Add Comprehensive Testing Support for the Digital Credentials API \#357](https://github.com/w3c-fedid/digital-credentials/issues/357)

* Mohamed: Today, we only test unhappy paths. You send a malformed request, you get an error. You call from an iframe, you get an error. But nothing tests the full flow. This issue proposes adding WebDriver support, “virtual wallet,” to simulate platform and wallet. It’ll be a lot of work, but it’ll be aligned with WebAuthn. The second option is “action-based testing protocol.” “Return this in the next request”, “reject the next request”, etc.  
* Matt: Speaking to the virtual authenticator API for testing large scale pilots has been a very successful pattern for WebAuthn. It makes it easier for developers to keep tests up to date. It doesn’t feel like we're testing the virtual driver implementation; it feels like we’re testing WebAuthn. Because of that, I would vote for pursuing web driver support for DC API and a virtual wallet. It seems more complex, because there will be more actors and protocols, which means webdrivers might have to implement all that stuff. Might be too much to support long term. Not familiar with the action-based protocol; will go look at that.   
* Lee: Does the virtual wallet need to support all the protocols and doc formats? Just return an empty value.  
* Mohamed: Would you want to test the case of one wallet supporting one protocol, one wallet supporting another, combinations like that?  
* Lee: The job of the API is to take the request and route it to the platform. The complexity of what happens at that level doesn’t need to be built.  
* Tim: What if we just had static credentials?   
* Matt: Interesting idea, Lee. I originally thought that static credentials would be a nice middleground for downstream, end-to-end testing of a system. If an org wants to build an end-to-end test and they wanted to use the virtual driver, if we didn’t build out full support, could this web driver support be built out so that a verifier could specify what return values are?  
* Mohamed: I like the direction of Tim’s and Lee’s responsibilities. The verifiers probably only care that they get some response.  
* Rick: In general we shouldn’t have things in web platform tests that aren’t in the spec. The complexity that this introduces, WebAuthn is at a higher level of abstraction. My intuition is that we'll run into the problem of WebDriver BiDi. The implementation will have to wait for a request and then respond. Years ago we added BiDi support — Chrome and Firefox support it, Safari not yet — but the big question is, can we build such a test suite without BiDi support? Do we need a way for the test to request a specific response?  
* Mohamed: We can also have it such that, “respond with this for a request in the next two seconds.”  
* Lee (from chat): I think if you truly want to test that your OpenId4VP requests are correct and you are parsing responses correctly, maybe webdriver isn't the right place? because  it's extremely complex :) maybe that's better tested using one of our test wallets  
* John: Having some dummy response to make sure the format gets passed back is useful. It doesn’t need to be full-fledged, but making sure that the message can flow back appropriately. One of the differences between WebAuthn and DC API is, in the DC API, more things are happening in the client. We’d need to instrument more of that middle layer in the browser, but I think it’s the right direction. Whoever is running the test needs to be able to direct the request to the simulated wallet. If the WebDriver replaces all of the credential selection functionality, we might not actually accomplish anything?  
* Rick: One thing we need to think about is how developers are calling DC API. If you imagine a website trying to test their behavior, a “testing wallet” might be something we could offer.  
* Matt: Rick, your comment made me think that if web driver support becomes difficult with all the coordination that needs to happen for a DC API call, would having a library kind of approach be useful? Similar to how we have 1password as a software authenticator. We could take that model and create a library that offers a virtual authenticator and wallet, and someone could wire that into their end-to-end test. Is that approach better longer term? Not entirely sure what it would look like, but maybe it’s something to explore.   
* Lee: Maybe we focus on “spec conformance” here in the spec, and then some other solution could offer verifiers the ability to test flows.  
* Rick: People complained for a long time that testing hooks were missing in the web platform, using the same capability to help achieve conformance and E2E testing. The part we build for ourselves ends up becoming a powerful tool for developers. The latter is almost certainly a WebDriver capability so why not build one good one across browsers?  
* Lee: What if we use the building blocks to solve the bigger problem? Can we decouple things enough so that we don’t block the spec on needing to, e.g., test the entire OID4VP flow?  
* Rick: Can we develop a pluggable API for a wallet to plug into to handle the protocol-specific behavior?

### [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)

* Heather: We keep coming back to this, people have strong feelings for or against. This also came up at the GDC convention.  
* Tim: This is well-written. Other issues highlight that if browsers allow non-registry protocols, then what’s the point of the registry? The spec is back to offering guidance on how protocols should behave, but no hard rules because no registry.  
* Matt: I have yet to read this, but the way it's structured and based on Tim’s comments, it’s top of my list. If we decide not to pursue a registry, how can we include this material in the spec to help explain why not for future?  
* Rick: We have the registry to answer the question, “how will we protect user privacy and security through this API?” W3C principles include trying to defend users from abuse. The registry is the only thing we have right now to try and address abuse. If we don’t pursue the registry, we should capture why we’re not pursuing W3C principals.  
* Wendy: I’d suggest we ask TAG for their feedback. For the specific applicability of these arguments to DC API, there might be more for us to discuss here. The TAG is probably the best place to document the questions of abstract principles.  
* Christian: We should have some kind of rationale no matter what we decide. We’ve been circling around this topic for a long time: “Who are the players in this space, and what are they doing? How are they protecting the user?”  
* Simone: I agree that we need to protect the user. One approach proposed by Martin Thompson in TAG was to not use a registry but implementation requirements. If we manage the registry but the WG closes, for example, who will maintain the registry in the long term? Adding some requirements is useful.  
* Mohamed: No browsers are planning to block protocols, but could show a warning for protocols that aren’t in the registry.  
* Matt: If we considered the implementation requirements path, how would this spec offer to enforce the requirements? Where would that happen? In other specs, it’s hard to say an authenticator will behave a certain way, because it’s not part of the web platform. Other orgs would have to manage that.   
* Tim: At the end of the day, protocol and format can convey the same information. If you go down this path, this is about divulging government-issued identifying information. I don’t think we can dissuade abuse by protocol identifier alone. Maybe a “credential profile” is the way to consider instead.   
* Nick: The enforcement mechanism should be that the browser is far more cautious if it receives a request that’s suspect. If we have requirements and a registry of things we’ve evaluated against those requirements….  
* Simone: Following up to Matt, we should be protecting users. The implementation requirements pattern was followed by the Encrypted Media Extensions (EME) and might be a pattern we could follow too. If we want to have a registry we should also have requirements to speed up review.  
* Heather: I’m hearing we think we might want a registry, and the things in the registry offer some degree of assurance, but it wouldn’t be a blocker to use other protocols.  
* John: If mdoc lets you do bad things, and mdoc is in the registry, that won’t prevent people from doing those bad things with mdoc. It would be a misdirection to the user.  
* Matt: The idea of “haip” comes to mind; an opinionated way to use the protocol. Could we benefit from that here? Being in the registry doesn’t prevent you from doing bad things, so do we need to pair that with opinionated guidance on how to use things in the registry?  
* Heather: I think a secondary protocol would be a separate spec. Separately, if you have requirements what does a registry offer you?   
* Nick: The value of a registry with requirements is that someone has evaluated something against those requirements. The group evaluates, then records the decision in the registry.  
* Christian: Wouldn’t you have to evaluate on a use case basis? Otherwise you cannot really evaluate privacy.  
* Nick: It wouldn’t address all the other parts of privacy. We have many other privacy aspects documented, but we could evaluate the exchange protocol aspects.  
* Rick: We can answer the question, e.g., “has OID4VP evaluated the protocol for user privacy?”  
* John: The registry at any layer can say, “yes, this could be privacy-preserving if all of the layers do their thing.” Nothing stops a malicious issuer from doing bad things if they have the ability to collude with other layers. Just looking at the protocol doesn’t tell you the wallet is not a bad actor. The registry is useful for saying yes, we’re not allowing things that aren’t privacy-preserving, but it shouldn’t say that any one implementation is privacy-preserving.

## Any Other Business (AOB)

* Ryan: Is there any effort to provide updated text around the cross device engagement to distinguish Passkey requests from mDL/VDC requests? Right now in the existing implementation, it always asks "create passkey?" and in our UX testing on mDL, people found this confusing.  
  * Ryan: One thing we noticed in our testing is that the UI shows the same text regardless of what you’re requesting, “Do you want to create a passkey?” A lot of users were confused because we have mDLs and passkeys, and they’re only being asked for passkeys. Not a major thing but folks were definitely questioning what was being requested.  
* Tim: Are you talking about the little chip that shows up in the camera?  
* Lee: “It’s fixed.” We just have to update the Camera app; that fix is rolling out now. Long term, we might just remove the chip completely; scanning the QR code will take you directly to the flow. Figuring out that text is tricky anyway — “show your ID” for a boarding pass doesn’t make much sense.

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Mohamed Amir Yosef (Google \- Chrome)  
* Rick Byers (Google \- Chrome)  
* Lee Campbell (Google \- Android)  
* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Matthew Miller (Cisco)  
* René Léveillé (1Password)  
* Tim Cappalli (Okta)  
* Simone Onofri (W3C)  
* Bjorn Hjelm (Yubico)  
* Brian Campbell (Ping Identity)   
* John Bradley   
* Christian Bormann (SPRIND)  
* Marian Harbach (Google \- Chrome)  
* Ryan Galluzzo (NIST)