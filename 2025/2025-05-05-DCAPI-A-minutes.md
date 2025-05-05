# FedID WG Telecon \- DC API Series A, 2025-05-05

* Moderators: Wendy Seltzer

* Scribe: Rick Byers

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API  
  * [Switch goto@google.com for mamir@google.com to edit Digital Credentials \#234](https://github.com/w3c-fedid/digital-credentials/pull/234)  
  * [Horizontal Review Preparation: DC API \#227](https://github.com/w3c-fedid/digital-credentials/issues/227)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (10 minutes)

* Wendy: Any updates anyone wants to share?  
* Rick:  
  * Google announced cross-device version of DC API in origin trial in a [https://developer.chrome.com/blog/digital-credentials-cross-device-ot?hl=en](https://developer.chrome.com/blog/digital-credentials-cross-device-ot?hl=en)   
  * Google Wallet discussed/announced using ZKP for age proof attestation. [https://blog.google/products/google-pay/google-wallet-age-identity-verifications/](https://blog.google/products/google-pay/google-wallet-age-identity-verifications/)   
  * Android announced DC API [https://android-developers.googleblog.com/2025/04/announcing-android-support-of-digital-credentials.html](https://android-developers.googleblog.com/2025/04/announcing-android-support-of-digital-credentials.html)    
* Nick: Is there anything I can do to test, not in the UK?  
* Rick: not that I know of yet  
* Matt: It seems still behind a flag in Desktop chrome. When should those be available without a flag?  
  * Mohamed: Should be working today in OT on desktop. Planning to fully launch in Chrome 140 without needing an origin trial.   
  * Matt: only tried one origin trial before. If a website doesn't have the header, will the call fail?  
  * Mohamed: yes  
* Mohamed: another update: some minor breaking changes in Chrome 136, will be communicated to OT participants. [https://docs.google.com/document/d/11rz\_5i4psO8lqm506d-xizViBg4hRZgFyf9uA1QffSg/edit?tab=t.0\#heading=h.tbjqoo7h2gio](https://docs.google.com/document/d/11rz_5i4psO8lqm506d-xizViBg4hRZgFyf9uA1QffSg/edit?tab=t.0#heading=h.tbjqoo7h2gio)    
  * Also working with Tim to get the content on digitalcredentials.dev  
* Christian: Today was a hybrid event from OIDF interop tests. 10 implementers (Wallets, verifiers, issues) tried, including DC API. Very nice demo of things all working together.   
  * [https://openid.net/oidf-hosts-unique-global-demo-of-digital-id-interoperability/](https://openid.net/oidf-hosts-unique-global-demo-of-digital-id-interoperability/)   
  * Matt: Are there DC API interop tests in OIDF's test suite?  
  * Christian: Two different things. Conformance tests, going to support DC API but don't think they do yet. The event was purely DC API, all implementations using DC API.

### DC API

* #### Editorship

  * [https://github.com/w3c-fedid/digital-credentials/pull/234](https://github.com/w3c-fedid/digital-credentials/pull/234)	  
  * Wendy: Thank you Sam for your work, proposing Mohamed pick up editorship. Thank you.  
  * Sam: Something very natural, take this as investment from Chrome team. Mohamed has been writing all the code in chromium for a year now, we're excited to have him also edit the spec and hope it will help the group.   
  * Wendy: Thank you, spec work depends on the involved participation of editors. Appreciate engagement.  
  * Mohamed: I'm new to the space, please bear with me if I make any mistakes. Hope I will learn fast.  
  * Matt: Sam, are you stepping away from all this, or just as an editor?  
  * Sam: I'm still going to be involved. Between Rick, Mohamed, and I, we're going to try to load balance. I'm increasingly excited about this space, you should see me participating where I can. But between the three of us, it's a lot of Chrome investment. But it will help for Mohamed to take editorship, maybe I can contribute in a different way now.  
  * Wendy: If others are inspired and excited about finding more ways to help, your participation in github issues and other ways is always welcome. Good team here.

* #### Horizontal review

  * Wendy: W3C process requires horizontal review for accessibility, architecture, i18n, privacy, security to make sure the specs serve the needs of the web for all. We do an internal self-review first, then ask for review of the materials and to do their own review of the spec.  
  * Wendy: So we need internal volunteers to pick up different reviews and start with self-review. Preparing our material for presentation to accessibility group, TAG, i18n, privacy, and security groups. Call for interest and help in conducting those reviews.   
  * Wendy: Thank you, Matt, for volunteering for the accessibility self-review.   
  * Wendy: Any questions/comments or other volunteers?  
  * Nick: I have thoughts on the privacy side. I asked last Oct that we start writing privacy considerations. It would be surprising if we went for privacy or TAG review without anything more than the placeholders we have today. I suggest we start writing and marking open issues where we don't have mitigations.   
    * [https://github.com/w3c-fedid/digital-credentials/issues/183](https://github.com/w3c-fedid/digital-credentials/issues/183)   
  * The other thing we could do is to adopt a threat model document and put some of the security work ??? and Simone have done and work Rick, Kyle, and I have done, and put it into a threat model document. That might be a longer doc than we're willing to put into a privacy considerations section. Given the concerns that might be worth doing, with a summary in the spec. I'd suggest we adopt that as a deliverable.   
    * [https://github.com/w3c/credential-considerations](https://github.com/w3c/credential-considerations)   
    *   
  * Simone: I agree we have a big threat model that we should probably mix with credential-considerations, and of course summarize threats and mitigations in the spec. Or if threats are not mitigated, we should document with group decisions. I can help with writing the section.   
  * Wendy: Credential-considerations doc being discussed in the privacy working group?  
    * Nick: We have discussed it there, but if this group is willing to work on it, we can occasionally involve the privacy group — not that many people there are following it.  
  * Wendy: Good to get these sections flushed out beyond headers, especially if we can anticipate concerns. The more information we can present to reviewers, the easier we can make their job of reviewing.   
    * If you want to volunteer, you can propose some text in PR.  
  * Matt: Based on recent experiences in WebAuthn, they're going to be looking for a static link to a fixed version as well as a deadline. I wonder what our static link is and what our deadline is?  
    * Wendy: We will be requesting the FPWD publication shortly. That will become a static link that always refers to the FPWD. Anticipating that this month.   
    * Wendy: We don't have a deadline for next draft publication. But aiming for an early review to make sure our spec is developing in the right direction.   
    * Simone: In general, we need a static URL, and sometimes an explainer. We can decide on the time needed to write. Privacy and security will be complex; we can estimate time. For security, we will work on a threat model, something we already have.   
    * Rick: Re timeline, chrome wants to hit chrome 140, branching in early August, intent-to-ship starting early July. Needs a TAG filing from chrome process. If we can do that through the group, before intent to ship, e.g., by start of June, that would be ideal. I think it’s better if the WG files for TAG review, if the timeline works.  
    * Wendy: When we have a shape we think meaningfully reflects the documents we'd like to get reviewed, that's a good time for the group to request architecture review. If TAG comes back and says it's terrible, better for us to learn that early. Sounds plausible to make that request with FPWD being the thing we want reviewed.  
    * Nick: Good to get early review. Having no text would make that not a pleasant review. Not optimistic about hitting that timeline or being reasonable to ship that to all customers when we don't have any mitigations. If we want to stick to that deadline then I think we are behind and should be working as quickly as possible.  
  * Wendy: Who can volunteer to do work proposing PRs?  
  * Simone: I can start working, used a diagram from Tim in breakout session at IIW. We can have some breakout sessions.   
  * Wendy: Thank you. I know lots of work and thinking have gone into security and privacy, let's get that reflected in our documents. Let's show reviewers that we have thought about it.  
  * Matt: On the topic of sections of the spec that have a TODO. Accessibility considerations is one of those. Would accessibility review expect us to try to take a stab at that initially? Or can content reflect what we get from the review? I could probably take a stab at it, just don't know which comes first — content or review.   
  * Wendy: Going through the self-review checklist and drafting answers might identify some things we know of or might show this spec doesn't implicate things reviewers are concerned with. Fine to be going at this early stage with a self-review and asking if we're missing something. In some groups, they put the responses to the self-review as an appendix in the spec.  
  * Wendy: Also important are i18n considerations. If there are labels, consideration of text direction and rendering in various locales, responsive to global needs. Catching that early. Anyone intrigued by helping to lead i18n considerations? Similarly will be looking for folks to pick up security, privacy, drafting a request for TAG review.   
  * Christian: Wondering how much of that is in scope of DC API and how much is in underlying protocols? Doesn't seem fully clear to me.  
  * Simone: Normally security, privacy, accessibility on API level. But for this specific API, we need to analyze at the protocol and ecosystem level as specified in the charter.   
  * Wendy: At a technical level we're responsible for what's described in the spec. So if the spec makes it impossible to meet these things, that's a failure we need to correct. If the spec enables other layers to meet the needs, then we might have non-normative guidance encouraging implementors to meet those needs. Formal requirement is ensuring the spec enables meeting the requirements and spec is taking affirmative steps. TAG may help us think about the layering and modular aspects of the spec in the ecosystem. 

### Any Other Business (AOB)

* Wendy: Next slot is B series, next week; next A series is in two weeks.  
* Please tag issues for agenda, working async for issues and PRs.   
* Just before this meeting began I got a note from the W3C planning team — time for chairs to start thinking about TPAC in Kobe Japan.   
* Currently trying to schedule a WG hybrid meeting with IETF meeting in Madrid (21-25 July), if anyone has office space in Madrid it would be helpful. Rules differ between IETF and W3C so we can't just borrow an assigned room from the IETF venue.   
* Also expecting a hybrid meeting for Kobe meeting at W3C TPAC  (10-14 Nov)

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* Rick Byers (Google chrome)  
* Nick Doty (CDT)  
* Mohamed Amir Yosef (Google Chrome)  
* Christian Bormann (SPRIND)  
* Simone Onofri (W3C)  
* Matthew Miller (Cisco)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Sam Goto