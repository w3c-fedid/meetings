# FedID WG Agenda — DC API Series B — 16 September 2026

* Moderators: Heather

* Scribe: Matthew Miller

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

## Agenda

* Administrivia  
  * Scribe volunteer(s)? Matthew Miller  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Annex C being optional — \#578](https://github.com/w3c-fedid/digital-credentials/issues/578)  
  * [Add security considerations on forged credential chooser requests — \#506](https://github.com/w3c-fedid/digital-credentials/pull/506)  
  * [Platform-bound wallet attestation for issuance (\#382) — \#586](https://github.com/w3c-fedid/digital-credentials/pull/586)  
  * [EU Commission’s DC API assessment](https://github.com/w3c-fedid/meetings/blob/main/2026/Assessments%20of%20W3C%20TSs%20%20-%20W3C%20Digital%20Credentials.docx)  
* Any Other Business (AOB)

## Notes

## Administrivia

## Ecosystem Updates (10 minutes)

* Heather: Global Digital Collaboration conference breakouts were interesting. Regulators and standards people were all in the same room at the same time, asking how to make the ecosystem work when Verifiers are largely unrepresented. Not the most balanced conversations, but still useful and important. The next round of conversations will happen in Geneva, with some overlap with the Linux Foundation conference later in the week.  
* Heather: Issue is Verifiers need other orgs than governments to be issuers, e.g. colleges, banks, postal services. “Why can’t you use these credentials already issued by the government?” But this could lead to verifiers getting more info than they need\! Issuers need to figure out if they’ll be using VDCs for their accreditations.  
* \[ should verifiers know about or care about the details of the Digital Credentials API? or would they just outsource that to verifier vendors? or does it really matter to at least include all their requirements and different use cases? \]  
* Lee: In most of the conversations we were in, it was almost always with Google with its Verifier hat on. There should have been other large Verifiers there. I’d like to see more Verifiers represented at GDC next year.  
* Heather: “Why didn’t the standards development orgs bring the verifiers with them?” An interesting question that came up at GDC.  
* Tim: These companies want the products/solutions they pay millions of dollars a year for to do all this for them. They hear about the underlying technologies because Gartner crams it down their throats, but they care more about solutions and results than the stack.

## DC API Issues & PRs (45 minutes)

### [Annex C being optional — \#578](https://github.com/w3c-fedid/digital-credentials/issues/578)

* Brian: We should be promoting and referencing freely available standards. In line with the ethos of the W3C. Apple has been pushing very hard to keep the ISO reference in DC API, matching up to their implementation out in the world. I missed a meeting and we changed everything and now there are references directly included in the spec, largely deemed as “consensus.” But when I interact with the groups, there is *not* consensus about including any ISO standard in the spec. I feel like the issue is rehashing something said in a PR that was closed. It seems perfectly reasonable, even given the deployment realities, to keep the reference optional. There was also a formal objection about this that was overruled, with reported reasoning steeped in misinformation. It feels important to me to continue pursuing this.  
* Nick: I was one of the people who suggested making the reference optional. I had concerns about doing privacy and security reviews and continuing spec development whether or not the ISO standard was accessible. I thought the group had made a decision, but the chairs are in a better position to tell. It looks like there’s now a reading-room accessible version, but I don’t know if we can do a privacy and security review on a version like this. What can we do with this released version of the ISO spec?  
* Brian: It was Nick’s comment that I was referring to in another issue. The need to do privacy and security reviews seems to have been abandoned. Those are fair questions.  
* Marcos: We went from not having any protocols required to nailing it down to the two. When we said we were going to narrow it down to mDoc and OID4VP, despite claims to the contrary, it wasn’t just Apple but a range of organizations supporting making the ISO spec freely available. So it’s not just a single vendor, but a range of countries — Apple isn’t even listed as a sponsor. As to being able to comment, discussions are occurring on GitHub. There’s nothing preventing anyone from doing a privacy and security analysis. I know the ISO processes are weird and not open, but it’s not something I’ve participated in. W3C as a community has pushed for openness. That’s why “weird crusade” comes out: we’ve had a generally good relationship with ISO, so I don’t understand why this is an issue. Yes, they have a model that requires funding themselves. I think everyone’s requirements are now met. If not, we can take the requirements back to ISO, but I think we’re in a good place. We have normative requirements where you do need to make the specs because of how we’re going to handle processing the spec. And if you look at the OpenID spec, it has normative requirements on the ISO spec as well. They’ll have to make it a normative requirement over there as well.  
* Brian: The point is we’re under no obligation to make the ISO business model work. You’re right; there are references in the OpenID specs. They’re there to allow the protocol layer to convey mDoc credentials. This obviates the need for Annex C. My requirements are not met at really any level.  
* Simone: If we don’t have any new information, we have the ruling from the council to the group. We have to stick to that.   
* Heather: The decision from the council was whether we reference it. The decision was if it was a normative reference (?)  
* Tim: I do think one thing to correct, is that the ISO discussions and drafts in GitHub are not for feedback. You have to attend ISO meetings in-person to give that feedback. I don’t think the drafts are in a proper state to allow Nick and others to complete security and privacy reviews. I think it’s important to call that out because it’s not correct.  
* Brian: That’s assuming you could even get nominated as an attendee. It’s not a simple process.  
* Ted: Regarding the representation of the council decision as being steeped in misinformation: I don't know whether that  is accurate, but assuming it is, does correcting such misinformation count as *new* information for purposes of reopening the Council's consideration of that Formal Objection? I hope it does, but I am not expecting it to.  
* Simone: Brian, which new information do you have now to bring to a review of the formal objection?  
* Heather: I believe Brian wants to bring corrections to the council of erroneous facts that may have gone into the council decision.  
* Simone: I’m happy to follow up with you, Brian.  
* Heather: Formal objection aside, if you believe that the information is wrong, therefore the decision is wrong, speak to Yves for next steps on the formal process of revisiting the decision. The question for this group is, do we have consensus to normatively refer to Annex C and OID4VP? I believe we have a rough consensus and am happy to go back through the notes with Wendy. I may be wrong, but I believe that’s where we are right now.  
* Brian: The question was whether to make it optional, and in that meeting we had unanimous consent. I don’t know what happened in subsequent meetings, if consensus changed… it’s frustrating to achieve consensus in one direction and then consensus changes and this gets pushed to the side.  
* Heather: Wendy and I will revisit where consensus occurred and how it changed and get back to the group at the next meeting.

### [Add security considerations on forged credential chooser requests — \#506](https://github.com/w3c-fedid/digital-credentials/pull/506)

* Heather: This PR seems largely uncontentious  
* Matt: This seems very implementation-specific. Is this generally applicable to platforms and credential choosers, or is it too specific and foisting architecture onto other implementations?  
* Lee: I agree, this seems very specific. Do we need this at all? There’s always a risk that the browser gets compromised to make calls to the OS. Seems a bit too detailed.  
* Ted: Distinct from that, I have three pending editorial suggestions that I don’t think change the meaning of things, but make several sentences clearer. If anyone has any arguments with them I’m happy to talk about it, but I think those changes should be applied before merging.  
* Marcos: Browser A was secretly contacted and may have had to pay a bounty. Browser A came to Browser B and notified it (WebKit) of the issue. I turned around and added this PR to help Browser C avoid making the same mistake. AI has made attacks that exploit this particular issue much easier. The first line of defense is now specifications because a lot of the code being generated in code is now being written by AI. So AI needs this information to make sure they add these checks when authoring these features. As we go forward in the future and Ladybird or whichever implements this, these specs need this information for AI to read.  
* Lee: I think because the implementation needs these doesn’t mean it needs to be defined in the spec. I don’t think we need to use specs to provide guidance to AI as it implements these specs. It feels like a layer too deep. These specs seem like the wrong level for this level of detail. This feels like browser developer guidance.  
* Ted: This is indeed developer guidance. It may not belong at this part of the spec; it feels like it falls into the security and privacy concerns, or the threat model sections of the spec. Threat model analysis is important and will take years to perform, but I think this is a relevant problem for the specs we’re drafting and thus should be included in there.  
* Simone: The threat is important, and there was a conversation about this at GDC. This should have a place in the threat model section, with a reference to it in the security and privacy section.  
* Lee: Once you go down this path, to provide real implementation-specific guidance, where do you stop? “You should only define browsers in memory safe languages”? “You should only offer digital credential usage in browsers written in memory safe languages”? This addition seems below that line. If this guidance seems genuinely useful we could include it in additional Markdown documents within the repo for agents to consume.  
* Marcos: This is in the security and privacy section. This is not putting that level of restriction or adding such requirements. This is the case of two browser implementations that were affected by the same thing. It seems kinda bad that if we didn’t explicitly tell Firefox about this, but told them to generally be careful, they could still be bitten by the bug. This is part of the line that we depend on, that someone can hack the transient activation check, and it seems a reasonable ask to include this.  
* Ted: This is feeling to me like CORS. An awful lot of implementers of websites usually get this wrong, and something bad happens. How much harm can be done by failing to do this right? The two browser engines that have been fixed to not make this mistake, seems like a rather large impact for other browser implementations that fail to do so. Worthy of a warning in the spec, even if it’s not in a specific section of the spec which feels like another discussion.  
* Heather: The argument seems to be about where to put it. As Tim points out we have developer implementation guidance. Do we capture this? Yes. Do we capture it in the spec? Maybe. Not hearing consensus about where it should land.  
* Marcos: Ted is right, there should be more warning. In WebKit it was fixed throughout because this problem affected several call sites. At the same time this is not observable behavior to regular web developers, it only affects browser engines.  
* Heather: I’m going to take this back to Monday’s call to see if we get any new information, then figure out where to go from there.

### [Platform-bound wallet attestation for issuance (\#382) — \#586](https://github.com/w3c-fedid/digital-credentials/pull/586)

* Nick: I read it but I admit I don’t understand the text. I don’t yet understand how the proposed solution would provide the wallet’s app ID back to the issuer. It’s a privacy issue if it allows the issuer to know the wallet. It’s a more serious issue if it allows the issuer to coerce the user to use a specific wallet.  
* Lee: You’re right, this does reveal the wallet’s name which is a privacy issue. We’ve looked into other solutions which we can get into next time. We could probably build this to not require divulging the package name. You could say “it’s a certified wallet, one of N.” We could probably also solve the problem of every issuer having an allowlist of wallets, which makes it hard for new entrants even if they get certified. I think the last point, whether we can force an issuer to put a credential into *any* wallet, we probably can’t get out of that. The issuers do want to know the properties of the wallet they’re issuing into, like the EU which requires checking. We might be able to build the ecosystem to allow more people to get on the list, like certification.  
* Nick: Certification or “one in a group of N” is better, but not as good as what we should have. My browser, I don’t pre-certify with every website.  
* Tim: If we think about it, it’s still the user’s choice if they save the VDC into an app. If we treat the CM as another user agent, the user ultimately has to trust it just like with the browser. It’s not the most ideal scenario, but the way the ecosystem currently works, this is probably the best path. We had this issue in the early days of WebAuthn, banks would never update their allowlist of CMs. One caveat we should call out is, this is a discussion in FIDO, we may have to take some of that work back here into W3C.  
* Matt: How do we envision issuers keeping track of the lists of which apps/wallets are in the lists? Will there be trust registries, or will different entities have their own lists?  
* Tim: I think Nick dropped, but wanted to mention this would be optional. It might become heavily used, but optional.

### [EU Commission’s DC API assessment](https://github.com/w3c-fedid/meetings/blob/main/2026/Assessments%20of%20W3C%20TSs%20%20-%20W3C%20Digital%20Credentials.docx)

* Heather: I uploaded [a Word document](https://github.com/w3c-fedid/meetings/blob/main/2026/Assessments%20of%20W3C%20TSs%20%20-%20W3C%20Digital%20Credentials.docx). Take a look and we’ll talk about it on the next call.  
* Simone: The Commission expects feedback, but this can include asking questions. I assume 80% of our feedback will be questions.

## Any Other Business (AOB)

# Queue 

* \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Matthew Miller (Cisco)  
* Brian Campbell (weird crusader)  
* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Nick Doty (CDT)  
* Lee Campbell (Google Android)  
* Helen Qin (Google Android)  
* Tim Cappalli (Okta)  
* Marcos Caceres (Apple)  
* Simone Onofri  
* 

