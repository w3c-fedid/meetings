# FedID WG Telecon — DC API Series A, 2026-06-29

* Moderators: Heather

* Scribe: Matthew Miller

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Proposed path to CR](https://docs.google.com/document/d/1RoII98j7sgrxWdoHQIHBp6mlmvjNLM-HkWG_htQAkLg/edit?usp=sharing)  
  * [https://github.com/w3c-fedid/digital-credentials/pull/546](https://github.com/w3c-fedid/digital-credentials/pull/546)  
  * [https://github.com/w3c-fedid/digital-credentials/issues/382](https://github.com/w3c-fedid/digital-credentials/issues/382)  
  * Issue Triage (starting with issue 263, oldest to newest)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (5 minutes)

* N/A

## DC API Issues & PRs

[Proposed path to CR](https://docs.google.com/document/d/1RoII98j7sgrxWdoHQIHBp6mlmvjNLM-HkWG_htQAkLg/edit?usp=sharing)

* Mohamed: Went through and tried to tag issues “v1,”, “v2,” etc… Also looked at all the horizontal reviews and tried to address the gaps. Used AI. On the first pass, it overlooked a bunch of issues. We can go through this, address the PRs, take it from there.  
* Heather: How did you think the group would respond to this? My thought is to send this out, give people time to highlight what they do or don’t agree with.  
* Mohamed: We didn’t make it that far. If we ask everyone to go through and look at everything, it’s not a productive use of time. Hoping that Tim and Wendy can go through to help figure out what we should talk about as the wider group.  
* Wendy: I think we need to sit down and take a look. I noticed that some are marked as “nearly done,” some as “easy” or “hard”... Presumably, the easy ones can get to PRs soon; is that right?  
* Simone: Yes, the point was to identify what’s missing before going to final review.  
* Wendy: Because all of these are potentially of interest to the rest of the working group, particularly the ones tagged “hard,” if others can flag the ones that are important to them, that’d help not make the editors the ones who have to propose answers to everything. Some are labeled “potentially out of scope,” which sounds like a question for us chairs to look at and decide how to proceed.  
* Tim: Should I read “spec editors agreed” as Marcos and Mohamed agreed, or is my memory bad?  
* Mohamed: I’m sorry if I said otherwise; only Marcos and I were together when we did this.  
* Simone: When trying to sequence things, particularly for the security and privacy side of things, we assumed some of us would have different viewpoints on what the solutions to those are.  
* Tim: Is this now frozen? For example, completely changing how issuance works wasn’t a problem until this document came out. Are we freezing architectural decisions because this document came out?  
* Mohamed: It’s all for discussion.  
* Tim: I mean, when we get consensus on the path to CR, are we freezing things?  
* Mohamed: No, this is more like our issue tracker.  
* Tim: We now have three issue trackers. We should only use one place to track issues. And we need to freeze issues once we believe we have consensus.  
* Wendy: That makes complete sense. These different ways of looking at the issues are trying to help us focus our discussion on what we need to address before we call the API “done.” This is a callout to other participants here to discuss issues and make sure the important issues are discussed. I agree we need a plan to get the issues closed. We’re aiming to get to zero by TPAC, and that time will come sooner than we expect.  
* Simone: It was a Google doc we used to not interfere with official planning. Let’s try to sort things out and get something to work.  
* Tim: I appreciate you doing the work. We should consolidate as soon as possible.   
* Simone: I agree it can be confusing. We wanted to prioritize without interfering with offi….  
* Matt: \+1 to Tim. Can’t we put the prioritization into a canonical place?  
* Simone: Yes, that remains the goal, this third doc was to take advantage of us being in the same place.  
* Nitin: Hi, I’m a PM on the Edge team, first time joining. I’m trying to find the right collection of use cases for which to build solutions. We use GitHub issues to identify those. What’s currently the right way to find them?  
* Heather: Good question. We’re trying to figure out how to pull this document back into the official source of truth, which is GitHub. The project board that Tim referred to is in GitHub. It tries to take the issues and PRs and represent them in a useful manner.  
* Nitin: I see lots of things in TODO, I’m hoping for a way to prioritize within those columns.  
* Heather: Yes, agreed.  
* Heather: Wendy and I will dive into this and identify items that we think don’t have the consensus we need.

[https://github.com/w3c-fedid/digital-credentials/pull/546](https://github.com/w3c-fedid/digital-credentials/pull/546) (related issue: [https://github.com/w3c-fedid/digital-credentials/issues/356](https://github.com/w3c-fedid/digital-credentials/issues/356) )

* Mohamed: CredMan typically returns a credential, but in DC API issuance doesn’t return a credential. The semantics of .create() are different in DC API because no credential is returned. It seemed unusual to use .create(). So we thought to propose a separate method on DigitalCredential. We talked with Nina @ Chrome and she proposed  
* Tim: Who said the semantics are confusing?  
* Mohamed: Any developer who uses CredMan. They expect to get a credential back from .create() but DC API will break this.  
* Tim: Is there concrete feedback from developers? I’ve talked with many and they said it’s not confusing.  
* Mohamed: No, but we suspect there will be confusion.  
* Tim: Developers don’t read CredMan, they read WebAuthn/DC API/etc… This is a last-minute change that has far-reaching implications that’s not justified. This seems to have come out of nowhere.  
* Mohamed:   
* Tim: Developers who are used to WebAuthn will be looking at DC API and will be used to using .create() and .get(). Adding a third method will be very confusing to developers. Just explaining the different pairs of method calls will become confusing.  
* Helen: We’ve already partially shipped something like issuance. We had to add a bit of documentation that .create() doesn’t return a credential, but beyond that there wasn’t much confusion. The way it’s currently proposed is going to change a lot of existing integrations. We need to think through how big a change this will be and ask if it’s worth it to make this change at this time.  
* Matt: I agree that putting issuance as a static credential has weird ergonomics, but surely we can think of a way to document the weirdness, and continue to use .create() and .get() as webauthn works. There are plenty of devs who are used to the patterns of passkeys. Let’s keep the methods that are used the same. Benefit from the advances to credman rather than making issuance unique.   
* Tim: If this was done two years ago, this might be done “for the sake of simplicity.” We also say the protocol decides what to return from an issuance protocol. What if we have a future protocol that *does* return something? And Matt is right that we would lose all the convergence around CredMan thanks to WebAuthn and FedCM. And PXP would need to fundamentally change because it expects to work with data in the shape of the CredMan APIs.  
* Christian: It’s probably too late to make this change. We likely need to add more documentation around issuance. If we explain that the real issuance happens between wallet and issuer, “this is how it is,” that’ll address the confusion.  
* Heather: I encourage you all to leave your comments in the PR. I’m not hearing a lot of consensus to move forward at this time.  
* Tim: The way this issue came out, there’s a PR with web platform changes, so this seems like a done deal. The optics of proposing such PRs is negative; maybe okay for non-trivial changes, but not for something like this.  
* Wendy: It’s helpful that the proposer has come with all of these extra things, but it does not signal consensus in the WG.  
* Matt: Where does feedback ring loudest? PR or issue?  
* Heather: I suggest leaving them in the issue.

[https://github.com/w3c-fedid/digital-credentials/issues/382](https://github.com/w3c-fedid/digital-credentials/issues/382)

* Mohamed: Lee, what was the outcome from FIDO? Do you think it makes sense to add it to the spec now? I don’t want to ship it and we get a breaking change later on.   
* Lee: We could add this in a lightweight way. We call it an “issuance binding token” that gets passed in and then leaves the behavior open. It’s dependent on the issuance protocol and platform to interpret. Call it a “nonce” that can be used by platforms in attestations during issuance. Make it optional. If you go further than that you have to get into details of how platforms handle it. I also feel like if we decide, down the line, if wallets get certification and root down to a given cert, we limit its use to certified wallets, we can add something else later.  
* Mohamed: Great to hear, that we can simply add it.   
* Tim: Counter-proposal is to not do cross-device issuance. I’ve tested the idea out and no one’s brought their pitchforks. This issue is something that will get brought up during review. So perhaps for v1 we don’t define cross-device issuance and look for a solution in v2.  
* Lee: Would this actually help? An attacker could probably find other fairly trivial ways to inject some code into a good wallet to achieve success. Maybe blocking hybrid makes it harder, but not impossibly hard.  
* Tim: If this is a more global problem than DC API, it might be. We have not found a place to have that conversation around protecting navigator.credentials. Maybe we should tackle these conversations together because someone else will come to that realization and wonder how to fix it.  
* Lee: Anyone that can run some JS on a page, all an attacker has to do is call .create() with a replayable nonce. And in fact there’s no origin binding in the .create() call so an attacker could replay a request from their site.  
* Tim: This is probably the strongest proposal to protect navigator.credentials. Put out a recommendation to the CredMan team.  
* Lee: Could we do both? Add the nonce *and* pursue solutions to protect issuance?  
* Tim: I think if we publish something to TAG and get their review… It shouldn’t be an eleventh hour change.  
* Lee: I think it’s going to be a weaker defined feature, unless we define all the attestation formats like in WebAuthn.  
* Tim: Everything we’ve weakly defined over the last three years has led to problems along the way.  
* Lee: It would probably be a year-plus effort to increase integrity in the browser and platforms around these APIs. Establishing PKI as another solution takes time as well. This new value could offer a solution in less time.  
* Tim:   
* Mohamed: What do you mean about protecting navigator.credentials?  
* Tim: We’ve been talking for a while about making navigator.credentials read-only.  
* Mohamed: We couldn’t ship it yet?  
* Tim: No, it’s disruptive so we need consensus. It’s not necessarily in-scope for this group, but nothing is stopping us from writing a note to WebAppSec.   
* Mohamed: So anyone should be able to read navigator.credentials?  
* Tim: Yes, it’s only to prevent injection.  
* Lee: We’d have to protect everything in the ecosystem to prevent replay, which is non-trivial. Freezing this could be an alternative to the nonce idea.  
* Mohamed: You said the EU is asking for this?  
* Lee: Not the EU right now, but there are other nations with this same concern asking for a solution. VCI might need to get updated if we go with this approach to make the request non-injectable.  
* Christian: VCI doesn’t currently have DC API support so it’d have to gain that, which means incorporating whatever we do here into it.  
* Tim: We should have an issue in 1.1 to add “origin” and “expectedOrigin.”  
* Christian: I think the plan was to add this in 1.2.  
* Mohamed: If the value is optional, could DC API ship without this and we add it later?  
* Lee: It’s likely we can do most of this in parallel. My vote is to proceed with this nonce or whatever we call it, and there’s a low chance of it coming back to bite us later. Most other solutions are 12+ month timelines that’d block us going to CR.  
* Mohamed: So we could proceed without any changes for this?  
* Lee: Sure.  
* Tim: We’ve been talking about this for so long it’s time to add this to Security Considerations.  
* Wendy: Good conversation, we have a list of things we can proceed down from this.

### 

### [Issue Triage](https://github.com/w3c-fedid/digital-credentials/issues/) (starting with [issue 263](https://github.com/w3c-fedid/digital-credentials/issues/263), oldest to newest)

* Ted: There’s now a way to show opened, last edited, and closed dates on items on the GitHub project board (only [took 4.5 years](https://github.com/orgs/community/discussions/8518)\!). Sorting PRs or Issues by increasing "Last Edited" date during triage encourages constant churn of the task list to help work through items.

## Any Other Business (AOB)

* Christian: When is the vote for response encryption going to occur?  
* Heather: Wendy and I are working on that right now. It’s coming soon.

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Matthew Miller (Cisco)  
* Mohamed Amir Yosef (Google Chrome)  
* John Schanck (Mozilla)  
* Christian Bormann (SPRIND)  
* Nitin Dwivedi (Microsoft)  
* Isaiah Inuwa (Bitwarden)  
* Simone Onofri (W3C)