# FedID WG Agenda \- DC API Series B \- 5 August 2026

* Moderators: Wendy

* Scribe: 

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

## Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (10 minutes)  
* Poll results (10 minutes): [email summary](https://lists.w3.org/Archives/Public/public-fedid-wg/2026Jul/0012.html) [WBS](https://www.w3.org/wbs/154550/fediddcapienc/results/)  
* DC API Issues & PRs (35 minutes)  
  * [Add requestOrigin attribute to DigitalCredential \#567](https://github.com/w3c-fedid/digital-credentials/pull/567)  
  * [Classify validation failures into specific exception types \#515](https://github.com/w3c-fedid/digital-credentials/pull/515)  
  * [Add document origin to request context \#512](https://github.com/w3c-fedid/digital-credentials/pull/512)  
  * [Require support for both mdoc and signed OpenID4VP protocols \#454](https://github.com/w3c-fedid/digital-credentials/pull/454)  
* Any Other Business (AOB)

## Notes

## Administrivia

Wendy: reminding us of our code of conduct.

## Ecosystem Updates (10 minutes)

Marcos: started implementing OpenID4vp 1.1 in WebKit. And will be sending feedback. Don’t think there have been too many browser folks implementing, and encourage others to take a look. The crypto side needs a look.   
    
Matt: Is there a public bugtracker for the WebKit stuff? 

Marcos: It's a few people implementing, so we will try to get everything linked from [https://bugs.webkit.org/show\_bug.cgi?id=317545](https://bugs.webkit.org/show_bug.cgi?id=317545) That’s linked to the larger overall digital credentials bug. Our PR template links to WebKit and Chrome bugs.

## Poll results (10 minutes): [email summary](https://lists.w3.org/Archives/Public/public-fedid-wg/2026Jul/0012.html) [WBS](https://www.w3.org/wbs/154550/fediddcapienc/results/)

Wendy: We tried to reach consensus without voting regarding response encryption. As we couldn't reach consensus, we took it to a vote. 9 participants voted for response encryption, 6 voted to have it SHOULD instead of MUST, 1 voted to leave it unspecified. So the 9 votes were the majority.

Wendy: That gives us a direction forward. We are now working on next steps to implementing that in the spec. What do the editors need from the working group to move forward?  
     
Marcos: We have a PR up that I was crafting with Mohamed. Editors need review and agreement whether that’s the right way to proceed [https://github.com/w3c-fedid/digital-credentials/pull/520](https://github.com/w3c-fedid/digital-credentials/pull/520)

Wendy: Any further discussion there? Hearing none... Moving forward with the agenda.

## DC API Issues & PRs (35 minutes)

### [Add requestOrigin attribute to DigitalCredential \#567](https://github.com/w3c-fedid/digital-credentials/pull/567)

	Marcos: Pending 520, once we have response encryption, the last piece of information the RP might want to know is what origin was used for the crypto. It’s a bit useless, because they already know it if they made the request, but it’s included for completeness.   
Matt: Pretty major difference, because no integrity on this value. What’s the anticipated use case? How would a verifier use it?   
Marcos: It’s not forgeable, because a read-only attribute on a returned object. It’s hard for an attacker to change.  
Matt: But not impossible.  
Marcos: Fairly unforgeable.  
Matt: Certain scenarios the API has to account for, including malicious user agent. If we don’t trust the user agent, what is the utility of a UA supplied value that cannot be verified?   
Marcos: The origin that’s used for crypto validation is provided by the UA, so I don’t agree. Otherwise we’d require all requests to be signed.  
Matt: Response encryption requires request signing. Weird trust model, seems like a self-inflicted wound to say we don’t trust the UA. This seems out of alignment with the poll. Question whether we should proceed with it.  
Marcos: I think all requests should be signed. We could tighten that up  
Matt: [Issue\#568](https://github.com/w3c-fedid/digital-credentials/issues/568), created a week ago. If you are going to require response encryption, you need to protect the secrets conveyed, so you need request signing, too. Not my argument, but one being made by others in the WG. Seems to be snowballing.   
Marcos: Snowballing is common in development  
John: I agree with Matt. This field doesn’t belong in the API because it’s not signed over. I think there’s a case for unsigned requests in the API. We have that in WebAuthn, e.g., over an authenticated channel. It’s possible to have a credential that’s bound to an origin and you need just to establish a secure channel to the origin. I like the idea of having signed requests and encrypted responses, that’s the easiest combo to make a security argument for. But then we’re not providing much value add from the DC API.  
Matt: The spec in WebAuthn generally trusts that the user agent is fine. If I had to give an alternative to [\#567](https://github.com/w3c-fedid/digital-credentials/pull/567), I’d redirect to say whether request signing is mandatory.  
John: Request signing is a core decision.   
Matt: Expect the A call to have some input.  
Marcos: EUDI and I believe Openid's HAIP profile mandates request signing.  
John: think about where in the layering this is mandated: protocol or DC API? In other calls, there has been talk of responses that go to multiple parties, and have to be encrypted to multiple parties. Consider the metadata.  
Matt: OID4VC multisigned is one consideration for that use case. It’s a real shame we don’t have client-data JSON. Arguments about the cost of encryption operations. I might make an issue about that. Whether DC API needs request signing and response encryption, beyond what the protocol captures.  
Marcos: Look at issue 333 maybe, an issue Tim filed.  
John: I’m more concerned that we’re going to get into arguments about whether or not protocols are meeting those encryption requirements, and another lack of consensus. 

### 

### [Require support for both mdoc and signed OpenID4VP protocols \#454](https://github.com/w3c-fedid/digital-credentials/pull/454)

Marcos: If we mandate, what does that mean? What should we require? What should browser engines implement? Consider also what’s being asked by regulators.  
John: What does it mean to require support for the protocols? My actual implementation strategy is to hand things off to the CTAP platform, hybrid protocol. I have no idea what the platform is going to support, but my obligation as the browser is to hand it off?   
Matt: A group of folks in the WG have been arguing for that without opinionated action from the browser.  
John: I’m worried that something could be added to the spec that requires me to parse mdoc or OpenID before handing it off to the platform.  
Marcos: [\#520](https://github.com/w3c-fedid/digital-credentials/pull/520) has minimal checks, e.g., that response encryption is set from the OpenID side. My understanding is that Chrome has implemented CTAP support. On Apple’s platforms, we hand everything over to the identity document services framework.  
Marcos: Please take a look at the mandated specs, and send feedback.

### [Classify validation failures into specific exception types \#515](https://github.com/w3c-fedid/digital-credentials/pull/515)

Marcos: When we hand things to the platform from the browser, sometimes the platform gives an error. This helps improve interop by classifying exceptions into types. Simple classification scheme to work across browsers. What happens if in the future we realize that a signature scheme is broken, what should the UA do? Compare the case of a self-signed certificate, where we warn about the potentially unsafe action.  
John: Probably want to fold that into the not allowed case to avoid leaking information about the user’s software version, etc. I’d follow WebAuthn in that, not providing lots of granularity in the error.   
Marcos: I disagree with folks who say the browser shouldn't be involved in that decision at all. As UA, if we find a dodgy certificate, we should tell the user about that.   
John: My feeling is that the browser might not be the place to do those checks. When an encryption scheme is broken, you treat it as no longer encrypted, and can forbid it at the browser level. It’s not as easy as it sounds to “mandate encryption”.  
Marcos: You’re right, I was conflating platform and browser activities. Close coordination where that check happens, but I think it’s fair to say that happens in the platform. From the Chrome side, any time you make any request, it sends a popup, "are you cool with sharing information?", before initiating CTAP.  
Marcos: Please review

### [Add document origin to request context \#512](https://github.com/w3c-fedid/digital-credentials/pull/512)

Marcos: This one ties everything together. If you’re making a request from an iframe that is not same-origin or same-site, you should display something to the user, that another site is requesting your credentials. WebKit side, we thought we should surface that; this spec fix enables the information to show that interstitial  
John: Makes sense for a prompt being shown by the browser. I’ll take a look.

### 

## Any Other Business (AOB)

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Matthew Miller (Cisco)   
* Marcos Caceres  
* John Schanck (Mozilla)  
* Sami Tikkala (Visa)