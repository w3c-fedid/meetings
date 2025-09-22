# FedID WG Telecon \- DC API Series A, 2025-09-22

* Moderators: Wendy 

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
* DC API Issues & PRs (40 minutes)  
  * [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)  
  * [Redo security considerations \#360](https://github.com/w3c-fedid/digital-credentials/issues/360)  
* Any Other Business (AOB)


# Notes

### Ecosystem Updates (10 minutes)

* Mohamed: Reminder Chrome launching presentation in Chrome 141 — stable this week. We're planning to start a trial of issuance origin in Chrome 142 next month. Blog post coming soon.  
  * Matt: Will the post about Chrome also cover Google wallet, e.g., verifier registration requirements?  
  * Rick: Generally separate, e.g., see [ZKP post](https://blog.google/products/google-pay/google-wallet-age-identity-verifications/) for a wallet-specific post.

## DC API Issues

### [Is a registry needed? \#345](https://github.com/w3c-fedid/digital-credentials/issues/345)

* Wendy: Tim has proposed a [PR](https://github.com/w3c-fedid/digital-credentials/pull/376) to remove the registry [\#376](https://github.com/w3c-fedid/digital-credentials/pull/376). We've asked TAG for their input on the larger issue of registries in general. TAG is [writing](https://github.com/w3ctag/design-principles/issues/583) up a proposal recommending registries.  
* Rick: Sounds like people feel middle ground isn't working. Sounds as though another option to consider is being prescriptive in the spec as to what protocols are supported.  
* Matt: If we do that, we're back to the problem of Chrome supporting everything. What if a new one comes out?  
* Christian: Question of governance, controls DC support. Brings back the whole circle of discussions.   
* Lee: What are we actually trying to solve with the registry? Security and privacy requirements. Registry wouldn't solve these problems really. Still format agnostic, can have mDocs / ST-JWT. Martin's and Nick's concerns are at that level, not even the protocol level. Needs to evolve, e.g., with usage policies. Extremes are no registry (and we just get over it), that's where we are now and what is largely shipping. Another extreme would be W3C fully defining everything — display protocols, formats, what version of the specs — introduce usage policy and make it mandatory, etc. That seems quite unlikely at this time — hard shift. Really only left with what we're doing now.  
* Matt: I find myself leaning towards the "no registry" side of the debate. But I did appreciate Nick's observation on B call last week that we need a place to capture security and privacy considerations. I wonder how we envision that guidance being established and who's going to host it. Where might people learn about this, even enthusiasts who just want to learn more? Do we see [digitalcredentials.dev](https://digitalcredentials.dev) being a good place? We should still have a place insights should go. I guess [digitalcredentials.dev](https://digitalcredentials.dev) seems like it could be a good place if we can get people to think about it.  
* Simone: I'm not caught up on all the minutes from past meetings, but one idea is to have implementation requirements on different levels. We can export this in a W3C note, cross-link on  [digitalcredentials.dev](https://digitalcredentials.dev). And to anticipate my internal discussion on security considerations, we could move the general one into the threat model for the web and just refer to them from the DC spec's security / privacy considerations section.   
* Rick: Nobody is saying spec shouldn’t have security and privacy considerations. Reference other layers of the stack. Non-normative. That should be our primary authoritative source on best practices. Those of us who are implementers should work to align these and our implementations.  
* Matt: With s\&p being privacy-agnostic, when choosing a protocol, consider security and privacy  
* Rick: Yes, and can have protocol-specific examples in our spec.   
* Christian: For the examples, it would be good to point to profiles. For OpenID4VP this would be HAIP (high assurance interoperability protocol).   
* Wendy: I think this is getting to a good understanding. For things that were defined in some respect in terms of the registry, we can talk about how to replace that with sections in our security and privacy considerations. Encourage people to review the issues and Tim's PR and leave comments there to help us get to the end of this one and bring the discussion back between the two calls to get towards consensus. 

### [Redo security considerations \#360](https://github.com/w3c-fedid/digital-credentials/issues/360)

* Wendy: We have lots of TODOs in our current spec. An important piece of getting ourselves ready for wider reviews is getting through these TODOs.  
* Simone: People working on DC API are now coming back to working on these. Feedback from Marcos on GH issues makes sense to move generic threats to the [threat model on the web](https://github.com/w3c/threat-model-web/blob/main/index.md) (from W3C SIG) and just specify things specific on the web API level. List the threats we can take care of and the ones we cannot take care of but are interested in. This is the idea and if someone wants to help the security interest group, we are happy for the help. Worst case we could have a quick meeting at TPAC (over breakfast / lunch or in SIG meeting on Friday). Optimal to have something ready for TPAC and discuss and close there.   
* Wendy: So you propose that working with the SIG, we'll draft some PRs?  
* Simone: Yes, to focus just on the web API level. I will continue working on this one. Moving the generic things to the threat model on the web. At the moment we don't have a place for generic threats; we started asking groups to write them in the spec.  
* Simone: [PR \#277](https://github.com/w3c-fedid/digital-credentials/pull/277). Need input in terms of what is covered by the spec in terms of security mitigations, and which things we think are important but other layers in the ecosystem need to manage the threats.   
* Wendy: So, like privacy, there are things we can address here, and things that are handled elsewhere in the ecosystem. It would be helpful if folks particularly familiar with the API would make sure the threats in the spec are appropriately focused. Do you need some side conversations? Do you have the right people to talk to?  
* Simone: If anyone would like to help, feel free to contact me. We could organize a specific call with the interested people from SIG and FedID groups.   
* Matt: These mitigations, the idea is to flesh them out into actual guidance? Where does the fidelity stop? It could get pretty big.  
* Simone: It's good to specify that this can be a good mitigation for quishing and similar things. Need to think about QR codes.   
* Matt: If someone wants to mitigate a MITM attack with nonce, that might get drafted in terms of code recommendations?  
* Simone: At the requirements level, e.g., "please put a nonce in the protocol to mitigate this class of attack". We have a lot of examples from OpenID4VP covering a lot of our threats; we can list these as examples.   
* Christian: Makes a lot of sense. Usually have a list of threats, and a list of requirements derived from the threats. For us, some can be dealt with by the DC layer, but we can have a separate list of requirements we give to protocols for threats addressed at a different level.   
* Matt: Do we have a deadline that we're working towards?  
* Simone: We can define a tentative timeframe. I'm going to ask other folks who are working on this but weren't available today. But there is still a lot of work done that's not exposed in the PR. We have a good doc we're working on.  We already have a long list of threats, already a lot of the job is done, not starting from scratch.   
* Wendy: Continue to follow the [issue](https://github.com/w3c-fedid/digital-credentials/issues/360) and [PR](https://github.com/w3c-fedid/digital-credentials/pull/277) for updates and will look for agenda+ tags when that's ripe to come back for a group discussion. Also feel free to @ people to request specific reviews and come back to the calls to get help from others with particular spec knowledge. 

## Any Other Business (AOB)

* Wendy: [Call for breakouts at TPAC](http://github.com/w3c/tpac2025-breakouts/issues) is open [https://github.com/w3c/tpac2025-breakouts/issues](http://github.com/w3c/tpac2025-breakouts/issues)  
  * File a GH issue to get a topic into the scheduling queue for a breakout discussion.  
* Simone: Will have a synchronization call with the European Commission. Two main things: if there are some requirements from the ARF that we need to do in the DC API. If you have any questions for the EC let me know. They would like to know if we have an estimate for the timeframe for a recommendation, if we have a guess. We're still waiting for adoption from the group.   
  * Wendy: I would find it difficult to make a time prediction for work on standards.  
  * Rick: Regarding timeframe, OpenID Foundation has hustled to meet timeframes, in the ARF. DC API has been slower, and I worry, feeling real time pressure. If we’re too slow, our API won’t be used as much as other things such as custom schemes. Worry that we’ll never get to consensus.  
  * Christian: The way it works in Europe now is a new law, revision of eIDAS. Commission is forced to write implementation acts which provide the technical details to achieve the commission goals. The commission has time pressure but no idea how long they will take. Will be still ongoing at least next year.   
  * Wendy: For chairs, yes, we hear you and don't want the search for consensus to be an indefinite wait. What we're trying to do is to make progress to fill the gaps for things we know need to be done before there can be a spec and push those forward. We're not at the point where all we lack is consensus right now. And also work to identify the points of disagreements and potential consensus. I don't yet see places where we need to invoke different decision-making methods. Consensus doesn't mean unanimity or blocking forever until everyone is in agreement. It means getting to reasoned decisions where objections have been heard and we can reach a reasoned resolution to those objections. As we get more of our issues closed we should be looking for places where we have our reasoning documented. If there are places where we need to come down to a determination without being able to satisfy everyone then lets find those and get to good decision making. To help that along, if there are time points where we need to be looking ahead to a deadline, those can be helpful in pushing everyone to think about what can we get done in this time, what can we prioritize to get to a spec that will be out and in its most useful place in the world. Our hypothesis from the beginning of this work has been that it's better to have a well-documented spec that's widely used than to leave people scrambling with something that's less well documented and analyzed from a security, privacy, i18n, and architecture perspective. Simone, if you're hearing pressure for when we can get things done, please convey those back to us. I should be more emphatic that it's not just it'll be done when it's done, but we're making progress and a lot of good faith work and good progress in closing issues and bringing things closer together.   
  * Wendy: When is the meeting with the EC, Simone?  
  * Simone: Tomorrow. My impression is that we exclude the discussion on the registry since the PR was just one hour ago. I don't see huge issues to be solved by that.   
  * Wendy: I will see if I can work with Heather to get you a bit of a chairs' summary to share.   
* Matt: Mohammed I wanted to call out [\#238](https://github.com/w3c-fedid/digital-credentials/pull/238) for you to take a look at. There's one unresolved conversation there. Wanted to see if anything else following has resolved this.   
* Matt: Our workflows on github actions might have a weird error with link validation. Can someone take a look? Happened with Tim's and my PRs.  
  * Simone will take a look, usually W3C tooling.

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Rick Byers (Google Chrome)  
* Wendy Seltzer (co-chair)  
* Matthew Miller (Cisco)  
* Simone Onofri (W3C)  
* Christian Bormann (SPRIND)  
* Ashima Arora (Google Chrome)  
* Helen Qin (Google Android)  
* Mohamed Amir Yosef (Google Chrome)  
* Marian Harbach (Google Chrome)  
* Bjorn Hjelm (Yubico)  
* David Waite (Ping Identity)  
* Brian Campbell (Ping Identity)