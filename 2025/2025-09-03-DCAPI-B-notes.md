# FedID WG Telecon — DC API Series B, 2025-09-03

* Moderators: Wendy Seltzer

* Scribe: Rick Byers

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
  * [2025 TPAC](https://www.w3.org/2025/11/TPAC/schedule.html) FedID WG meeting dates:   
    * Thursday, 13 November, @ 09:00-12:30 UTC+9  
    * Friday, 14 November, @ 09:00-12:30 UTC+9  
    * TPAC, proposal for joint session Thursday afternoon with the Web Payments Security IG  
* Ecosystem Updates (5 minutes)  
* DC API PRs (10+ minutes)  
  * [249: Add guidance on how to handle multiple presentation request entries](https://github.com/w3c-fedid/digital-credentials/pull/249)  
  * [238: Add a11y guidance for user agents](https://github.com/w3c-fedid/digital-credentials/pull/238)  
* Any Other Business (AOB)


# Notes

## Administrivia

* TPAC  
  * Wendy: WPSIG joint meeting? [https://www.w3.org/securepay/](https://www.w3.org/securepay/)   
    * Marcos: Would need a better description of what he means of "digital wallets".  
    * Wendy: WPSIG would be interested in an update about the DC API. They are thinking about the FIDO alliance on wallet certification. Should W3C host an IG with participation from OIDF, FIDO, ISO, EMVco, etc?  
    * Wendy: Are there things we'd like to discuss with them?  
    * Bjorn: Dependency in the WPWG on the DC API, would be beneficial to have a joint meeting to have this conversation. I assume they'd bring use cases that may be better answered by this group than by the WPWG alone. Not only whether we are interested, but WPSIG is interested in talking to us about supporting *their* use cases.   
    * Tim: That's a better conversation for OpenID; we're not defining the protocol. All is in a different layer. Regarding creating another group: absolutely not, too many groups already. They should come to where the conversations are. Every year it seems we have a fairly generic meeting with WP which doesn't need to wait for TPAC.  
    * Wendy: Scoping the discussion to where we can be uniquely helpful is important.  
    * Marcos: Giving them an update is always nice. Given that we'll likely have reps from multiple SDOs, it might be worthwhile. Don't imagine we will get much out of it, but I don't dislike the idea of getting together and having a fun social gathering.   
    * Wendy: Yes, something to be said to knowing names and faces to facilitate the conversations Tim says they should be having elsewhere.  
    * Lee: We can give them a quick update. We should ask to give some focus on the topic with some meat. Last two TPACs we've given them an update and nothing at all has changed since the last one in terms of the API. Is there an actual ask? Some feature or regulatory requirement people are looking for that we can have some meaty discussion over?  
    * Bjorn: Expectation is a general update, I don't know what happened before I joined WPWG. Based on my experience, they could use a refresher on where it is and how the ecosystem has evolved. They will bring questions related to use cases discussed in that group. Within W3C, we should have cross-WG conversations on how different specs work together.  
    * Lee: Yes, it would be good to do updates. Would also be good to bring use cases.   
    * Wendy: OK, willingness to have dialog, but interest in getting a more specific agenda. I will work with Ian and co-chairs and work out a more specific agenda.

## Ecosystem Updates

* Chrome (Rick)  
  * [Approval](https://groups.google.com/a/chromium.org/g/blink-dev/c/cPLAQLj8nV0/m/3uhJJthZAgAJ?utm_medium=email&utm_source=footer) to fully ship Digital Credentials API in Chrome 141 (no  longer need an Origin Trial token)  
  * Goes stable Sept 30  
  * Tim: .get or .create too?  
  * Rick: Just .get right now. Issuance not in OT yet but probably will be soon.

## 

## DC API PRs and Issues

* [249: Add guidance on how to handle multiple presentation request entries](https://github.com/w3c-fedid/digital-credentials/pull/249)  
  * Matt: Raised this in an effort to get eyes/approvals and hopefully get merged soon. Ted has suggestions for some revised wording. Trying to define behavior for when semantically identical requests are present in the requests array, UA should only return one response.  
  * Marcos: I need to move in the steps for getting, and I guess there will be steps for creating. There will be a sequence of steps that this will need to move into. Conceptually what you have is good, but won't flow with the steps as written.  
  * Matt: Glad to hear there's motion on that. Does this need to wait?  
  * Marcos: Yes, I will push some stuff up, and will send a branch link to you  
  * Matt: OK so you and I collaborate on this and I'll rework on your branch.  
  * Marcos: OK, pushed up get-steps branch  
  * Rick: Also be aware Mohamed is OOO for a week or so, but would likely be happy to take a look when he's back.  
* [238: Add a11y guidance for user agents](https://github.com/w3c-fedid/digital-credentials/pull/238)  
  * Wendy: Thank you Matt for getting accessibility sections ready for review with horizontal groups. Where do you need help?  
  * Matt: Looking for general feedback on this one. Mohamed had a question about credential choosers. Calls out they're out of scope. Could we just say "user agent" instead of "credential chooser"? Otherwise ready for review. Would like feedback and merge if possible.  
  * Marcos: The way to check these things is whether you get Chrome or Safari to pop up the pre-sheet. We can make comments on the OS. These are "considerations" for wallet implementers to make things accessible. For example, Chrome had the QR code labeled; we fixed that in Safari. The way to verify is to bring up Voice Over and check whether anything is missing. Another example is that the escape key didn't work to cancel the operation. Things like tabbing around the UI should be considered by the platform side and also by wallets. Making sure wallets are accessible, text is not rendered in a weird way. I'll have a read and see if these are covered. These are the main things I've found playing around with different implementations in wallets. Those should be specifically called out.  
  * Matt: What you're saying makes sense and aligns with prior guidance you gave. I've incorporated it so please have a read and let me know if anything is missing.   
  * Wendy: See Tim noting in the chat that the scope of our charter doesn't include QR code. But in the non-normative sense, our document can remind (platform and wallet) developers to consider the overall accessibility of the experience. How can we make sure that what people get to through this API is accessible?   
  * Matt: There's a discussion in WebAuthn where we can't be prescriptive about what the UI is going to be, but we can define desirable experiences and conceptual UX. Not so much "you must", but define desirable end-states that generalize so we're not trying to define specific behavior. I might add this as an agenda item or file an issue; don't need to spend time on it now.  
  * Tim: That makes sense for things in the spec. But it's worse for developers if, e.g., the only place the spec mentions QR codes is here.  
  * Marcos: I did similar accessibility considerations for the badging spec: [badging/pull/117](https://github.com/w3c/badging/pull/117/). Generally this is a thing we compete on as implementers, so other than obvious bad things, we don't want to go too deep into it. Other than accessibility, I don't think there's too much else. If we need to give guidance on what's being done terribly by OS or wallet developers, then we should provide guidance but be careful not to over-step. Keep it constrained to the API.  
  * Matt: Prerequisites for this landing or keep in mind going forward?  
  * Marcos: Just keep in mind as we see them.

## 

## AOB

* Marcos: I was waiting for an OK from the group to merge the limit scope to UA boundary — [PR 344](https://github.com/w3c-fedid/digital-credentials/pull/344)  
  * This is defining the boundaries of what we're specifying here.   
  * Rick: I've seen Marcos’ comments re Mozilla. Not sure that "this is written in browser code" is a meaningful boundary. Isn’t it more about what’s exposed to developers?  
  * Marcos: Not encroaching on stuff the OS gives us, since FF wouldn’t be able to make the OS engineers give them particular APIs.   
  * Rick: FF could choose to store credentials themselves if they wanted, rather than ask the OS for access to its credential store.  
  * Rick: I’m fine with merging it this way, but keep in mind that we might want to make some changes if a third implementation comes up with another direction. Latest comments from MT on [Mozilla standards position](https://github.com/mozilla/standards-positions/issues/1003) are interesting in this regard.  
  * Lee: You can’t assume the browser will be able to hold every credential. Is there a way we can codify in the spec that this API is designed to get to the wallet apps?  
  * Rick: Maybe we should invite Moz to come and share their perspective if they’re going to implement  
  * Lee: It would be challenging if an implementer interpreted entirely differently  
  * Rick: you could imagine a browser saying “we are both a browser and a wallet, giving access only to credentials in our wallet”  
* Marcos: Security considerations section  
  * Lists a whole bunch of stuff but doesn't directly relate back to what's in the spec. I'm wondering if we can redo that section now that we have a better understanding of how the API works. For example Mike West criticized this section as being kind of useless as part of Chrome's process of launching the API. I proposed some ideas of how we can approach the problem. On the WebKit side, for example, we've focused on how we prevent a zero-click attack; how do we prevent a one-click attack (parse data); how do we protect wallets? How do we protect websites? That approach is helpful because it provides some checkpoints in the spec itself and starts putting some of the things we've already baked into the spec into the algorithms as well. Opened [issue \#360.](https://github.com/w3c-fedid/digital-credentials/issues/360)  
  * Wendy: Will add Simone as assignee to look at that, since he's spearheaded security reviews. Good one to add an agenda label to.  
* Tim: Can we keep the "registry or no-registry" on the agenda until we reach a consensus? Can we set TPAC as a loose goal for trying to get consensus on that topic?  
  * Wendy: Yes, good topic.  
  * Tim: Half of the issues go back to the question of registry.   
  * Lee: Should this be a big topic at TPAC?  
  * Tim: TPAC is two months away, I don't want to wait that long. Don't want to start from scratch on this at TPAC with people who don't have the context. Ideally, worst case, we come with a WG position.   
  * Lee: Some of the people who care about the registry argument (Kyle, Martin) might be there but not here. But agreed, it's a long way away.   
  * Wendy: TPAC is also a good place to tee-up feedback from TAG and other cross-cutting groups. \+1 to the more work we can get done before this point, the better.   
  * Lee: How do we resolve this? Dedicate a call to this?  
  * Tim: Why don't Martin and Kyle come to this call? Is it a timezone issue? Maybe we could have a special call and invite them? If they're not implementing, they may not see it as a place they need to be. It is valid for people who aren't participants in the WG to have perspectives on the work the group does, and we need to take that into account. We can specifically invite them to a call that's discussing issues they've raised. Maybe we should put that back on our upcoming agenda and give them a specific invitation.   
  * Lee: Could we at least get the group who does attend to form a consensus we could align on?  
  * Tim: A majority of the issues are requirements on the registry. Whether we say yes or no to the registry we can close or respond to those issues.   
  * Lee: Can we aim for a proposed answer for the "do we need a registry"? If it's yes then the question is what are the requirements.  
  * Tim: You can only object so long if you're not contributing to the conversation.   
  * Wendy: I see you put an agenda+ on the issue ([345: Is a registry required](https://github.com/w3c-fedid/digital-credentials/issues/345)). I asked TAG if they had guidance. Let's bring it back up on our next agenda. It would be good if we can get this group's conclusion on the utility of a registry for the API.   
* Lee: Heads up that on the issuance side, on the create call, we have a problem we call "wallet binding".   
  * There's a man-in-the-middle attack that can happen and fixing it probably needs a DC API change. It impacts all the protocols.  
  * You've logged the user into the website and you're going to click "save driving license to my wallet". You make a create call, and it passes a token which will get exchanged with the credential. Most of the protocols have wallet attestation in them, so it only issues to a wallet the issuer accepts. The problem comes if the user installs a malicious wallet and it gets the token; it can then forward it to an attacker-controlled phone and inject it into the real wallet, and the attacker will get the credential into the legit wallet on the attacker's phone, not the user's phone. Our API doesn't allow the issuer to detect that this has happened. There are solutions to this, but they involve putting something into the request that the platform supports, for binding to the wallet that was picked. But none of it works unless we add a parameter to the create call. I think it's blocking for some real-world deployments.   
  * Tim: You mean like client data?  
  * Lee: Client data solves a bit of it but doesn't solve all of it. WebAuthn is still vulnerable to this. A malicious passkey provider can forward to an attacker's phone, and get back a full security key attestation from the attacker. But if we had client data, it would make it a lot easier, because the platform could put something into it. But we'd still need one extra thing. I will file an issue.  
  * 

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Rick Byers (Google, Chrome)  
* Tim Cappalli (Okta)  
* Matthew Miller (Cisco)  
* Marcos Caceres (Apple)  
* Ketan Mehta (NIST)  
* Bjorn Hjelm  
* Brian Campbell  
* 