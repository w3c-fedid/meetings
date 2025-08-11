# FedID WG Telecon \- DC API Series A, 2025-08-11

* Moderators: Heather Flanagan

* Scribe: Christian

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
    * yay Christian\!  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues (30 minutes)  
  * [Add guidance to verifiers/issuers and clients/client platforms on cross-origin usage \#332](https://github.com/w3c-fedid/digital-credentials/issues/332)  
  * [Top frame origin should be passed to client platforms and credential managers for cross-origin requests \#333](https://github.com/w3c-fedid/digital-credentials/issues/333)  
  * General issue cleanup  
* DC API PR (30 minutes)  
  * [Fix cross-origin usage example text \#335](https://github.com/w3c-fedid/digital-credentials/pull/335)  
  * [Define Coordinator and Client \#306](https://github.com/w3c-fedid/digital-credentials/pull/306)  
* Any Other Business (AOB)  
  * IIW meetings

# Notes

### Ecosystem Updates (10 minutes)

* None

## DC API Issues

### [Add guidance to verifiers/issuers and clients/client platforms on cross-origin usage \#332](https://github.com/w3c-fedid/digital-credentials/issues/332)

Tim: Somewhat controversial (even in WebAuthn) because we do not provide strict requirements. We have to add some clarity / a bit more context

Lee: Native API goes through the wallet and currently only passes the origin and if this requirement was added, then it might become usable

Tim: this is only about native API, that it should show both. 333 is the requirement that the information should be passed downstream

Lee: Asks what is currently shown for WebAuthn, is it origin or RPID?

John: RPID is shown but both is sent

Lee: thinks that we should make a decision on what is shown here

Nick: It sounds like we are saying both of these origins might be relevant and we should give some guidance so the user can make a better decision? What should the user decide based on these origins? Users were previously confused by different origins — main question would be what the expectation is towards a user decision when being shown 2 origins.

Tim: Strong preference, but implementations started implementing it differently

Matthew: Thinking about the shop checkout flow. It could be a Shopify-powered website, but the user sees the storefront's branding. So the request should be coming from the entity triggering the request (in that case, [example.com](http://example.com), not Shopify). 

Lee: When you share data with an iframe, you might be sharing all of that data with the topframe. Some of the information might be end-to-end encrypted. Another thing is that we don’t always use the origin to identify the RP; it might be a certified business name and that party is the one registered and agreeing to data policies, etc. From that perspective, it wouldn’t be [google.com](http://google.com) doing the request, but a company certificate and that it is important to take that into consideration when talking about origin.

Tim: That is a good example of why it should be the business entity interacting and the user has no legal relationship with an intermediary like Shopify, but with the store that might be using such a service. The user’s relationship is with the site, not with a service platform.

John: There are differences between passkeys and verifiable credentials — passkeys are issued and tied to the web origin; thus the web origin is more relevant to that. The important information we want to provide to the user is who is the data processor.

Ryan: The verifier is not necessarily the entity that is processing the data. This is a real-world problem and there is value in communicating exactly who you are passing the data to (e.g., the top-level origin or the merchant for payment).

Matthew: On the web, do we have to assume that both origins have access to the response data? 

John: There is a risk in making assumptions based on the receiving frame. Presenting a verifiable credential is like passing a bunch of attributes and the question is if we inform the user about only the first step or all steps in the release of information. Making an assumption that the containing page gets access to all or any of the information might not be accurate.

Nick: We have a lot of different parties involved. Are we sure we want to involve all of the involved parties? It might be clearer for the user to not disclose all of that information. If we want to include the other parties, then we need to pass on all context. If the user is not getting informed, then we should just say that we cannot get informed consent at this level.

Matthew: It’s hard to imagine how all of that is being conveyed by the browser. It should be the responsibility of the protocol to include such information. Origins seems an easy option to provide some clear information. Protocols should deal with the other involved parties and getting consent.

Christian: You can only get fully informed consent if you have full information. It has to be provided in the wallet; it requires understanding the ecosystem and trust assumptions, and yet those will be different in different contexts 

Tim: User Agent should provide some context to the user and keep it at the level of understanding of origins. 

Heather: We have to separate between the bigger picture and which pieces this API can provide. You will need to have different mitigations at the different layers.

### [Top frame origin should be passed to client platforms and credential managers for cross-origin requests \#333](https://github.com/w3c-fedid/digital-credentials/issues/333)

Was covered mostly in the previous discussion

### General issue cleanup 

Heather: Roughly 90 issues open right now and we should try to understand where the important ones are.

\#35

Matthew: Could something like this be kept around as a discussion? Maybe turn it into a discussion on github? These are issues that will likely not turn into meaningful changes in the  spec.

Heather: If it will not bring any meaningful changes into the specification, why are we investing time into these issues?

Matthew: This topic might be a living discussion that is not treated like a traditional issue that can be used over a longer period of time.

Michael: Fewer places to discuss are better

Wendy: We have to do some gathering of threats like this that were brought up in the formal objection to the re-charter.

Nick: We should address the issue and we could and should make some concrete changes to the spec.

Lee: When it comes to formal objections, we need to have some kind of process on how to deal with them. This discussion seems quite open ended. Make it more concrete into dedicated issues that are actionable.

Tim: There have been some changes to the spec to address this. Not saying we have done everything, but some progress has been made.

Wendy: We can express a preference to commenters to join calls and if we feel we have done our part, we should say so. Otherwise, we should keep these issues open and keep discussing.

Heather: Hopefully we can get this sorted out into a more actionable manner.

\#84

Matthew: There are some assumptions about what the issuer can do — it seems like all of this is outside of the parts that the DC API is involved in. DC API could help initialize the process, but concrete mechanisms like this seem out of scope.

Tim: Tim to create an issue with a more concrete discussion (\#343).

\#44

Nick: Based on feedback of the group, 2 issues were created (\#208/\#209) with more concrete proposals. If we consider and adopt them, this can be closed.

## DC API PRs

### [Fix cross-origin usage example text \#335](https://github.com/w3c-fedid/digital-credentials/pull/335)

Already merged since it was purely editorial. Why was there an Agenda tag on it?

### [Define Coordinator and Client \#306](https://github.com/w3c-fedid/digital-credentials/pull/306)

Tim: There is some disagreement on the terminology and entities that should be defined?

Matthew: It can share a lot of overlap with the user agent model used in WebAuthn. Something of this feels like one level of abstraction too much. Client and coordinator are not commonly used for other web APIs

Tim: There are quite a few things that are different from other specs. It adds browser-specific things out into the open and adds confusion.

Heather: No consensus on this one today and asks for comments in that PR.

## Any Other Business (AOB)

* 


# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Lee Campbell (Google)  
* Christian Bormann (SPRIND)  
* Nick Doty (CDT)  
* Matthew Miller (Cisco)  
* Simone Onofri (W3C)  
* Bjorn Hjelm (Yubico)  
* Ryan Watkins (Mastercard)  
* Helen Qin (Google Android)  
* Mike Jones (Self-Issued Consulting)  
* Ketan Mehta (NIST)  
* René Léveillé (1Password)  
* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Nick Steele (1Password)  
* 