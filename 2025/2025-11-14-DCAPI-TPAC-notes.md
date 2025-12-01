# W3C TPAC 2025 \- Federated Identity WG/CG \- DC API

## Friday, 14 November, @ 09:00–12:30 UTC+9 — Floor 4 \- 401

See the [W3C TPAC Calendar for connection information](https://www.w3.org/events/meetings/72ac91c8-aede-4efa-8ab3-827eba494cb9/)

# Agenda

* Administrivia  
  * Scribe volunteer(s)? Mohamed, Heather  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* [Registry](https://github.com/w3c-fedid/digital-credentials/issues/396) (all) \- 50 minutes  
* [Security Considerations](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.0) (Simone) \- 50 minutes  
* Privacy Considerations (any changes based on Registry decisions) \- 20 minutes  
* [~~Wallet Selection Binding~~](https://github.com/w3c-fedid/digital-credentials/issues/382) ~~(Lee) \- 20 minutes~~  
* [Digital Credential UX Research](https://docs.google.com/presentation/d/1YwB-ocoI5Y7MWtMxh4eQVp1qm6SfUBKHoSt81E_oRu8/edit?slide=id.p#slide=id.p) (Marian) \- 30 minutes  
* Timeline to CR/REC (remaining blockers) \- 15 minutes  
  * [Transition to CR process](https://www.w3.org/policies/process/#transition-cr)  
  * What do we expect to demonstrate in terms of adequate experience at the end of CR?  
  * What features are at risk?  
  * Need to assign Horizontal Reviews. ([Issue \#227](https://github.com/w3c-fedid/digital-credentials/issues/227))  
  * Need to double-check what other groups/orgs we need to ask to review (see [Section 5 Coordination](https://www.w3.org/2025/02/wg-fedid.html#coordination) in our charter).  
* Process (Process CG) \- 10 minutes

# Notes

* Heather: Administrative details, agenda \[switched to put Registry first\]

## [Registry](https://github.com/w3c-fedid/digital-credentials/issues/396) (all) \- 50 minutes

* Heather: Registry has been controversial, different opinions, Tim created an [issue](https://github.com/w3c-fedid/digital-credentials/issues/396) to list the options.  
* Rick: Not all options are there. There is tension between the EU wanting openness and autonomy, and having a spec we can reason about in terms of security and privacy. We should meet the regulator requirements for adoption. One extreme is we refer to other specs for parts of our specs; another option is to exhaustively list all considerations in our spec, which is a cumbersome task,  
* Martin: This group is responsible for delivering APIs that can be used and implemented interoperably. What’s there now is almost the opposite of what I’d like to see for advancing interop. Ideally, I’d like to see a set of choices listed, and steps necessary to add another to the list. E.g., in the Attribution API, we have an extension point, and would describe each choice and how to integrate it. Here, you’d see the choice and be able to walk the tree, understand the properties on review. The Privacy section says there should be no backchannel between wallet and verifier, but the enrollment phase, as I understand it, requires that. Understanding integration points of this unique API is important, even if the statement is explicitly deferring to someone else. So I’d say list the concrete options, maybe document the requirements for further additions. If you’re going to do a registry, have an external process for additions, need to do more to document integration: interop requirements and privacy and security requirements (what we owe the users). Having a registry is more difficult than having a list of things.   
* Tim: The protocols aren’t in the registry yet because that’s the easy part to add, and the rest is the hard part. Could you elaborate more on the interoperability difference between this API and others?  
* Martin: When someone invokes create, what is being done? Identify the place parameters are being passed  
* Marcos: mdoc doesn’t define how to implement, just a data stream. We’re not in a position to be responsible for defining that, on the W3C side. If there were things abhorrent in the spec, you could throw a security error.   
* Tim: But that’s not interop. Protocol A or B, you pass parameters in, pass it to the underlying platform.   
* Martin: Then say that.  
* Mohamed: Helping implementation is one thing; security and privacy is another. Understanding the consequences is different from what you need to implement.   
* Nick: Not entirely certain I understand the new option. These options would be written into the spec, with explanations of how they satisfy privacy and security.   
* Martin: And choice of registry is orthogonal.  
* Nick: I’d be more on the side of having detailed requirements that we as a WG write down. We just heard a presentation from security researchers about holistic review, that we can’t understand or ensure the privacy or security properties unless we review all the pieces together.  
* Rick: My proposal, concretely, would be to remove the registry and explicitly specify 4 or 5 protocols: OpenID4VP 1 signed and unsigned and multisigned, OpenID4VCI, and ISO mdoc (part 7, annex c). There may be a few more, but not 20 more.   
* Tim: Clarifying question   
* Mohamed: What are our expectations of implementers? Not to allow any unlisted protocol?   
* Rick: I’m suggesting that our spec normatively say the API fails if something unlisted happens.  
* Marcos: We had changed it… How are we justifying inclusion? Registry criteria were based on review. We can get rid of the criteria, but it feels a bit sad   
* Nick: Rather than having an open-ended registry with requirements, we list the implemented options, that would satisfy my recommendation that UAs should implement only a limited set of options. Then privacy and security: my preference would be to set requirements on them, but my second concern is that we be honest: if people are implementing, at least we know.   
* Rick: Talk about why we’re implementing them. I’d say the protocols I’ve listed have all put a lot of thought into their privacy and security properties. They all have WGs where I can engage to suggest improvements; they can meet our security needs. And, if we don’t include all these protocols, I believe we won’t get adoption. So we should continue to invest to help these protocols meet our security needs.  
* Martin: As Nick says, these protocols may not meet all of our needs. Documenting that honestly is next best. There may be an option to add constraints, take those questions to the groups developing the protocols. This is making sense to me. Would help in the holistic review Nick was talking about.  
* Marcos: I like this proposal for a number of reasons. Shared learning. For instance I’ve never attempted to implement OpenID4VP. If that were to happen, I’d like to learn from other implementers. Likewise if Mozilla were implementing mdoc, they’d likely want to hear our experience. Feeds back into privacy and security considerations at the protocol implementation level.   
* Tim: We talked about this at WebAuthn yesterday. Can’t have 11th hour feedback to protocol groups. Need earlier feedback while their protocols are being developed. The W3C process needs to be improved as well.   
* Heather: We’ll talk about the W3C process at the end.   
* Nick: A couple important comments about justifying our choice. I don’t know that the docs all address privacy. Part 7, what I’ve seen, doesn’t address privacy considerations. The participatory process also doesn't seem right. I can’t go to ISO meetings or see conversations. Those were other requirements we were intending to put on registries. If we want to put reasons for including protocols, that would be valuable. Let’s make them accurate  
* Rick: I recognize not everyone is in the same position. I was careful to say “I feel *I* can participate” Nick: thumbs up.  
* Simone: ISO has security and privacy. We are in contact with ISO, and can have a liaison with them to get access to the spec. We can provide a security & privacy self-review questionnaire for protocols that must be public. Important because it’s not just about protocols, but profiles.   
* Marcos: This is new to me. I don’t understand how we can participate in these meetings.   
* Simone: We can get documentation, as liaison.   
* Tony: Which category?  
* Simone: I sent an email.  
* Martin: ISO is opaque to lots of us. Whatever we can do to make it less opaque is good. I don’t feel I can meaningfully contribute to lowering opacity, so comments about 11th hour review don’t feel appropriate. Their process is not open and transparent. Standards we develop here are voluntarily adopted. If they’re not in a fit state to be adopted, they won’t be adopted, in all directions. I got on the queue to talk about what happens with multiple choices: you need to think about who has to implement what. If we’re talking about the difference between ISO and OpenID paths, who is able to implement one or both? Browsers, relying parties, wallets. If you don’t pin something down, you often get interop failure.  
* Mohamed: I’d like to clarify Martin’s comment on mdoc features. Would we allow unsigned cross-device requests? Do we go that far?   
* Martin: In the universe of possibilities, some of which have terrible privacy and security properties, it would be reasonable to say we effectively have a profile of things we’re implementing. Say “no thanks” to some features we don’t want, in a targeted fashion. Not full-scale profiling, but if someone identifies a risk, document for that specific protocol integration.   
* Marcos: The liaison with ISO might help. Work predated this group  
* Tim: Part 7 was done inline with this group. Format shouldn’t be of concern to web API. That’s a layer removed from where we’re operating. You shouldn’t need to understand how to implement mdoc.  
* Marcos: In WebKit, we need to translate to WebIDL, understand the security, and possibly throw an error. When you get something back, you need to put it into the digital credential object. Not just throw it over the wall.   
* Tim: That’s an implementation decision.   
* Heather: We’ve spent lots of time on this option, want to hear if anyone wants to advocate for another.   
* PLH: 2 things. On mdoc reference, one consideration is whether spec is available for free to implementers, web developers in general, even if you’re not in this room. We can talk again to ISO. WG Charter says “secure and private, agnostic to different identity systems”. One thing I’m not certain of: if the implementation is not listed, is it an error? Concerned about forward compatibility.   
* John: At the highest level, I wish people would stop saying mdoc. We’re talking ISO presentation formats. ISO annex c transports. For the DC API, we should concentrate on presentation protocols, not complicate the terminology of underlying document formats. On the OpenID side, we’ve done a lot of work on profiling security and privacy. That’s what HAIP is all about. We can’t stop bad governments, bad wallets, bad platforms.  
* Heather: If anyone wants to argue for anything other than this option 7, please …  
* Daniel: This is not going to solve one the problem of engagement, but ISO standard will likely be made freely available next year    
* Mohamed: In case of multiple requests where only some of the protocols are listed, should we fail or accept partial? Backwards compatibility questions.   
* Rick: I’m supportive of saying ignore, and don’t pass through to the platform.   
* Mohamed: Once we ignore and if there’s only one, it will fail  
* Rick: Ignore is important, so if there’s a 2 in the future, wallet can get both.   
* PLH: I don’t see the difference between drop and ignore. If I send a protocol that’s unlisted…   
* Mohamed: If you pass a request with no requests, you get the same failure as if you pass an unsupported request. If you request one supported and one unsupported, the supported one goes through.   
* Heather: Do I hear a consensus on this topic? Tim is taking the action to write the first draft.  
* Marcos: Mohamed and I will take action on processing.  
* Wendy: Please do that, when we have the text, we can make sure that the text reflects the consensus in the room and share it on the mailing list, too. It is exciting to have a tentative conclusion. 

## [Security Considerations](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.0) (Simone) 

* Simone: No presentation, just a document. ([link](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.0))  
* Simone: The objective is to agree on the direction and approach, not necessarily resolving the security considerations in detail. The document covers API, protocols, and other components. The idea is to reach consensus on the document and then extract part of it into the spec, cross-reference other specs, and identify missing parts in the document. The idea to have a weekly meeting (Europe-friendly time) to discuss the security consideration, probably in the security IG. We should probably also add what is expected from other parties to the security section. Some discussions are going on regarding what malicious extensions might do (which can be discussed in the extensions WG).  
* Marcos: WebKit sent a PR to themselves to protect against other extensions forging the API; could send that to spec .  
* Simone: One idea is to protect against forging APIs discussed with Mike West not specifically about DC API. We should at least document the assumptions, potentially challenge them, and address related threats. And be explicit about what can be implemented in each level. Following RFC 3552, list exactly what is within the scope, and what isn’t, and accept any residual risks.  
* Marcos: This goes back to regarding having two implementations, and every change in the algorithm has a justification. I don’t like the current format of the security considerations because it is generic. We should, for example, list exactly where fingerprinting is and where to prevent it. My proposal is to list explicitly what kind of protections we did to address zero-click attacks, one-click attacks, etc. This is better than saying, for example, “QR-Codes are bad”. Yes, we can list general mitigations, but those mitigation are listed somewhere else.  
* Simone: Yes, this is the approach we are going to follow. The full list of threats could be published as a group note.  
* Simone: Who’d like to join in this exercise? Mohamed, Rick, and Marcos raised their hands.  
* Nick: Process SGTM. Are we going to present the rest of the document today?  
* Simone: Document is long, if there is time we can quickly give a guide of how to navigate.  
* Nick: I have some comments, don’t need to talk about them now, can hold for another meeting.  
* Heather: I am not planning to go through it, but I would like to make sure we are very clear on what should be included in the spec, and specifically what the DC API should be doing.  
* Simone: Sounds good, we can also modify the model if requested.  
* Nick: My concern is that with the set of assumptions we have, it is tempting to make those assumptions, but for example I don’t agree with the assumption that the “Wallets can be trusted by the user”.  
* Simone: The question of trusting the wallet is complex. We should indicate if we don’t trust the wallet, and what mitigations are in place to address that.  
* Nick: We have some mitigations, but it was an example of the assumption I don’t agree about.  
* Simone: We can now go through the structure, and different levels, and challenge the assumptions.  
* Zahra: We have assumptions in the beginning of the document. Then we have a discussion of what can go wrong. We try to list at which layer each threat occurs. We mapped the 16 threats we found to different layers. We then describe the different threats, attack scenarios for each, and finally the proposed mitigation for each attack, indicating which layer is this mitigation.  
* Marcos: This is great, and what can be useful here, it has 4 columns, WebKit does this, Chrome does, and the spec does this. My concern is, there is a lot of stuff here, but I don’t want it to be hypothetical — I want to see where in the code this is done, Simone: this is why I need your help, Marcos: yes, I can help, and Mohamed can help with the Chrome side.  
* Simone: My proposal is to have an implementation requirements section in the spec that lists the requirements of the protocols.  
* Zahra: We also highlighted which threat is coming from which layer.  
* Johann: I am thinking about how this can be transformed into a security section. The first section is a list of requirements, but it is relatively uncommon to have a list of requirements in the security section. This is a non-normative consideration; we shouldn’t add normative requirements.  
* Marcos: So far, we only add things that have been implemented to the spec.  
* Johann: Realistically, we should expect web developers to read those specs to have a secure implementation.  
* Simone: If the audience is protocol ???, it is relevant.  
* Tim: HTML spec can be put into developer mode.  
* Nick: I think we should have verifier requirements.  
* John: There are verifier requirements, but not part of the DC API. openif4vp and ISO Annex-C both have verifier requirements. E.g. HAIP is all about that.  
* Martin: There is another way to think about it, we are documenting the expectations from other parties of the system. Listing those expectations makes it easier to reason about the system at the end. We cannot force anyone to do anything; those standards are voluntary, especially on the verifiers' side.  
* PLH: We should focus on what is relevant for the DC API, and have companion documents cover other aspects potentially in other groups.  
* Marcos: We have beautifully detailed examples in the spec. I will be sad if the same doesn’t exist on ISO and openid4vp sides.  
* John: We all agree this information should exist in a consumable way. But they exist in other places.  
* Tim: We should define only the DC API, and stay away from the details of the protocol. We have a developer guide website for end-to-end examples.  
* Johann: This is a non-normative section, and shouldn't have normative requirements. Putting requirements in the algorithm is a great idea. There should be no verifier requirements in W3C spec text; they don’t read it. We could potentially list some requirements in one separate section instead of weaving them into the spec.   
* Kristina: Those verifier requirements are listed in openid4vp, and I am sure ISO has something similar. But the example on the screen for the example needs more details. It would be great if the DC API focused on the web-platform part, because this work is done somewhere else and we should work together on it.  
* Simone: This document is a living document and a threat model for the whole ecosystem; out of it, a PR to the spec will be extracted.   
* Kristina: We explicitly separated the functions of the DC API layer from the protocol layer. Feedback to the protocol is highly welcomed. But I’d prefer if we keep this document for DC API assumptions only.  
* Heather: We discussed the structure; we have volunteers to help. Anything else?  
* Simone:  
* Heather: We will talk about whether the privacy consideration section will change. We will probably finish early and not need the full 20 minutes.


## Break

* Heather: Use Zoom for the queue. We took [Wallet Selection Binding](https://github.com/w3c-fedid/digital-credentials/issues/382) (Lee) off the agenda due to lack of new information. Context and details in the issue.

## Privacy Considerations (any changes needed based on Registry decisions?) \- 20 minutes

* Heather: Any changes needed based on discussion this morning?  
* Nick: Two things relevant for us. The registry was going to include a requirement that we conduct privacy and security reviews of those protocols. Suggest that we do those even if not as part of the registry inclusion step. If we’re committed to including 4–5 protocols, no matter what, then once we’ve done the review, we should update the privacy considerations to include the implications of using them.  
* Marcos: Agree. For the security considerations, hoping we can remove the bulky ones we have, and start again for a tailored set.   
* Johan: The privacy considerations try to look at what we should ask of protocols. There are probably things we’ll learn as we try to integrate protocols in the spec.   
* Marcos: Who else might help Tim with removing the registry language?   
* Tim: I’d like to commit to a draft PR of the big changes by the end of the month.  
* Marcos: Mike, the current security considerations weren’t meeting your needs.  
* Mike: I will happily review any text you produce.  
* Heather: Tim is holding the pen on registry changes to the spec. We have a group of people who have committed to work on security analysis. I hear we want to do protocol reviews. Question: for an S\&P review on HAIP and others, is that something we want to do as a one-off for this WG, or something that could be used elsewhere?  
* Tim: An artifact produced in this group could be used elsewhere.  
* Nick: I’d mention it to the Privacy WG and try to get their help.   
* Mohamed: In the privacy considerations, we should take care to consider issuance. Also the cross-device flows, such as using CTAP..   
* Nick: We’ve covered privacy considerations from the registry discussion. We still have a lot of open issues on privacy awaiting discussion.   
* Johann: There are three types of issues; those we can work through individually; big fundamental philosophical questions where the group will struggle to find consensus; those already resolved by the registry decision. 

## Digital Credential UX Research (Marian) \- 30 minutes

[Deck](https://docs.google.com/presentation/d/1YwB-ocoI5Y7MWtMxh4eQVp1qm6SfUBKHoSt81E_oRu8/edit?slide=id.p#slide=id.p)

* Marian: literature review and design principles. Finding research on UX of digital credentials, derived six key themes:   
  * usage expectations — store a wide variety of credentials, variety of uses, including anonymity combined with verifiable attributes.   
  * Inaccurate mental models are often reinforced by the card metaphor. But this doesn’t clearly cover aspects like selective disclosure. Finding and using a more suitable metaphor could help.   
  * Trust in DC. Trust is built through consistent operation and the reputation of the wallet operator. QR-code is identified as a source of friction. Trust is transferred from some entities to the wallet, but can be overridden. Media can impact adoption (e.g., negative reports affected German eID adoption).  
  * Information needs: users need to know verifier reputation, purpose of data collection (contextual integrity), and relation of data collected to the needs. Transparency helps to assure users. Concerns about over-collection, lack of agency. Info needs go beyond origin requesting data.   
  * Users weigh benefits (convenience) against privacy costs. Often, the benefits are more immediate and tangible. Users can become desensitized to disclosure from multiple prompts (e.g., Android install-time prompts vs. those in context of use). Users will take mental shortcuts. So the entire UX system needs protections that limit harm.   
  * What can be done? Habituation is difficult to mitigate. Show as few prompts as possible; they should feel helpful and include impactful information.   
* Summary: Encourage helpful mental models (of selective disclosure); avoid habituation by limiting prompts to those on which user can take useful action; make site reputation and purpose of data collection available for decision making; use technical safeguards to limit the harm users can get themselves into.  
* UX design principles:  
  * Friction in design, a spectrum of friction based on data sensitivity and data exposure.   
  * Principles: get out of the way where possible; seamless experience between browser and OS (users don’t know the divided responsibilities); incentivize sites to supply important information; tailor UX to include that info …  
  * Choosing friction: when unlinkable ZKP, low friction; lots of disclosure for minimal purpose, high friction. Consider information asymmetries.   
* From chat:   
  * Martin: Not sure that I agree that the risk assessment is completely linear outside of the y=x line in that chart. The risk compounds based on exposure \+ sensitivity, but either one being high can be a risk. I don't think that "ZKP \= low sensitivity" is a good assumption. It depends on what the proof proves. Verifiable age is, at some level, sensitive. I don't know that we should broadcast it completely without friction. Streamlined, yes.  No friction, probably not  
  * Wendy: And we may want friction for policy reasons beyond the individual user.  
  * Nick: But maybe some other term there could be useful. Unlinkable (both in presentation format and data type) low-sensitivity.  
  * Michael Kleber: No matter what you think of age specifically, there surely are some single bits of identity-derived information that deserve more friction. If a government can set up a scanner on the street that will point out everyone walking by who is not a citizen, then something has gone very wrong.  
  * Alan Buxey: But a site could give a ‘reason’ that is dubious or wrong....  
* Provocation: example UXes with varying degrees of friction.  
* Ben: Lots make a lot of sense. Two points you made are in almost direct conflict. The degree of friction increases the aptitude for friction, but you’re also increasing friction on high-risk sites  
* Rick: People become habituated by aggregate prompts, so you want to reduce those that are not actionable.  
* John: We have multiple layers of selection. At what level do you provide guidance? Figuring out who does which asking may depend on the ecosystem of the given credential, e.g., in Europe, we expect there will be registries of relying parties, but not so in the US. Ideally the browser shouldn’t have to understand every ecosystem of every credential. Getting the user to understand you might have an SD credential where all the fields get disclosed, different kinds of correlation … Lots more that makes it hard for users to make good choices.   
* Rene: There’s a certain amount of indirection in the ecosystem; over-asking is difficult to detect as a wallet. How do you coordinate system prompt and wallet prompt to understand legit/illegitimate asks? In the EU, there’s a registry; in other environments, there may not be — so how does one detect and display this info?  
* Marian: Yes, let’s work on getting information to make enough available to provide good UI  
* Nick: Based on that exchange, we need to make sure the API surface has the ability to provide relevant context. If a verifier can commit in a legally enforceable way, we want them to have a way to put that in the UI. Otherwise we get overprompting and habituation.  
* Erik: This UX research appears to be heavily focused. Have you done research on desktop browser scenarios which involve cross-device flows? It would likely have more friction and affect how users respond to different UX, affecting the analysis. For example, a reduced-friction flow might only be 5% less friction if the user needs to pull their phone out either way.  
* Marian: Some, not shown here. Try to front load as much of the information users need as possible.  
* Martin: Encouraged by the point that people pay attention to what they hear in the press in their choices to provide information. Suggests if you build in transparency, you have a way to hold actors accountable. To John’s point, you don’t want all actors in the system thinking they’re responsible for adding friction. Don’t want so much friction that we end up back at taking photos of passports. 	You didn’t say much about the two blank quadrants. Not necessarily linear. Like this case for understanding not just the info presented, but also the context in which it’s presented. 

## The Path to CR

* Heather: We had a few big things to do before we could start estimating timing. Needed to get registries settled; horizontal and wide reviews.   
* Marcos: Not so much when as how. Let’s look at what we need to do to get to CR, keep things scoped. Division of labor. With Tim taking on the Registry PR, Mohamed and I will focus on algorithms. Checks and balances among the editors. Being meticulous about testing. By the time we get to CR, we will have 2 fully interoperable implementations. Division of labor helps me see where I need to focus. Clarify the highest priorities to help the editors focus. Make PRs small to make them easy to process  
* Wendy: Are you suggesting that people are going through the spec, and the WG will triage the issue to understand if this is a CR issue? Keeping the discussion in the issue?  
* Marcos: At the end, other people have different knowledge, e.g., Tim on IETF stuff, and also on the developer’s side.  
* Heather: Hearing please make sure there's a clear division of labor and a clear explanation of why things are being proposed.   
* Nick: I noted before there’s a lot of privacy work to be done. Lots of potential design work, e.g., in response to Marian’s presentation. Not just talking about writing non-normative text and getting horizontal review.   
* Tim: We also need to leverage other orgs, e.g., connect Marian with FIDO.  
* Heather: We have more work to do before requesting reviews.  
* Marcos: We don’t need to wait for CR to request review.  
* Wendy: We have some placeholders for some of the issues. We have asked for champions to help lead the review work from the WG side. We have seen good progress on accessibility self-review from Matt.. A lot of work is happening on privacy and security. We have internationalization as an area looking for an internal champion. We have a request in the chat for architectural review.  
* Rick: I volunteer for leading the internationalization review.  
* Nick: Internationalization may have considerations around the different kinds of national IDs, for example.  
* Marcos: And we can report bugs that we see in one place.  
* Heather: We’ll be asked about features at-risk; we need to check the charter and get reviews from other groups mentioned.  
* Tim: We’re still debating roles and responsibilities of different parts of the ecosystem. We’ll keep going in circles and missing timelines if we can’t agree on the basic shape of the API.  
* Marcos: I think we can solve it.  
* Rick: We have a sense of urgency because there’s deployment on custom schemes already. Can we agree that we in this group focus on the places where we agree there’s some difference between this flow and custom schemes? Better to devote our time to things that we could do better than custom schemes and differentiate our API, e.g., from Marian’s presentation, chance to display purpose.  
* Marcos: I don’t like that pressure from a bad implementation.  
* Rick: We can’t get there in 6 months if we’re trying to build a threat model for the entire ecosystem. Let’s focus on reviewing the things that are different in our API.   
* Heather: A simple question won’t get the same answer from people who have different concerns. Where we know we’ll get questions, I’d like us to write down where we think the answers would be found (e.g., in a different layer). If we can document a bit more clearly for those who don’t know where to direct their worries, it would be helpful.   
* Simone: This is where we think the threat model can help differentiate between our problems and not our problems.   
* Tim: I agree, but I’m not getting the sense that everyone agrees.   
* Simone: Define the scope clearly to our API.   
* Heather: I’m going to take something that was suggested earlier: does security and privacy analysis of protocols fit?   
* Simone: We should focus on our spec: define requirements for protocols.  
* Martin: I don’t think security review of protocols has been suggested. We can use the work that’s been done on protocols to understand them. Document the expectations of protocols, not end-to-end system analysis.   
* Tim: I don’t disagree, don’t necessarily hear it from everyone.  
* Martin: Some people in this room will do complete system analysis in order to understand implementation in their product. They bring that expertise here to analysis of the API.   
* Marcos: We’ll be updating this thing for a while, so CR isn’t particularly relevant.  
* Rick: To disagree, we’ve heard from regulators that until we reach CR or even Rec, we won’t be referenced  
* Heather: Speaking as chair, I like to see specs graduate. Will that benefit the ecosystem? That’s why we’re doing it.   
* Simone: We have multi-layer threat models that we can use to focus on our layer.   
* Marcos: We’re looking at a year or two \[from now\] to get to Rec. 

## Process

* DW: We are reaching out to working groups to talk about the Process.  
* \[ Hands show some familiarity with [W3C Process](https://github.com/w3c/process/) \].  
* DW: Thanks for chairs for supporting the AB work.  
* … The goal is to collect and address top concerns.  Top concern is to make W3C grow and be relevant to the industry.  Addressing that in a new interest group: Exploration IG.  
* … Question 1: For a WG are there any blockers you have encountered to advance documents on the REC track?  
  * Heather: We were just talking about that.  
  * Marcos: These are not blockers.  Horizontal review means getting the quality we expect. The questionnaires should be considered and standardized more. Culturally we need to identify who is responsible for something.  Chairs and editors often get stuck doing the work, even if they aren’t the best person to do that.  
  * DW: I’m hearing that we don’t have standards for horizontal review.  
* …Question 2: Are there any tools that might help?  
  * Marcos: It might be interesting to try making tools for standardized processes.  Hard to know if those tools are able to get in the way, informal things (google docs) can be easier.  
  * Heather: I’ve heard repeatedly that the reviews take a long time.  A very long time.  In some cases, the review arrives after deployment.  Thinking about how to resource reviews so that they can be quicker is something to consider.  
  * Marcos: We do have at the top of the document, editors who are accountable entities.  As we make changes to specs, we can make more people responsible.  Maybe identify who is responsible for what. Editors can be the worst people for some things. Experts who develop the specification can help.  Set timelines.  
* Question 3: Formal objections.  Any feedback on experience with FOs?  
  * Heather: Is this about how hard it is to raise or answer them?  
  * DW: Any bad experience at all.  
  * Heather: We had an FO on the charter.  
  * Tim: That delayed this work 6-7 months.  
  * Rick: Is 6-8 for an FO what we would expect?  Is there a system in place to cap the time?  
  * DW: What do you want?  
  * Rick: I would want a process to have FO within 4 weeks.  WIth a deadline, no more than four months cumulative.  
  * Nick: Faster processing would help absolutely everyone involved.  Sometimes on charters, we end up with an FO and a long delay just because we didn’t uncover the issue earlier in the process where it could have been fixed.  That has happened in other places, so getting feedback earlier might allow us to avoid FOs.  
  * DW: We should be more interactive?  
  * Nick: Getting interaction from people who might object, we might do the work before the charter is proposed.  
  * Tim: Literally, some of these feel like an 11th hour drive-by.  I would like to avoid extending this backwards into the pre-process.  
  * Heather: In our FO, it was a challenge, because when we charter, you set a deadline.  You need to be open to feedback up until that deadline. That can still be frustrating. Trying to get the people who submit an objection to participate, so that they don’t repeat their objections is frustrating.  
  * Nick: Maybe another step there to improve the speedup is that it can be frustrating if the objector doesn’t respond, if the response doesn’t satisfy them.  It might be faster to determine early if this is something that we resolve by consensus or not.  Sometimes you can see that there isn’t going to be an agreement, move on.  
* Question 4: (Angel) Anyone has any comments on the Invited Expert program or Code of Conduct?  Or anything else that the AB should know about, whether it is the Process or the work of the AB?  
  * Marcos: If we invite people, we should support them.  
  * Simone: (I’m sorry, I couldn’t understand what Simone was saying here.)  
* DW: Thank you everyone.

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Philippe Le Hegaret (W3C)  
* Rick Byers (Google Chrome)  
* Mohamed Amir Yosef (Google Chrome)  
* Wendy Seltzer (co-chair, invited expert)  
* Tim Cappalli (Okta)  
* Nick Doty (CDT)  
* Bjorn Hjelm (Yubico)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Marian Harbach (Google Chrome)  
* René Léveillé (1Password)  
* Alan Buxey (MyUNiDAYS Ltd.)  
* Marcos Caceres (Apple)  
* Martin Thomson (TAG, Mozilla)  
* Simone Onofri (W3C)  
* John Bradley (Yubico)  
* Hiroyuki Sano (Sony)  
* Erik Anderson (Microsoft Edge)  
* Simone Onori (W3C)  
* Yi Gu (Google Chrome)  
* Harald Alvestrand (Google Meet)  
* Chris Fredrickson (Google Chrome)  
* Natalia Markoborodova (Chrome DevRel)  
* Suresh Potti (Microsoft Edge)  
* Siddhartha Pandey (Microsoft Edge)  
* Kristina Yasuda (SPRIND)  
* Benjamin VanderSloot (Mozilla)  
* David Waite (Ping Identity)  
* Henna Kapur (Visa)  
* Tatsuya Katsuhara (Digital Agency of Japan)  
* Max Crone (1Password)  
* Hadley Beeman (W3C TAG)