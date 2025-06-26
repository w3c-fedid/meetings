# FedID WG Telecon — DC API Series B, 2025-06-25

* Moderators: Heather Flanagan

* Scribe: Matthew Miller


Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
    * [Matthew Miller](mailto:mattmil3@cisco.com)🙏🙏🙏  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Meeting schedule  
    * DC API-related calls on 30 June (Series A) and 14 July (Series A) are cancelled  
    * Full WG meeting proposed during [IETF 123](https://datatracker.ietf.org/meeting/123/agenda) Tuesday, 22 July, 11:30–13:30 CEST  
* Ecosystem Updates (5 minutes)  
* DC API Issues, PRs  
  * [Write privacy considerations \#183](https://github.com/w3c-fedid/digital-credentials/issues/183)  
  * [Add clientAllowsProtocol static method \#221](https://github.com/w3c-fedid/digital-credentials/pull/221) (related issue: [Add isProtocolSupportedByClient static method \#219](https://github.com/w3c-fedid/digital-credentials/issues/219))  
  * [Adds additional terminology \#271](https://github.com/w3c-fedid/digital-credentials/pull/271)  
* Any Other Business (AOB)  
  * FPWD status

# Notes

## Administrivia

* No physical location for IETF meeting. Intent is to use the time to focus on standards development.

## Ecosystem Updates

* Matt: Any further guidance from Apple how to play with this API during developer betas?  
* Marcos: We have an FAQ. I’ll send it and post shortly.  
* Matt: Intention is to enable devs to use beta without Apple Business Connect?   
* Marcos: Yes  
* Lee: OID4VP spec went for final vote. If you can vote on it then please vote  
  * [https://openid.net/notice-of-vote-for-proposed-openid-for-verfiable-presentations-final-specification/](https://openid.net/notice-of-vote-for-proposed-openid-for-verfiable-presentations-final-specification/)  
* Tim: For DC API, you don’t get back a full Annex C response in dev mode?  
* Tobias: Yes, that’s what we’ve observed as well.  
* Christian: Next week is the Global Digital Collaboration conference. Many of us in WG will be in attendance, so it may be a good time to collaborate.  
* Heather: Aiming to have a WG session to ask EU regulators about thoughts on open standards efforts.  
* Christian: I think they will be there, and less that they trust W3C and more that it introduces gatekeepers into the wallet ecosystem.

## DC API PRs and Issues

### [Write privacy considerations \#183](https://github.com/w3c-fedid/digital-credentials/issues/183)

* Johann: Posted an update to the group last week, summarizing “remaining” issues identified during this work. A lot of these are linked from the Security & Privacy Considerations section. It’s difficult to capture everything, but we documented many of them. Some issues are similar with slight variations, which is good; we're trying to identify the core considerations. We’re arguably in a state where we’ve documented the main issues.  
  * [https://lists.w3.org/Archives/Public/public-fedid-wg/2025Jun/0010.html](https://lists.w3.org/Archives/Public/public-fedid-wg/2025Jun/0010.html)   
* Nick: Thanks to Johann for putting a lot of work into this. There’s been a lot of work completed quickly. Agree that some are overlapping, and we’ve begun to consolidate them. Two open PRs, [unnecessary use](https://github.com/w3c-fedid/digital-credentials/pull/262) and [fingerprinting](https://github.com/w3c-fedid/digital-credentials/pull/283), are both useful things to have in the document such that someone who reads them can understand that we’re not finished but can know what the topics are and where we’re going with them. In the rush to meet the timeline from the chairs and group, we’ve not necessarily reached consensus, but we wanted to get something in. There will be follow-up work to achieve consensus.  
  * Unnecessary Use: [https://github.com/w3c-fedid/digital-credentials/pull/262](https://github.com/w3c-fedid/digital-credentials/pull/262)   
  * Fingerprinting: [https://github.com/w3c-fedid/digital-credentials/pull/283](https://github.com/w3c-fedid/digital-credentials/pull/283)   
* Heather: This is fantastic work, thank you  
* Martin: I appreciate the work that’s gone into this, but this is nowhere near implementable. I read through this yesterday and I don’t think this anywhere near ready for implementation.  
* Heather: I was making the assertion that it’s ready for a working draft.  
* Martin: I think there is considerably more work needed.  
* Marcos: I agree. We have two interoperable implementations but still gaps. The bulk of the actual work for the implementations is in the presentation and credential formats themselves. What’s in there is a bit meager at the moment. Some of the work we’ll do in following weeks is to, e.g., define what a client is, work with Chrome to reconcile behavior, figure out what happens when you request one format and get back another, etc. Some of this will have to go into the Credential Manager spec.  
* Wendy: I want to make sure we’re understanding your comment, Martin. We’re trying to get out a FPWD, not an implementer’s draft. Do we have a good sketch that indicates where people are looking for this to go? First set of IP commitments, set a marker for further public development.  
* Martin: I don’t think we’ve reached that bar. Marcos added more detail. But I don’t think there’s been enough information captured. The only thing this captures is that there’s a need for a protocol, some privacy considerations. But to pretend you have a spec is something of a joke. I’m not going to tell you not to put out a FPWD at this point, but you’ve documented a lot of my concern.  
* Johann: I think a lot of this is abstracted away by Credential Manager. There’s a lot of stuff going on behind the scenes in CredMan — “Where’s the stuff? Oh, it’s in CredMan.”  
* Nick: I’m just asking for clarification. I’m not sure what Marcos means when he refers to the design as being open-ended?  
* Tim: Just like in WebAuthn, most of the meat is in the layer, not in the spec. How the web platform talks to the wallet. I disagree with many of the characterizations so far.  
* Marcos: To Martin’s point, if this is for web developers…\<audio issues\>  
* Rick: I get the fact that we would all love to have more detail. Deeply concerned that we continue to promote the terrible. These ecosystems are coming whether we like them or not, but there is no spec for custom schemes or how data flows to/from wallets over them. Do we delay this for five years when Apple and Google have signaled plans to release this capability? This is a significant step in the right direction, but there’s so much “stop” energy. I’m not convinced that Martin wants us to proceed. If this group isn’t interested in moving quickly then maybe we need to find a new place for this work.  
* Philippe: I think it’s important for us to solve this. It’s not a matter of if, but how we can solve this. Yes, we wish we had more time, but unfortunately governments are moving too fast for us to take the time. It’s unfortunate that it’s happening, but it’s happening. We have privacy principles and we do mean those principles, we’re going to have to work hard to make it happen. For Apple and Google to ship that early, they’re doing it whether we like it or not. If they run into issues they can let us know and we can put it into the spec before we even know.  
* Heather: Reminder of our code of conduct. Even in heated discussion, please take a breath and keep in mind that we’re trying to work together.   
* Marcos: We should remember who we’re putting this out for. The motivation can’t be just to appease regulators. We should consider all constituents, not just work to some weird deadline or other regulatory body. It’s rushing when we can do it in a way that’s good for developers, other interested parties. There needs to be a balance here.  
* Wendy: I think Martin left, but acknowledged in the chat that he’s not trying to stop the work. Input is important from those who have concerns. As a chair I’m seeing this phase of discussion reaching a conclusion.  
* Rene: I don’t quite understand the lifecycle of the standards work here. Is the intention to not have breaking changes after publishing a draft? It confuses me why there’s so much resistance to getting FPWD out. In my mind, this should be an accepted risk.  
* Heather (with Philippe nodding): Breaking changes are still possible after FPWD.  
* Philippe (in chat): quotes from the boilerplate *"This is a draft document and may be updated, replaced or obsoleted by other documents at any time. It is inappropriate to cite this document as other than work in progress."*  
* Rick: There will be differences between what is implemented and what’s in the spec. But the intent is to not break what ships. We don’t want to hurt those who chose to take advantage of an API in an immature specification.  
* Marcos: I think WebKit is pretty flexible on changing stuff. It’s an immature spec and everyone knows it, so we’re very flexible on that.  
* Tim: Unless we’re adding a new required top-level member, there’s not a lot that will break at this API level. That’s a good thing.  
* Heather: One of the reasons we put out the call for consensus is to try and make sure there aren’t any urgent blockers when we get further along.  
* Philippe: One thing I want to highlight is that we can highlight specific issues in the status section.  
* Matt: To add one’s voice to the CfC, it’s as easy as reply-all?   
* Heather: Yes

### [Add clientAllowsProtocol static method \#221](https://github.com/w3c-fedid/digital-credentials/pull/221) (related issue: [Add isProtocolSupportedByClient static method \#219](https://github.com/w3c-fedid/digital-credentials/issues/219))

* Tim: We’re blocked on the name again. If we can merge this today, let’s call it whatever. I still think “client” is the right approach, but “user agent” or whatever is fine.  
* Marcos & Mohamed: I don't mind.  
* Matt: This highlighted disagreement on what this thing is, user-agent or client. Let’s hash that out in [271](https://github.com/w3c-fedid/digital-credentials/pull/271).  
* Marcos: Hoping to work on adding that in the next couple of weeks.  
* Tim: These are logical high-level concepts, not intended to be mapped to pieces of WebKit infrastructure. Definitions are talking about roles in the ecosystem.  
* Marcos: Mohamed and I need to work on the connection to implementation.  
* Matt: I’m frustrated by the rush to get this method out and settle on a name. As long as getting the PR in doesn’t lock in the name, I’m ok. If the [271](https://github.com/w3c-fedid/digital-credentials/pull/271) discussion shows us a different name is better, do we change it?   
* Tim: I think we just leave it, because it’s not wrong, just potentially ergonomically awkward.  
* Matt: I just don’t want \`userAgentAllowsProtocol\` and \`clientGetCapabilities\` to mismatch.  
* Heather: I want to suggest we stick with something unless completely new information comes in.  
* Heather: I think we’re good to merge once you make that change.  
* Matt: For devs, good to have it off credential. 

### [Adds additional terminology \#271](https://github.com/w3c-fedid/digital-credentials/pull/271)

* Matt: To clarify, I don’t think this should be a blocker. And then move forward with new methods, not keep talking about the name. I think all the proposed names make sense  
* Tim: These help the consumer of the spec understand their role in the ecosystem. Not intended to refer to implementation innards.  
* Marcos: Suggest we split into separate PRs.  
* Matt: Can we have these discussions now, try to dig into the issues for the next meeting?  
* Heather: If you’re going to split the PR, do so and have the conversation there.  
* Matt: With webdev hat on, having a terminology section that defines the active players is helpful to understanding the document. Devs are a key audience. It should be easy for a dev to go through the doc and understand which actor is performing which part of the dance. Implementations will be there by the time the devs get to this. Be clear what we’re calling actors.  
* Marcos: Agree with developer centric.  
* Wendy: It’s clear we still have some work to do on terminology, and how it fits with implementation.  
* Mohamed: I thought we basically concluded this one. Going back to the last one, what is hybrid? I want to make sure we capture that. I think chat shows different understandings.  
* Tim: We have no way to describe how the client interacts with the protocol, it’s circular.  
* Mohamed: No, this will not return true for hybrid.  
* Tim: What’s returning true? There’s no hybrid capability check.  
* Lee: In the short term, it’s our hope that browsers pass along protocols. On macOS, you should be able to present your Android credential. Even if the local implementation doesn’t support the protocol, the user may have another device that can support it. There should be a different subset of supported protocols over hybrid than locally. It stops presentation over hybrid from devices that can support protocols that aren't supported locally.  
* Marcos: As we discussed in the WWDC talk, we have a different security model. I don’t know how shifting from that model can be done. It’s risky. That doesn’t mean we can’t add it in the future, but it’s how we see the world right now, there’s just too much risk right now.

## AOB

* CfC is still open

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Matthew Miller (Cisco)  
* Nick Doty (CDT)  
* Rick Byers (Google Chrome)  
* Tobias Looker (MATTR)  
* Johann Hofmann (Google Chrome)  
* Simone Onofri (W3C)  
* Martin Thomson (Mozilla)  
* Christian Bormann (SPRIND)  
* Wendy Seltzer  
* David Moore (IBM)  
* Rene Leveille (1Password)  
* Bjorn Hjelm (Yubico)  
* Mohamed Amir Yosef (Google Chrome)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Helen Qin (Google Android)  
* Mike Jones (Self-Issued Consulting)