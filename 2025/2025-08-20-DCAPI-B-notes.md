# FedID WG Telecon — DC API Series B, 2025-08-20

* Moderators: Wendy Seltzer

* Scribe: Heather Flanagan


Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer: Heather  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
  * Note: IIW dates have changed\!  
  * [2025 TPAC](https://www.w3.org/2025/11/TPAC/schedule.html) FedID WG meeting dates:   
    * Thursday, 13 November, @ 09:00-12:30 UTC+9  
    * Friday, 14 November, @ 09:00-12:30 UTC+9  
* Ecosystem Updates (5 minutes)  
* DC API Issues, PRs  
  * [require in-context in-content explanation and an element for user-initiated presentation \#208](https://github.com/w3c-fedid/digital-credentials/issues/208)  
  * [enumerated values for purpose, sharing and retention in API method \#209](https://github.com/w3c-fedid/digital-credentials/issues/209)  
  * [Figure out a system for displaying contributors in the spec \#311](https://github.com/w3c-fedid/digital-credentials/issues/311)  
  * [Editorial: make digital wallets out of scope \#338](https://github.com/w3c-fedid/digital-credentials/pull/338)  
  * [Define Coordinator and Client \#306](https://github.com/w3c-fedid/digital-credentials/pull/306)  
  * [Add request validation \#156](https://github.com/w3c-fedid/digital-credentials/pull/156)  
* Any Other Business (AOB)


# Notes

## Administrivia

* Wendy: Usual administrivia (working group membership, W3C code of conduct). Remember to check your calendar re: changes to IIW. Note we will not have a WG meeting proximate to IIW. TPAC will have two meetings for the FedID WG; expect one will be for FedCM, one for DC API. If participants have schedule constraints that suggest which should go on which day, and any particular agenda items, please let chairs know.

## Ecosystem Updates

* Lee: One extra deployment has happened. If you watch porn in England, there is age verification that uses the DC API with OpenID4VP and Google’s zero-knowledge proofs (ZKPs). Makes for interesting testing. Since it is using ZKPs, it’s interesting from a privacy point of view.   
* Matt: With ZKP for this use case, in Europe, the allow listing model about which verifiers can request info from a PID, with ZKPs involved, is that changing or opening up what verifiers can ask for?   
* Lee: The EU is doing an interim thing that will use the DC API and non-government issued credentials to do age attestations. They are also intending to use ZKP but haven’t decided which one. It hasn’t launched yet; goal is for when the EUDI wallets come out, real EU IDs can be used for this too. Don’t know what policies they’ll use for the allow lists  
* (from chat) Nick Doty: [https://ageverification.dev/](https://ageverification.dev/) — optional zero-knowledge proofs, and no legal limits or restrictions on when the data can be requested or what the verifiers will do with it  
* Brian: Are you in a position to move some of those things into a place that will allow standardization to happen?  
* Lee: Yes.  
* Lee: Helen reminded me that there is now also phone number verification in DC API, coming back as an SD-JWT. This has launched as a beta.

## DC API PRs and Issues

### [require in-context in-content explanation and an element for user-initiated presentation \#208](https://github.com/w3c-fedid/digital-credentials/issues/208)

* Nick: We discussed the broader issue at the last meeting. 208 and 209 are proposals that came up as part of that. This one is about in-context explanation, using the web content itself before anything goes to the wallet for the website to indicate what they intend to do with the data and why. Details include using declarative elements, and having a way for the website to mark up that explanation so the user can initiate a request after that; then the user agent and wallet can consume that data and have a log of what the user requested.   
* Marcos: There has been an ask to do this, and some of it is in permission prompts in iOS. The challenge here is the amount of content, and that it’s web content. When we send the permission request, it goes to the platform API, which doesn’t have the ability to render dumb content, esp. a lot of unbounded content. Need to consider how much text we can actually send. That’s the greater challenge with this. HTML is well-suited to present this content, but whether it’s done as a policy thing, we can’t really enforce. We can recommend best practice. Is what is presented now insufficient? Will it be too much stuff for the user? Will it end up looking like a EULA that people won’t read?   
* Nick: The 209 proposal is more about providing extra detail that could be used in a permission dialog. I’m agnostic as to which is better. As to whether the users are getting enough context now, the answer is no. Have asked several times if anyone has seen a real world demo where the company controls all of this, but there’s nothing suitable out there for in-context explanation.  
* Tim: I understand the problem statement, but I have concerns about a third prompt the user has to get through. It will be just another thing the user won’t read. It also wouldn’t apply to 99% of credentials out there that aren’t government IDs, even same-party issuance and verification. I still think it should be the wallet’s responsibility to manage the consent, not the web layer.   
* Nick: We have experience with other APIs and it’s fairly negative. It is relevant here because of the wallet software, which does not have context about what’s been explained to the user. The opportunity for the web layer is to pass on what has been sent to the user.  
* Tim: The request can contain the information and the wallet based on the verifier information. It’s just a different layer  
* Nick: When we discussed putting it in the request protocol, those groups pushed back and removed the purpose, but it is another valid option.  
* Marcos: Would be good to list the requirements or concerns in the spec and send that to different wallet teams. It might be nice to have that in the spec as a UI consideration. Even if we can’t mandate them, Nick has a good point about calling them out. The UIs will evolve over time. There might not be a technical fix we can mandate, but there is guidance and best practice similar to accessibility suggestions.  
* Nick: We could provide advice to wallet software if this info is being passed on to the wallet?  
* Marcos: Yes. On the Apple platform side, it’s the wallet that’s responsible for the picker. The step before that about choosing which wallet to choose, that’s a point where you could present something, but it will be up to the wallet to indicate the data policies. We could indicate it will be the responsibility of the wallet to provide that info.  
* Nick: As opposed to the web content approach?  
* Marcos: In the web content, you’d still provide context. The website is still getting info back, but the request going to the wallet would be something else. It’s a shared responsibility of both web content and passed-through-to-the-wallet context that we could recommend presenting  
* Matt: Of the two approaches, 209 seems nice just because the website can show anything, and it’s hard to consider requiring anything from people here. Even thinking about the enum approach, we’d have to be careful to indicate that these are hints about the purpose of the request. There’s nothing required of the website to do anything. The possibility of abuse is greater if the impression is given that this would *control* the wallet experience in any way. If we go through the exercise of defining the exact shape of the enums, would we be able to identify the benefit to each party? We should have the conversation.  
* Nick: The in-content approach (208) is specifically a response to the concerns browser vendors have had about presentation in a user agent-provided UI being confusing to the user. But if that’s passed on to the wallet, the wallet will have to decide what to do with it. When we discussed this with OpenID4VP, they suggested a binding. Some content where it’s being presented and a binding where we can have that info logged in the wallet. Having it in web content and passing it on to the wallet would be a way to provide that capability.  
* Brian: In OpenID4VP, it was explicitly agreed to remove “purpose” because we did not want to have an escalation of trust by having the wallet display arbitrary content to the user which could be abused.  
* Lee: Question for Nick — we had a discussion about, if you think about the idea of disincentivizing people from over-asking, what if you had a \`.well-known\` that had all the usage policies for a website. It wouldn’t necessarily get reflected directly in the UI, but it could be auditable. If they then don’t do what they said they would with the data, it would be actionable later. How useful is that model, or do you need it to be on a trusted UX surface?  
* Nick: A large part of the value of having any explanation from the verifier is in the accountability. It’s not some expectation that everyone will be truthful; it’s much easier to hold services accountable to breaking a promise. We can make it easier for the website to do the right thing, if we know what the right thing to do is. That’s why the receipt or log concept that wallets have promoted is about accountability. Having information on record makes a difference, and in some legal regimes, it will make more of a difference if it is presented to the user (e.g., consumer protection regimes) rather than just recorded somewhere.  
* Lee: When we did the OpenID4VP discussion, there was a purpose string. People didn’t like it because it was an arbitrary, unenforceable thing. There was no way to validate it, and yet it would be shown authoritatively via the agent or wallet. Then the argument went to enums and people said those don’t scale. So we dropped the whole thing. But if there was a middle thing where some requests could be signed, you could have the purpose string that the wallet could log and viewable by the user, not in the UI. We could bring purpose back if we got rid of the requirement that it has to be shown by a trusted UI. That would be more accountability than user consent.  
* Matt: The \`.well-known\` idea is interesting. How would that work if \`.well-known\` is decoupled from the site the user is presenting their information on?  
* Lee: Ignore the \`.well-known\`. It would be in the request, so it would be in the transaction log.   
* Nick: That’s the intent of the 208 web content version; you don’t have to show it in a trusted UI. This wouldn’t change the ability of websites to put false content out there.   
* Lee: If OpenID4VP brought back the purpose string and it was not shown in the selector and only used for accountability, would that be useful?  
* Nick: Probably will work less well if it’s never presented to the user because they can have a completely different explanation in the purpose string than what was on the website. It would be better than nothing, but having some concept of what the user saw in the web context would make it easier to provide that accountability, rather than having all the content provided by the wallet.   
* Wendy: Good discussion points; will link the minutes into the issues. 

### [enumerated values for purpose, sharing and retention in API method \#209](https://github.com/w3c-fedid/digital-credentials/issues/209)

* See conversation for 208  
* Nick: There have been some implementations sending certain flags to be displayed by the wallet (e.g., intent to retain), so if there was interest in some enumeration of flags on the wallet side, that could also be presented in the request.   
* Wendy: What more do we need to do to get these issues to a conclusion?   
* Nick: If we're trying to do shared responsibility, I should do more in 208, but if we don’t want trusted UI, I shouldn’t pursue 209?   
* Wendy: I don’t hear anyone objecting to that interpretation.  
* Brian: These all strike me as protocol layer things as well, so I’m not sure this is the right forum to discuss this. Intent to retain, purpose, that’s happening at the protocol of the request (OpenID4VP).  
* Nick: But OpenID4VP has declined?  
* Brian: Yes, but given that, the proposal here has no place.  
* Nick: Happy to discuss further in GitHub. One option is to say it's handled by the protocol layer... and have the protocol not handle it... and so users will just have neither context nor a chance for accountability

### [Figure out a system for displaying contributors in the spec \#311](https://github.com/w3c-fedid/digital-credentials/issues/311)

* Matt: There is a procedural problem this is highlighting.  
* Marcos: Can we do Coordinator and Client first? 306 is blocking a lot of things.   
* Wendy: There is interest in both, so we’ll start in agenda order.  
* Matt: The reason I added this to the agenda is that there seem to be procedural problems to work through as a WG. When I initially created this issue, we discussed whether there is value in having a list of people we valued to be mentioned in the spec. So, I created a PR for that. Did a few rounds on that, then had to put it aside. Since then, there was a perception that the PR was taken over and the content overwritten so the original work was lost. The sentiment presented in the PR was that it was all taking too much time. What is the expectation in this WG, what is the expectation about when this PR can be taken over? When can it be taken away from the original author of the PR? If we’re going to invite people to submit content, it’s unappealing that their work would be erased for whatever reason.   
* Wendy: Sorry that was your experience.  
* Brian: There were several approvals on content that Matt had written; I and other people appreciated having our contributions acknowledged. What was approved was changed and then merged.   
* Marcos: I didn’t see a response to Matt; did reach out to Matt on Signal. As primary editor, I have requirements to maintain this for the next several years. What I proposed (that wasn’t responded to) is what I expect to maintain. Editors have to make hard decisions to maintain consistency. We need solutions that are scalable and maintainable. What Matt proposed was not maintainable, so I proposed a solution based on what we discussed in the PR.   
* Matt: What is currently in the spec, which is the proposed text that was then merged, did not meet the intent of the original issue, because it thanks "everyone in the FedID WG", which encompasses everyone including people focused entirely on FedCM and not the DC API. That there was a proposal of wording that was unilaterally merged is why I think this is a procedural problem.  
* Brian: Many here are just doing our jobs, but it’s customary in every other spec development organization I’ve been involved in, to acknowledge actual contributors to the doc and keep a list of names. That’s not particularly onerous. We can discuss whether affiliation adds too much work. How this has been handled is not WG consensus and is actually insulting.  
* Marcos: Then send another PR and we’ll go through it again, but with the requirements that I have as well.   
* Matt: As we propose the final spec, how do we reconcile the disagreements?  
* Marcos: It will be a case-by-case basis and we can go through it.  
* Wendy: I’m hearing both making sure we have sufficient opportunity to discuss changes before they are merged. The editors are critical to the maintenance of the document, and the WG are also critical. So we will make sure this is properly discussed before we agree to merges.   
* Ted: I threw some trouble into this mix by suggesting using each individual's URI from the W3C identifier page so we can keep names unique. Having the URIs would be nice to have, though perhaps not required. Maintaining this list over the next decade seems an odd argument; the updated contributors doesn’t tend to happen until the spec itself is reaching an entire new version.   
* Wendy: Everyone is trying to do the best for the WG. I appreciate the time people are willing to put in to get us there. I apologize that that takes us to the end of the call without getting to the remaining issues we wanted to discuss today, esp. 306\. I encourage people to add their thoughts to that issue.  
* Marcos: I will be out next week; if people have time to stay on the call we can maybe get that discussed further now.

### [Editorial: make digital wallets out of scope \#338](https://github.com/w3c-fedid/digital-credentials/pull/338)

* \[skipped\]

### [Define Coordinator and Client \#306](https://github.com/w3c-fedid/digital-credentials/pull/306)

* Marcos: Waiting for Mohammed that this is not UA specific. The coordinator is the component in the user agent which browsing context can make a call. If you have an iFrame that’s showing the sheet to pick a credential, you can’t have other calls happening at the same time. It manages different browsing contexts. The client side represents the UI thread, the interaction between the wallet and the user agent. Those components seem fairly generic. They should be treated as independent components.   
* Tim: But all those things are browser internals that are not to be specified.  
* Marcos: Yes, but they are consistent across all user agents.  
* Tim: The end result is, but the problem is that we don’t have a client and client platform definition. I’m less concerned about the term coordinator than I am about the definition of client in this context. I’m not the only one or I’d back down. We can’t explain how this spec and CTAP communicate because we don’t have a way to communicate. Technically this spec should only talk about the DC API and the UA, but it is still part of a larger ecosystem that we should acknowledge.  
* Marcos: I don’t think WebAuthn is a good spec to follow.   
* Tim: It is the mostly widely deployed authentication protocol in the world so I take issue with that.   
* Marcos: We have our own spec and we should focus on it. From a testable perspective, this has the behavior and exceptions and points of checks that are consistent across user agents. Happy to change the terminology to use something other than client, but the point is that this handles all the interactions and DOM behaviors that need to be queued up. This does model accurately what is implemented across the two UAs; we can demonstrate that with tests.  
* Matt: How is the coordinator/client model able to capture the process of presentation and issuance over hybrid? Is it flexible enough for all the ways DC API does issuance and presentation?   
* Marcos: That boundary is where it hands off to the platform and the platform does the CTAP stuff. It’s outside the boundaries of the spec. That’s why we put into the scope that anything in the platform layer is OUT of scope.  
* Tim: This is where the nuance is important. In Chrome, it’s handled by the client — not the client platform.  
* Marcos: Whether the assumptions hold is the important part; that’s why I’m waiting for Mohammed to come back to verify.   
* Wendy: Mohammed has proposed different terminology.  
* Tim: I don’t love it, but I like where he’s going.   
* Matt: Does the spec need to be this prescriptive about how the user agent works?   
* Marcos: It all needs to be handled and described.   
* Wendy: It sounds like there are still points of dissent among where these lines get drawn, as well as the necessity of drawing them in this spec.  
* Marcos: I can split on the client part. Do we have agreement on the coordinator part? Is that needed? It is the simpler part of handling the state machine. If we can agree to that, I’ll make a lot of progress.   
* Tim: I’m not going to block on that, so if that’s what you want to do, go for it.  
* Matt: I don’t doubt that as a WebKit maintainer, these need to happen for you. But from a spec perspective, it seems overly prescriptive. If the goal of the DC API is to say “here is the API surface that needs to be called by the browser”, I'm not sure we need more than that. I don’t think we need to get into what a user agent is to the level we are in this PR.  
* Marcos: OK, will split it then, which may help with discussions. I do feel strongly that this needs to be described at this level of detail for security reasons, but we can discuss further. 

### [Add request validation \#156](https://github.com/w3c-fedid/digital-credentials/pull/156)

* \[ran out of time\] 

## AOB

* 

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Wendy Seltzer (co-chair)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* Tim Cappalli (Okta)  
* Nick Doty (CDT)  
* Bjorn Hjelm (Yubico)  
* Helen Qin (Google Android)  
* Matthew Miller (Cisco)  
* Brian Campbell  
* Brent Zundel  
* Marcos Caceres  
* Lee Campbell

