# FedID WG Telecon — DC API Series B, 2026-07-08

* Moderators: Heather Flanagan

* Scribe: Wendy Seltzer

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
  * [Privacy: Define expectations for Private Browsing (Incognito) Mode\#534](https://github.com/w3c-fedid/digital-credentials/pull/534)  
  * [Security: Prevent opaque origins from interacting with the Digital Credentials API \#535](https://github.com/w3c-fedid/digital-credentials/pull/535)  
  * [Add verifier hardening guidance for script injection\#539](https://github.com/w3c-fedid/digital-credentials/pull/539)  
  * [Add Internationalization Considerations section\#541](https://github.com/w3c-fedid/digital-credentials/pull/541)  
  * [Expand Accessibility Considerations section\#542](https://github.com/w3c-fedid/digital-credentials/pull/542)  
* Any Other Business (AOB)

# Notes 

## Administrivia

* \[administered\]

## Ecosystem Updates

* Marcos: I landed webdriver stuff in WebKit. I’ll see if I can put an article together about how to use virtual wallets. It was fun, quite easy with node. Should be in the next version of Safari tech preview. Because the latest Safari has an MCP thing, you can drive it all with agents. 

## DC API PRs and Issues

### [Privacy: Define expectations for Private Browsing (Incognito) Mode\#534](https://github.com/w3c-fedid/digital-credentials/pull/534)

* Heather: new PR  
* Nick: I think it’s useful to distinguish the don’t persist stuff, and describe the different threat of linking. I’m concerned this PR doesn’t give specific guidance. Sometimes you’re using private browsing for segmentation and you’re going to want to use credentials. And in some jurisdictions, age verification will be mandatory and will require credentials, so in many of the cases where people use private browsing, they’ll want access to credentials.  
* Marcos: I hope the age verification thing isn’t settled with credentials. I’m hopeful that private browsing mode of operation will be the standard mode. I thought we’d always be working in ultimate private mode.   
* Lee: Same. There’s nothing different we do in private browsing or normal. So I was thinking we didn’t need to put anything in the spec. Re age verification, I also think we should avoid DCs, but there might be some places like Europe where you have to do it.   
* Nick: I also don’t recommend it, just worry that it will be used ... For the local attacker, private browsing aims to not keep a record of where you’ve been. Also in some of the digital credentials work, we’ve been thinking that you should have a receipt of where you’ve used each credential. Also concerned about combinations of modes. If you use a credential in one context and then in private browsing, could the site connect them? Should this be handled at the browser or the wallet (the understanding of permission persistence or token reuse)?  
* Rene: For private browsing. Today, RPs don’t get any indication whether the user is in private mode. Just cookies don’t get saved. This is going to complicate the threat model on the wallet side if we try to add a hint or change behavior. If you’re ultimately deciding to sign in, the site can track.  
* Nick: If you present over-18ness, the user doesn't think of that as signing in.   
* Rene: I don’t think we should be exposing private browsing.  
* Lee: We changed it to incognito mode, Give description of what happens to set user expectations. The browser doesn’t save certain things, but that doesn’t mean that your activity is private. DMVs mandate that the wallet keep a transaction log of all the places the credential has been presented. I think in Europe the ARF requires saving a similar log of where credential is presented. We should make clear even in private browsing that the wallet may save this info.   
* Nick: I’d like the TAG to publish its document. There are some cookie-like things here. Recognition across browsing contexts sounds like a nightmare to communicate to users.  
* Heather: With TAG hat on, wondering what TAG finding?  
* Nick: I think there was a draft about defining terms in private browsing, started by Yan.  
* Marcos: I found [https://www.w3.org/2001/tag/doc/private-browsing-modes/](https://www.w3.org/2001/tag/doc/private-browsing-modes/).  
* Heather: What do we do here?  
* Nick: Is there a way to communicate from wallet to browser that this presentation may be linkable, or from browser to wallet that the user does not want this presentation linked?   
* Rene: Does W3C have a definition of what is expected of private browsing?   
* Heather: Nick’s point was that the TAG had started (in the document linked above)  
* Rene: If not, we’re just doing our own things.  
* Nick: I think it would be very useful if we could describe the difference between inherently linkable and not presentations, e.g., full driver’s license, vs over-18. Is the over-18 able to be presented in unlinkable form?   
* Lee: We can’t make a statement of unlinkability. Wallets can use different keys for different origins, then unlinkable across origins; but currently, linkable within the same origin. We could imagine a flag for “please use a different private key”. Fair point about the same-origin linking between different modes.   
* Marcos: If unlinking were possible, I imagine that would be the default mode  
* Lee: If Starbucks made a request for over-18, then currently that would be reused.   
* Heather: I’ll bring this back to the Series A meeting. 

### [Security: Prevent opaque origins from interacting with the Digital Credentials API \#535](https://github.com/w3c-fedid/digital-credentials/pull/535)

* Heather: Mohamed wrote this one, Rick supported. Any other reviews?   
* Marcos: Seems reasonable.  
* Heather: Please add your comments to the PR

### [Add verifier hardening guidance for script injection \#539](https://github.com/w3c-fedid/digital-credentials/pull/539)

* Heather: Marcos wrote, anyone else reviewed?  
* Nick: I don’t see any normative requirements. Opportunity to require CSP for high-risk cases?   
* Matt: Argument about the futility of mandating response encryption feels un-compelling.   
* Marcos: I liked mkwst’s suggestion that at a higher level we enforce CSP check, but we don’t have them. Concern with putting it on RPs is we can’t make websites do things.   
* Nick: Suggest that the API be gated on the presence of CSP, require some site updates.   
* Marcos: Look to WebIDL to enforce? We’d have to see what would break in the ecosystem, given a year of existence.  
* Matt: We can’t require user-agents to enforce a CSP set?   
* Marcos: There are no other APIs that do that.  
* Lee: Most of the data that will be available from this API will be things a user just types into a form today. Don’t assume it’s all highly sensitive.  
* Marcos: Proportionality is important.  
* Nick: I don’t think this is uniquely sensitive. Camera, location, are also sensitive. Improvement needs to start somewhere, and we’re a place we should have the conversation.   
* Marcos: And the bundle, that this represents my driver’s license, is valuable.   
* Lee: If there’s a database breach, and data leaked, does it matter that it’s signed?  
* NIck: But people have the ability to change the information they put in forms, and sometimes the signed data you had to provide on your government-issued ID is uniquely sensitive, with life and death consequences. And certainly we have seen public reactions to data breaches of drivers license images already from multiple vendors, and the public seemed to care about it.

### [Add Internationalization Considerations section \#541](https://github.com/w3c-fedid/digital-credentials/pull/541)

* Marcos: I worked with Mohamed to review the i18n Checklist, ​​[https://github.com/w3c-fedid/digital-credentials/issues/231](https://github.com/w3c-fedid/digital-credentials/issues/231) and then put in this PR.  
* Wendy: Do you think this satisfies the i18n group’s questions?  
* Marcos: Framed as a direct response to the questionnaire. I couldn’t think of anything further.

### [Expand Accessibility Considerations section \#542](https://github.com/w3c-fedid/digital-credentials/pull/542)

* Marcos: I added responses to the questionnaire here too.   
* Heather: Anyone else want to review?   
* Marcos: Once these considerations are merged, we can kick off wide review, so they’re high-priority. 

## AOB

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Wendy Seltzer (co-chair)  
* Matthew Miller (Cisco)

* Nick Doty (CDT)

* Lee Campbell

* Marcos Caceres (Apple)

* Helen Qin

* Rene Leveille

* Bjorn Hjelm

