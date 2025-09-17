# FedID WG Telecon — DC API Series B, 2025-09-17

* Moderators: Heather Flanagan

* Scribe: Matt Miller

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (5 minutes)  
* DC API PRs (10+ minutes)  
  * [Redo security considerations \#360](https://github.com/w3c-fedid/digital-credentials/issues/360)  
  * [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)  
  * [Editorial: Add feature and protocol detection examples \#371](https://github.com/w3c-fedid/digital-credentials/pull/371)  
* Any Other Business (AOB)


# Notes

## Administrivia

## Ecosystem Updates

* Tim: digitalcredentials.dev ecosystem table is up-to-date  
  * [https://digitalcredentials.dev/ecosystem-support](https://digitalcredentials.dev/ecosystem-support)

## 

## DC API PRs and Issues

### [Redo security considerations \#360](https://github.com/w3c-fedid/digital-credentials/issues/360)

* Nick: Marcos, Mike, and others noted that we haven’t written this section. Is it solely on Simone to draft? Is anyone else helping?  
* Wendy: Simone was getting some help from the Security Interest Group. It’s our responsibility to make sure the internal review is happening. We’re looking to Simone to help coordinate that interaction.  
* Nick: It took a lot of effort to draft privacy considerations, maybe we need a similar push for security considerations, like identifying/opening issues on github to track the possibilities, as well to help whomever drafts to track the work.

### [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)

* Heather: We’re still waffling back and forth on this. We need to talk with more people about this and see what it is they want to do. Are we going to talk with TAG about this?  
* Wendy: I’ve created an issue in the TAG repo inviting responses to this general question because the questions seemed higher-level than just how they’d work in the context of DC API use. Haven’t yet seen a response from TAG. To the more specific question here, it didn’t look like we’d get a completely blocking registry, i.e., implementers would use the registry to decide whether to allow use of a protocol. Leaning towards the registry being guidance, not a normative blocking decision. This led to the question of, then what’s the value of the registry?  
* Tim: The first response in the TAG thread seems to be approval of the idea.   
  * [https://github.com/w3ctag/design-principles/issues/583](https://github.com/w3ctag/design-principles/issues/583)  
* Heather: Individual responses from TAG members — is there an assumption that the registry would be the be-all end-all decider?  
* Nick:   
* Heather: No TAG position, and no consensus yet in the WG. Any suggestions on how to move forward?  
* Matt: Is this decision blocking anyone right now? Is anyone expecting us to establish this registry?  
* Helen: Two major browsers have shipped DC API support without it so it’s not likely blocking anything. It’s important to understand the security aspects, so we should still work on that.  
* Tim: It’s important for CR as it’s a big architectural decision, but we’re not rushing to CR right now.  
* Heather: I agree it’s not blocking, but I need to take a closer look at what Martin posted this year about protocol registries. I don’t hear a plan to get us any more information to get us to a decision.  
* Nick: Something I want to add is, to Matt’s question about blocking, a large portion of the privacy considerations that Johann wrote are about privacy considerations of the exchange protocol, how we’ll need features in place to achieve privacy in the system. But if we’re going to say that browsers can just implement the features of any protocols, it’s a very different approach. We’ll likely need to rewrite the privacy considerations we have accordingly. We either have the privacy requirements, or everyone has to figure them out independently.  
* Wendy: What could we propose, or resolve, as chairs? We need some more understanding and thinking with the group about how we do our privacy analysis of our piece of the ecosystem. What can we say about privacy review of the API if we don’t have a registry with more info about the protocols being passed through it? As we’re walking towards, “the registry does nothing normative,” I’d like to spend more time talking about what we can say about what else we can do to protect user privacy.  
* Heather: Okay, we’ll keep this on the agenda and see if we can’t come to some consensus. Wendy and I will keep talking to find a proposal to bring to everyone.

### [Editorial: Add feature and protocol detection examples \#371](https://github.com/w3c-fedid/digital-credentials/pull/371)

* Heather: We want to talk about how the PR was changed prior to it being merged. Let’s all have a common agreement about what “editorial” means. In my head, “editorial”   
* Matt: I brought this up so have some strong thoughts about it. expectation is that the author works through suggestions and merges it after the group has had a chance to support after all the feedback. I made some github suggestions with the diff view (\`pull/nnn/files\`), which can be accepted with a click. but then the editor can modify the text, accept the change and merge it as approved, without the suggester or author seeing or approving. Concern is that it could be disingenuous if words are changed without the author of the PR seeing or determining if it’s ready for review or confirmation. I don’t think the editors should be able to make such changes unilaterally.  
* Heather: We’ve heard these concerns before.  
* Tim: In other Working Groups, no actual changes get merged or issues closed without discussion in the WG. We don’t need to block on it, the work should happen async, but decisions made during the calls.  
* Wendy: If anyone has feedback, they’re welcome to share it now or directly to us as chairs. One of the reasons to do things similarly across WGs is so that people can develop a feeling for how things work. It’s not say we should “copy WebAuthn WG,” but more that these are common practices in other WGs. Everyone should be heard and feel as though they’re being heard as changes are discussed.  
* Nick: I’m grateful to the chairs for working through this. I wonder if part of the confusion here is that the WHATWG has a different model. The editor takes peoples’ feedback and makes the changes when they’re non-normative/editorial. Maybe this is where the mismatch is coming from.  
* Matt: Does our WG need to document our expectations? Is this just a misunderstanding? But as a courtesy, the author of the PR should have approval, rather than editors taking over the content.  
* Tim: I have sometimes suggested in WebAuthn that someone take over and open their own PR for a different approach. It’s a reasonable mode of work.  
* Wendy: It bears some more spelling out by the chairs since editors have different responsibilities and work modes across SDOs. It would be beneficial to get us all on the same page here.  
* Heather: Chairs have some work to do on this.  
* Nick: Separate from the question of who has change-control over PRs, I don’t know that we have a good work flow for getting eyes on content prior to merge. Are we going to make a decision on a call? Give authors one week to incorporate changes?  
* Heather: We documented this on the FedCM side of things, modeled on TC39. Work will be staged, here’s what the stages are, how things move through the stages, who writes and who approves what…I don’t remember how much we promoted that with the DC API when it was promoted to this WG. Need to review the FedCM side of the house to see if it’s appropriate here.  
* Tim: I wouldn’t want to bring in the phasing as the API is not complicated enough. But if there’s language around who clicks what button I think that would be good.  
* Matt: Is it possible to lean on GitHub as a collaboration platform to steer interactions in a certain way?  
* Heather: I’d rather establish the norms first than to lean on the platform like that.

## 

## AOB

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan  
* Wendy Seltzer  
* Matthew Miller (Cisco)  
* Nick Doty (CDT)  
* Ketan Mehta (NIST)  
* Tim Cappalli (Okta)  
* David Waite (Ping Identity)  
* Helen Qin (Google Android)  
* Bjorn Hjelm (Yubico)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
*   
  