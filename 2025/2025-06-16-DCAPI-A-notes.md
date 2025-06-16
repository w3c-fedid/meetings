# FedID WG Telecon \- DC API Series A, 2025-06-16

* Moderators: Heather Flanagan

* Scribe: Matt Miller

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
    * [Matthew Miller](mailto:mattmil3@cisco.com)  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (10 minutes)  
* DC API PRs   
  * [Add initial privacy considerations section for protocol requirements \#260](https://github.com/w3c-fedid/digital-credentials/pull/260)  
  * [Write initial privacy considerations for unnecessary use \#262](https://github.com/w3c-fedid/digital-credentials/pull/262)  
* DC API Issues   
  * [Security/Privacy Considerations: Trust boundaries between the Wallet and the Browser? \#269](https://github.com/w3c-fedid/digital-credentials/issues/269)  
  * [Protocol registry: Reviewing is not sufficient \#255](https://github.com/w3c-fedid/digital-credentials/issues/255)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (10 minutes)

* N/A

## DC API PRs 

### [Add initial privacy considerations section for protocol requirements \#260](https://github.com/w3c-fedid/digital-credentials/pull/260)

* Johann: Main focus is on delivering decent privacy considerations. How to get to requirements and add them to spec. Based on conversations with folks concerned about privacy, with deadlines in mind, what are concrete steps to take to get to where we believe a FPWD would not receive major objections?  
  * Outlined three things:  
    * Some API design choices are non-obvious without context of what it’s meant to replace. Can take much of what’s been previously drafted by, e.g., Rick Byers, others, and incorporate that  
    * (missed this one)  
    * Clarify permission vs consent. There have been comments about the browser not taking liability. We can’t enforce how wallets display and collect consent. Unlikely we can solve it today, or even in FPWD. Document that this is an issue in the spec.  
    * https://w3c-fedid.github.io/digital-credentials/\#user-permission-and-transparency  
* John: As we characterized the permission/consent problem, wallets and browsers don’t necessarily trust each other to collect the requisite permission/consent. Some wallets will be more concerned than others, there is tension in both directions.  
* Tim: For those who are new to this conversation, a majority of wallet folks don’t want the browser to ask for consent. This was a core consideration of the API design. Why do we have to put custom schemes (i.e., historical context) in the spec?   
* Nick: The reason we have the open question about this consent is, there are some misunderstandings of where in the ecosystem the user is providing consent. Understanding of consent as a legal matter is that the user is informed and free to decide. Why is data being collected? How is it being stored and shared? Answers to these questions need to be available. Based on demos to date no wallet is attempting to address these questions. Maybe people are seeing different wallets.  
* Tim: Many production wallets have scary prompts. Every production wallet I've seen is capturing consent.  
* Ryan (via chat): Every wallet I have seen is capturing consent in some fashion.  
* Nick: What about explanations instead? An alternative viewpoint is that the verifier should be doing this. Pre-presentation they’re in a good spot to do so. But that would be a different API design. But if we’re not clear on whether the wallet or verifier is doing it, we’re likely to have many mismatches.  
* Johann: Two pieces of user participation are considered: permission vs consent. Permission is (should be) mandatory per the spec. As spec authors, we trust what’s best for the user but don’t mandate any particular UI. In our model, there are important context details that the browser should pass along. Consent differs by jurisdiction, so it’s hard for us to make decisions on how this influences the spec. As all these frameworks are being written, it’s a problem that we can’t enforce disclosure. We will have to work on this going forward as these things are figured out.  
* John: The access and registration certificates workaround is still relatively…the prototypes are being built in the EU right now. Not excited about the possibility of verifiers having to buy certificates to become one. This seems to be the direction things are going. If so, how can we make this something that smaller verifiers can use as well? There may be some kind of balance between the legal entity making the request and what’s being requested. The wallet should be the final determination; it has the most context. There may be a role for this info to be provided for the wallet to act upon it.  
* Johann: \+1. Why do we want this information to be given out? The ability to consent is important for legal issues. Restriction of purposes, e.g., requesting government documents…there are specific things that user agents can make progress on.   
* Heather: The situations where the verifier or the wallet or the browser would be the right party to collect consent, you can find use cases for each scenario. A consent specification might be one way to standardize this, but we’re over-indexing on high assurance use cases.  
* Tim: There will be hundreds of millions of VDCs that will not require consent during presentation, e.g., in the workforce. Users are going to choose a wallet they trust (or be given one in the workforce) and trust will be determined in that way.  
* Nick: That’s a useful thing to describe. Johann has tried to put in some of that “spectrum,” and it’s appropriate that we’re focusing on use cases that have strong privacy implications. Even a thin layer on top of other permission and consent mechanisms creates complexity. If we design a system such that we hope consent will be collected at the right time and place, we’ll end up with lots of optional fields and softer suggestions. If we think people will get a higher click-through rate by skipping prompts, it’s likely to become the norm. We should make it clear that there are other scenarios   
* Matt: Does the first WD need to address the entire spectrum? Maybe we don’t have to. It would be useful to not have to. To Tim’s point, we are going to have a lot more less-user-privacy-centric use cases such as loyalty cards. Can start the first WD to focus on these simpler use cases.  
* Johann: Proposal is to keep current text as-is. The API is not doing consent, and calls out that there are problems around this and that norms will appear as the ecosystem moves forward.  
* Tim: If this topic is a concern, it should be handled at a higher level within the W3C. Why should this be handled differently than questions being handled in, e.g., FedCM? There are other intermediaries in other flows; it’s the same information from the same sources going through different APIs. We definitely need to handle it in FedID WG for FedCM, but this is an example of how lack of convergence leads to duplication of definitions.  
* Simone: There is a lot of interest in this API, so the API is different compared to FedCM.  
* Wendy: Thank you for engaging. As chairs we’re trying to see where things wind up. And thanks to Johann for drafting text to clarify questions and points of consensus. The FPWD isn’t the end state of our document; it’s to get a document out and secure the patent commitments. When we issued the first call for consensus, we heard that there’s not yet consensus but saw a path towards getting consent to *publish*. Are we in a good place with the text we have now to get consensus to publish it?  
* Sam: Tim is roughly right in that in FedCM, IDPs are allowed to gather consent. But it’s also true for the enumeration of well-known ID attributes that the IDP can use the browser to fulfill everything. This is one of the main differences: FedCM has a smaller number of use cases.   
* Simone: Just to follow up, we don’t have a FPWD, but we have the API available in two browsers. On the other side, we are in a different spot than we were for the first call for consensus.   
* Johann: There are a few smaller changes I would like to get in. Having the conversation today was a big one for me. To reiterate, I believe that the group overall will write down what’s currently here: we’re not facilitating consent via this API. We should remove the API’s consideration for collecting consent, with an issue to not lose track of this problem. These things being written down, it would be important to have agreement from the group that we should do this.  
* Nick: If consent is out of scope because “the wallet will do it,” then we need to define the mechanism for passing consent down. Maybe what people want is for the RP to explain their commitments, and confirmation for release is at the wallet side. Either side could be called (e.g., by a lawyer) “consent.” As a thing that involves multiple parties, different decisions will be made by each party. This document should contain guidance for all parties on how to properly gather consent.  
* Ryan (via chat): It probably needs to be in jurisdictional frameworks and we probably need to make sure the necessary information can ultimately be conveyed through the request protocols.   
* Ryan (via chat): Some of the wallet/credential specific consent presentation needs to also be part of the UI/UX recommendations. Not for the API but for the wallets (I do think this is part of what has been discussed in the EU wallet projects UI testing) and we are covering it in our NCCoE project.  
* Johann: Not saying that we’ll punt entirely on consent. It’s all a bit fuzzy. Is the suggestion that we build permission mechanisms into the API?  
* Nick: If we think that the purpose of all the information is to be provided by the verifier to the wallet, then we should facilitate that.  
* Johann: I’m aligned. We should make an issue to track this problem because it will involve future work to solve.  
* Nick: I’m fine opening the issue.  
* Johann: What’s currently missing from the current 15.9.3?  
* Nick: Addressing specific request ceremonies(?)  
* Tim: We talked earlier about request profiles. What happens when “your use case is not defined”? We can’t punt on this, it’s a fundamental API design decision. We need to come to consensus quickly or there’s no point in a FPWD. It would be catastrophic   
* Matt: Agreeing with Tim. The matrix of all the active players and use cases sounds way too complex to be captured in the DC API.   
* Rick: We appear to be struggling with two things: we designed it to be general-purpose, and where will consent be collected? We tried to design a system to be flexible. I’m not sure how we deal with that in the spec. We can identify scenarios in the future, and then define special rules for certain requests better than can be done with custom schemes. The one flow that Google has launched is the birthday correction flow \<shows a video\> Current Google Wallet UI is a bit simplified, but in some cases the issuer’s privacy policy can also be linked in the Wallet consent screen. This is an example of a case we’ll always have, privacy is communicated through a legal contract. Privacy requirements were gathered through a backchannel.  
* Heather: Johann, what are your biggest questions about the open PR?  
* Johann: I haven’t heard consensus that we should address consent. We can point to efforts like, e.g., EUDI requiring signing certificates and ask if we should integrate aspects of that into the spec. Not commit to it, but just write things like this down.  
* Wendy: Next steps: tagging issues into the draft, that we commit to resolve (post-FPWD) before the next formal draft.  
* Johann: Hopefully these are minor edits. The main sources of issues are ones that require longer conversations, a meta issue to collect the issues to discuss over time. The question of facilitating consent is one we can call out as something we’ll continue discussing as we don’t currently have a working solution; that’d help get to FPWD.  
* Heather: At no point did we expect things to be perfect. I’d be just as happy to open the FPWD call for consensus ASAP to say, “we’re making progress, having the conversations, so we should be able to move forward.”

### [Write initial privacy considerations for unnecessary use \#262](https://github.com/w3c-fedid/digital-credentials/pull/262)

* Johann: I think we talked about some of this earlier in the call. When does the user agent get involved, verifier certification, etc…   
* Nick: The discussion today with Marcos in that thread and Martin in another PR was whether authorization for access to government credentials needs to be communicated. Marcos seems to think that’s already the requirement, others seem to think it’s never the requirement. We should figure this out.  
* Tim: There is nothing that requires reader verification. I was mostly trying to correct comments in the PR that state it as a fact that the verifier has to be verified. This spec is certainly not the place to state that verifier must be verified.  
* Johann: I’m agreeing with Tim here that there are different frameworks requiring reader verification. If we don’t agree on this at a societal level it’s hard to bake that into the API.  
* Lee: Not even the EU mandates it. I’m not aware of any country that does.  
* Nick: Is there anyone from Apple or Mozilla that says we have to verify the verifier?  
* Benjamin: I thought it was a part of the latest ARF that says reader verification is required  
* Martijn (via chat): Not as a requirement in this API. Whether to require it is up to the wallet/ecosystem etc…  
* Tim: One set of wallets for one specific doctype. You need infrastructure to do this. A web API mandating deployment of X509 architecture can’t be done, of course.  
* Lee: It’s likely to be loosened to an optional requirement based on the assumption that users should be free to present their credentials where they want. It’s not mandated in the US, maybe in Japan.  
* Johann: I’m very happy to add this as an issue to GitHub to discuss and explore.

## DC API Issues

### [Security/Privacy Considerations: Trust boundaries between the Wallet and the Browser? \#269](https://github.com/w3c-fedid/digital-credentials/issues/269)

* 

### [Protocol registry: Reviewing is not sufficient \#255](https://github.com/w3c-fedid/digital-credentials/issues/255)

* 

### 

### Any Other Business (AOB)

* 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan  
* Nick Doty (CDT)  
* Benjamin VanderSloot (Mozilla)  
* Lee Campbell (Google Android)  
* Matthew Miller (Cisco)  
* Ryan Galluzzo (NIST)  
* Andrew Regenscheid (NIST)  
* Tara Whalen (W3C, Privacy Lead)  
* Chris Needham (BBC)  
* Wendy Seltzer  
* Ashima Arora (Google)  
* Bjorn Hjelm (Yubico)  
* Mohamed Amir Yosef (Google Chrome)  
* Helen Qin (Google Android)  
* Mike Jones (Self-Issued Consulting)  
* Simone Onofri (W3C)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Christian Bormann (Sprind)