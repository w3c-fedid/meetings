# FedID WG Telecon — DC API Series A, 2026-02-09

* Moderators: Wendy

* Scribe: Heather

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?   
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes)  
* Outstanding Privacy/Security issues (15 minutes)  
  * How to reframe the following in the absence of a registry  
    * [privacy review for registry inclusion \#226](https://github.com/w3c-fedid/digital-credentials/issues/226)  
    * [Protocol registry: Reviewing is not sufficient \#255](https://github.com/w3c-fedid/digital-credentials/issues/255)  
* DC API Issues & PRs (35 minutes)  
  * [What protocols should a user agent implement? \#439](https://github.com/w3c-fedid/digital-credentials/issues/439)  
  * [Add openid4vci-v1 issuance protocol and enumeration \#465](https://github.com/w3c-fedid/digital-credentials/pull/465)  
  * [Define "present credential requests" algorithm. \#419](https://github.com/w3c-fedid/digital-credentials/pull/419)  
* Any Other Business (AOB)

# Notes

Admin: usual reminders

### Ecosystem Updates (5 minutes)

* Mohamed: In the EU, this API will be mandated for all member state wallets. They will mandate both protocols (OpenID4VC and ISO/IEC 18013 Annex C).  
* Wendy: Are there any notes we can point to for people who were not at that meeting?  
* Mohamed: Not aware of any? Is the new ARF public yet? Will try to find a link and post in the group. [https://ec.europa.eu/info/law/better-regulation/have-your-say/initiatives/16112-European-Digital-Identity-Wallet-standards-and-technical-specifications-update-\_en](https://ec.europa.eu/info/law/better-regulation/have-your-say/initiatives/16112-European-Digital-Identity-Wallet-standards-and-technical-specifications-update-_en)

### Outstanding Privacy/Security issues (15 minutes)

How to reframe the following in the absence of a registry

* Wendy: Goal in putting together this agenda was to figure out how to move on things that will block us from getting to CR. We need to address some of the issues that have been with us for a while and that came out in the FO to the charter. How do we work with privacy concerns that have been raised? How do we address these issues before making the doc transition? Our goal is consensus; we won’t always be able to achieve solutions that have unanimity. 

#### [privacy review for registry inclusion \#226](https://github.com/w3c-fedid/digital-credentials/issues/226)

* Wendy: This and the next issue started as registry inclusion issues, requiring privacy review before registry inclusion. Review itself is not sufficient. We’ve kept these open beyond removing the registry to make sure we’re addressing the underlying issues raised here.  
* \<crickets\>  
* Wendy: The chairs will circulate these privacy questions to the list and reach out specifically to the people engaged in that discussion to see when we can pull them up for a broader group discussion. It can’t only be Nick Doty’s responsibility to push these issues. The group needs to resolve these. Maybe Johann can come back with ideas for how to move these forward.   
* Simone: An idea from Martin Thomson was not only to review but to specify requirements. This was an idea we had for the security considerations as well. This could be a starting point to have the discussion, to both review and make visible what’s needed in the protocols. These requirements could be for self-review, so we can identify what we’re looking for.  
* Wendy: The notion of requirements is captured in issue 255\. Johann expressed interest in that. We should follow up to see if work has been or will be done on that.  IF there is nothing else on these issues, we will bring them up again on a future call. 

#### [Protocol registry: Reviewing is not sufficient \#255](https://github.com/w3c-fedid/digital-credentials/issues/255)

* See above

## DC API Issues & PRs

### [What protocols should a user agent implement? \#439](https://github.com/w3c-fedid/digital-credentials/issues/439)

* Wendy: Marcos wanted us to take a look at this one. Does anyone have an update?  
* Mohamed: The main question here was whether we should require that the user agent implement both protocols or at least one. Marcos would like to say at least one is required to be implemented. What would we as a group like in the spec? If we say all of them, it will not map to reality (nor will it change reality).  
* Wendy: Aligning with reality is good, and specs that don’t reflect reality don’t have long useful lives.   
* Brian: What’s the point of saying just implement one, other than reflecting this reality? Might as well not do anything. What value is there to say that in the spec?  
* Lee: We should write in the spec what we think is the right thing for the ecosystem. If you only do one, all cross-device flows break. It’s also a very temporary state of affairs, and it’s a one browser issue. We shouldn’t write a spec based on one browser’s issues. Given the EU regulations, even that one browser is likely to support both. I would write the right thing and write the tests for both. If one browser isn’t compliant for several months, so be it.  
* Brian: Agree with what Lee says there. I think the timeline for when the other browser supports both is probably optimistic (if you say just one year).  
* Mohamed: Firefox is going to use the MacOS-provided APIs, which do not support OpenID4VP cross device. At least, that’s what it looks like. They aren’t going to implement CTAP itself. But that said, I agree with Lee.  
* Lee: Is this an API for cross device?  
* Mohamed: Yes, on MacOS, that API is part of the operating system.   
* Lee: There is no native DC API for MacOS or iOS that takes Annex C nor OpenID requests. So, not sure what Firefox could even call.  
* Mohamed: We can ask.   
* Lee: Right now, it’s a hard-coded mdoc API; it’s not even Annex C.  
* Wendy: Not hearing consensus. We’ll review the associated PR at a future meeting.

### [Add openid4vci-v1 issuance protocol and enumeration \#465](https://github.com/w3c-fedid/digital-credentials/pull/465)

* Mohamed: During the removal of the registry, there was disagreement about referencing OpenID4VCI because there was nothing to specify its behavior in the DC API. Tim wasn’t happy with that. After much consultation, people now seem to be OK with it. We agreed about the identifier. Lee promised to land the spec changes in OpenID4VCI soon.  
* Lee: Will try to do it this week  
* Brian: A reference to an issue in another SDOs issue tracking repo is very odd. Hopefully that’s transient and on a short scale. It’s a bad precedent.  
* Lee: I agree, we shouldn’t reference their issue. We should reference their specification, and I will create the PR to update our spec this week.  
* Mohamed: We can coordinate merging both PRs offline.

### [Define "present credential requests" algorithm. \#419](https://github.com/w3c-fedid/digital-credentials/pull/419)

* Wendy: Marcos wanted this added to the agenda; Mohamed still has questions and comments.  
* Mohamed: One part that’s still open for discussion with Marcos is what kind of error should be returned. Should it be an “unsupported” error like WebAuthn? Marcos wasn’t happy with that; we’re still talking about it. I would like to look into this more deeply. Overall, the PR looks good in terms of direction; encourage others to read and comment.   
* Wendy: Encourage people who might have thoughts on this to review and comment. Helping find precedents and examples of error reports would be great. The spec editors are looking for design patterns; might ask the TAG or ask security reviewers.  
* Mohamed: Exactly. After we reach some consensus, he’ll write a TAG recommendation for these kinds of use cases. Suggest we bring it back to the WG when it’s in better shape.

# AOB

* 

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* George Fletcher (Practical Identity LLC)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Simone Onofri (W3C)  
* Bjorn Hjelm (Yubico)  
* Isaiah Inuwa (Bitwarden)  
* Mohamed Amir Yosef (Google \- Chrome)  
* Helen Qin (Google Android)  
* Brian Campbell  
* David Waite  
* Wendy  
* Lee  
* \+6 ghosts 