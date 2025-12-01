# FedID WG Telecon \- DC API Series A, 2025-12-01

* Moderators: Heather

* Scribe: Wendy

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
  * [Add terminology section, merge in Model \#387](https://github.com/w3c-fedid/digital-credentials/pull/387)  
  * [Define Digital Wallet \#386](https://github.com/w3c-fedid/digital-credentials/pull/386)  
  * [Security Considerations](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.lgu8jgz2n99n)  
* Any Other Business (AOB)

# Notes

Heather: Admin reminders. Code of conduct note: at TPAC, many observers told us they enjoyed the interactions in our group. Thanks for helping us to keep that good tone\!

### Ecosystem Updates (10 minutes)

* \[none\]

## DC API Issues

### [Add terminology section, merge in Model \#387](https://github.com/w3c-fedid/digital-credentials/pull/387)

* Heather: Some conversation on our Series B call last week. Request to break into individual PRs per-term. Confirming that with this group.  
* Tim: Not a big deal. I’ll do it when I get a chance. There may be nothing left there because it got pulled into other PRs already.

### [Define Digital Wallet \#386](https://github.com/w3c-fedid/digital-credentials/pull/386)

* See last week’s minutes: [https://github.com/w3c-fedid/digital-credentials/pull/386\#define-digital-wallet-386](https://github.com/w3c-fedid/digital-credentials/pull/386#define-digital-wallet-386)	  
* Matt: Seems there’s still division between preference to refer as wallets vs credential managers. Can you help clarify which way things are leaning?  
* Rick: I don’t think we discussed this at TPAC. I don’t have a strong opinion.  
* Heather: Chair hat off, I’d be happy to avoid the term digital wallet, it’s messy.  
* Tim: Many other venues trying to get away from the term. We can add an alias. I’ll put it in my bucket to look again.   
* Matt: I too support calling it credential manager in the technical spec.  
* Heather: I think we have consensus on the change.  
* Matt: As we have editors split among calls, I wanted to hear from Mohamed.  
* Mohamed: If I’m the tie-breaker, I’d say credential manager.

### [Security Considerations](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.lgu8jgz2n99n)

* Heather: I fed lots of relevant documents into chatGPT; it gave me something plausible — [DRAFT: DC API Security Considerations](https://docs.google.com/document/d/1yeXZ9-IWWwXbCCFMnVGgA_Qczi_gqpAkQKX5c8jlIv8/edit?tab=t.0#heading=h.erv5qfexoxge).  
* Simone: I also found it a useful format.  I’ll add a link. Thanks to Mohamed and Rick for work on the threat model. We had some active discussion on the document. [Digital Credentials API - Threat Model and Security Considerations](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.lgu8jgz2n99n)  
* Mohamed: Good discussion on the doc, some small details remain. I think we need to agree on the format. Not sure if Marcos has strong feelings on format. If needed, I can join a B-series call. We need to add a bit more context to the mitigations.   
* Matt: Some cross-device scenarios, today being addressed by BLE. Is there something here that would… The doc describes protocol-layer, transport-layer as out-of-scope. Would we want that in-scope for cross-device? Is BLE risk in Hybrid in-scope or out-of-scope?  
* John: I think hybrid happens behind the DC API, a FIDO transport issue.  
* Matt: Where is the line for DC API to mention that class of problems? Not the specific protocol, but anticipating ultrawideband, etc. Should there be a generic discussion of that threat in the DC API?   
* Mohamed: I’d say it’s within scope, as it’s the DC API decision to use the transport.  
* Simone: \+1 to Mohamed.  
* Matt: Where should we add it?   
* Tim: It would be weird if WebAuthn doesn’t talk about it while the DC API does, even though it’s the same layer used by both.  WebAuthn doesn’t talk about it because it’s not required. The reason we have layers.   
* Matt: Take that point. I wonder out loud if there’s greater importance of cross-device flows for DC API warranting mention.   
* Rick: \+1 to Matt. EUDI requirements from Paolo talk about security and privacy of cross-device flow. In this case, being able to talk about security and privacy overall may mean normatively referencing CTAP is worth considering. I’d be ok if we made that decision.   
* Tim: Awkwardness is that we don’t want W3C on the hook for a protocol they don’t control.   
* Rick: We made good progress with that at TPAC and conversation with Martin. As with Annex C, just because we reference doesn’t mean we’re on the hook for it. Make the refs explicit so people can follow them. Hold the other groups accountable for what’s in their specs.   
* Simone: In WebAuthn security review, noted the FIDO security considerations that link to CTAP.   
* John: Good idea to reference appropriate parts of CTAP, beware the slippery slope. Once we start talking about the things that happen behind the DC API, then we have a huge potential set of security considerations. A reference, with things that are specific to the DC API JS interface being exposed. Scope carefully. We don’t want to talk about everything that happens between a credential provider and a selector.   
* Mohamed: A minor difference with WebAuthn is that this API has a competing custom scheme approach, so strategic reference to improved security considerations.   
* Tim: There will be another spec at some point that references Hybrid. Watch for it as we make normative reference.  
* Wendy: It sounds like there is consensus that a normative reference to CTAP will be appropriate. We should be careful about what is within scope.  
* Simone: We should include a threat model to formally address the concerns raised by Formal Objector.   
* Heather: Suggest we want a separate call to discuss the threat model. I think that remains a separate document. Discuss with SING, TAG, WG.   
* Simone: Fine, it’s a place we can point to say we have addressed the concerns raised.   
* Heather: Let's schedule a meeting for January.   
* Heather: For those who volunteered to draft security considerations, look at my doc as a strawman for context.


# AOB

Registry

* Wendy: We heard no objections to the decision at TPAC to remove the registry, so that decision is final. Thanks Tim for starting a PR to implement.   
* Matt: Tim’s PR answered most of my questions from reading the TPAC minutes; This is going to become a discrete list of protocols. I like it as it’s easier to use for an open source library. Did you discuss what happens if “popcorn protocol” comes up? We just bring it to the group?  
* Rick: Do we try to enumerate all the boxes that a protocol checks in advance? No, it’s a set of tradeoffs, including how critical it is to deployment and usage. So Martin said we shouldn’t try to define a checklist.   
* Matt: We have the whole "user agents support protocols" thing. Is that still useful?   
* Tim: This change doesn’t mean everyone must support all protocols. So that method would stay.  
* Matt: Did the conversation talk about whether the WG becomes a gatekeeper for new protocols?   
* Rick: I think what MT was asking amounts to some degree of gatekeeping. Being able to reason about security and privacy entails some gatekeeping. It’s possible there’s a cost, a tradeoff. Talking more about the path to rec, I supported this change, then found the cost-benefit tradeoff goes to this change.   
* Matt: Access to ISO spec?  
* Heather: It will apparently be made public, free next year.   
* Lee: Specs will be available for three years. It will be freely viewable on the website, not downloadable. There’s no stable link to it.   
* Tim: Raises a question of what normative reference link I use in the spec. I didn’t include issuance because that’s in 1.1. Need to figure out what we do timewise.   
* Matt: Will we have to have a discussion about deprecation? As OpenID v2 comes out, e.g.  
* Tim: As spec is written, old versions are allowed, not necessarily supported.   
* Matt: Do we need to keep track of recognized protocols vs supported? Is that in digitalcredentials.dev?   
* Tim: I think that’s digitalcredentials.dev. I think that if in the future, a privacy or security issue was discovered, that might be a case for deprecation.  
* Heather: That’s for the future.   
* Heather: For fun, I wrote a blog post about layering, [https://sphericalcowconsulting.com/2025/11/25/dc-api-politics/](https://sphericalcowconsulting.com/2025/11/25/dc-api-politics/)   
* Matt: For my PR, how to handle multiple request entries, have we defined enough of the order of operations of how the DC API should handle multiple presentation request entries?   
* Mohamed: I think  you’re referring to what Marcos calls the algorithm section. Still a WiP, 372, waiting for the terminology section. Need to ask Marcos.  
* Tim: Let’s not block on terminology. If there's a protocol request that's not identified in the spec, it should be ignored.   
* Mohamed: Think we remove before sending to the cred manager.   
* Heather: Expect some meeting cancellations toward the end of the year. 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Wendy Seltzer  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/him) ([OpenLink Software](https://openlinksw.com/))  
* George Fletcher  
* Mohamed Amir Yosef (Google Chrome)  
* Simone Onofri (W3C)   
* Bjorn Hjelm (Yubico)  
* Ryan Watkins (Mastercard)  
* Brian Campbell (Ping)  
* Isaiah Inuwa (Bitwarden)  
* Helen Qin (Google Android)  
* Rick Byers (Google)