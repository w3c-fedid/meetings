# FedID WG Telecon — DC API Series A, 2026-01-26

* Moderators: Heather

* Scribe: Isaiah

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?   
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
* Ecosystem Updates (5 minutes)  
* DC API Issues & PRs (50 minutes)  
  * [Change from Registry to Supported Protocols \#401](https://github.com/w3c-fedid/digital-credentials/pull/401)  
  * [What protocols should a user agent implement? \#439](https://github.com/w3c-fedid/digital-credentials/issues/439)  
  * [Security Considerations: Structure and Introduction](https://github.com/w3c-fedid/digital-credentials/pull/424)  
* Any Other Business (AOB)

# Notes

Admin: usual reminders

### Ecosystem Updates (10 minutes)

* Lee: The EU is going to use DC API for payment pilots. On the hook for payment flows actually working, since we have a fairly large consumer for the API, pretty big deal.  
  * Heather: Great that we’re doing passthrough, this would be a lot of work otherwise

## DC API Issues & PRs

### [Registry PR](https://github.com/w3c-fedid/digital-credentials/pull/401) \#401

- Mohamed:  
  - Some concerns with current PR shape  
  - We (Marcos and Mohamed) agree that we should merge 401, and then work on “full ops”  
  - Only remaining issue is whether we use “supported” protocols, vs. other options discussed in prior calls  
  - Should we reference issuance, or include it as full op?  
- Heather: The issues that would land on top of 401 (Marcos’s [comment](https://github.com/w3c-fedid/digital-credentials/pull/401#issuecomment-3798958332): 442 and 443\)  
- Nick:   
  - It looks like the PR just deletes the registry section and replaces it with a direct table  
  - PR also suggests that it closes other requirements that we agreed were important for consideration before something enters the registry  
  - Are we going to address those other concerns in other PRs? I would….  
  - Lee: Acc. to TPAC discussions: Spec is going to define which are supported; we would decide ad-hoc what goes in.   
    - Therefore, we hard-code support and we don’t have to publicize which are supported in the spec; there would be an internal list of requirements for future reviewers  
    - Nick: ??  
    - Lee: We changed to a pass-through API and picked these two protocols.  
    - Brian: Does this endorse the inclusion of a paywalled specification? I’m against that. It seems that we’re resigned to that.  
    - Lee: More resigned to reality than enthusiastic about it  
    - Tim: Everything that was there before is moved into this new format, except VP was changed?  
    - Brian: There was no reference to paywalled implementation prior to this.  
    - Tim: I’ll verify.  
- Mohamed:  
  - We don’t have the registry, so we don’t have general requirements.  
  - Will we reference the security requirements of the individual protocols from here?  
    - If something that we require is not supported in the upstream spec, then we will call it out.  
  - Wendy: Are there privacy issues that are distinct from gates on registry inclusion? Do we need to open those as new issues? At TPAC, we discussed that the registry is not the way do this.  
  - Simone: TPAC follow-up.  
    - In the Security Considerations, we have out-of-scope and in-scope. TPAC: we discussed an implementation requirements section  
    - Nick: I thought that was the consensus: implementation requirements that would be put in the spec.  
    - Nick: I could re-open in new issues, but it loses context of previous discussion.  
    - Lee: We changed significantly during the TPAC discussion: we used to be a dumb pipe, but post-TPAC, we are now effectively fully defining the whole thing (at least by reference). The privacy and security considerations would be against those specifications, not ours. Because we are well-defined, we can debate whether these two specs should be in DC API.  
    - Tim: (in chat) Removed references to closing 2 issues to address Nick’s concern  
    - Christian: I think it’s important that we are specific in the relationships between the DC API and the underlying protocols. We need to express our expectations.  
    - Heather: When we say we need a new protocol to be reviewed by a Working Group, by whatever guidelines... are those supposed to be in the spec?  
    - Tim: By nature of being a spec, it goes through the Working Group. So we don’t need to put process documentation in the specification.  
    - Heather:   
    - Lee: Isn’t this just like referencing any other specification? Like WebAuthn and CBOR: WebAuthn doesn’t define the properties of CBOR it needs so that it could add another format. Similarly, DC API is referencing the other specs.  
    - Brian: There’s a difference between a serialization format and DC API → underlying specs.  
    - Lee: Is this because it’s minor?  
    - Brian: Because the serialization framework is core to the DC API.  
    - Lee: I think it is different: we used to be able to pass anything, but now we can’t.  
    - Brian: The shape is the same.  
      - I maintain the objection that we shouldn’t include a paywalled spec.   
      - Lee: I would prefer that as well.  
    - Lee: User agents will not pass anything else; only these two specifications will be passed through. If it is supposed to be extended, then it needs to go through spec modification. Rightly or wrongly, that was the compromise. TAG wanted this to have something that was fully specified so they could review it.  
    - Simone: In my opinion, this is more similar to EME. That’s why I was proposing something like implementation requirements. We have a lot more pieces of the puzzle.   
      - We discussed whether including CTAP in the ecosystem means we have to reference it in the security considerations section.  
    - Christian:  
      - IIUC, DC API will mandate specifications: does that mean you need to support at least one, or all?  
      - Would we select a specific version of the protocol, e.g. would we accept extensions to Annex C?  
    - Matt: To Brian about whether undefined protocols would be supported by DC API:  
      - It’s split across two PRs, how can one request a presentation?  
      - The user agent has the agency to decide which protocols in the spec it supports.  
      - May allow some support for “dumb pipe” —  
        - We need to revisit this: if we don’t want this to be a possibility, we need to reword this, or make it more clear that we do.  
      - \#419 and \#420  
    - Lee: Marcus raised an issue about support.  
      - I think that we should mandate support for all  
      - Matt: \#439?  
      - Can we allow minor version differences? Not sure, we need to decide.  
      - We have to get on the same page of the implications of no longer being a pipe.  
    - Heather: We’re not going to revisit whether or not we’re going to have a registry. That’s done.  
      - I think we came to consensus on which protocols.  
      - I recognize the paywall consideration.  
        - W3C has precedent for referencing ISO specs.  
          - Brian: This should not be used as consensus in this WG.  
        - Contributions by Apple, Google, and others have made this specific specification  
    - Isaiah: \[double checking the capture of Matt’s comments re 419, 420\]  
    - Matt: re-reviewing those, will leave a comment there.   
    - Lee: User Agents can do what they want even if the spec says don’t (e.g. for origin trials/feature flags). Practically, we can’t prevent them from passing more information than what the spec requires.  
  - Matt: We need to reach consensus on the name of “supported” or not.  
  - Tim: With this much discussion about this issue, even though we discussed previously, “supported” definition is a minor issue. We need to move forward on previous issues.  
  - Wendy: We need to make sure that we separate issues.  
    - I hear Brian’s concern, and it bothers many, especially in the FOSS world. At this point, unless there’s new information, we will record a decision which should be appealed as a formal objection as we move forward.  
    - Brian: This was introduced in this PR and goes beyond removing the registry, so this is new information. We’ve discussed inclusion requirements before, but it...  
    - Brian: I think this is representative of participation that is not open or equitable contributing to the implementation of the specification. I would suggest that this PR move forward without the new normative requirement to the closed specification.  
    - Lee: Confirming: we’ll include OID4VP explicitly, and then come back to the ISO spec in a separate PR?  
    - Brian: I don’t think everyone agrees with OID4VP either, but yes, that is what I am saying  
    - Tim: It’s a double standard to remove one and not the other without review. We can’t take them both out, as we then reference no APIs, which leaves the spec unimplementable.  
    - Lee:   
    - Brian: Then we should wait for it to be publicly available before adding it here.  
    - Wendy: I rescind the suggestion to note it as a formal objection. Would you be OK with raising this as an open issue with this PR merged? Since this is an editor’s draft, it’s not meant to be used as this WG’s complete recommendation.  
    - Brian: This would work only if we frame the debate as whether “we should add it” or whether “we should remove it.” There’s a big difference in process between those two.  
    - Heather: I’d like to know how others feel about accepting the PR and working on issues, or not accepting the PR and resolving this first.  
      - Ted: Should we submit this as an At Risk PR?  
      - Lee: split in 3 prs? Remove registry \[unimplementable\], then add each protocol, independently? Have debate on each protocol.  
        - Christian: I think Lee’s proposal is cleanest  
      - Tim: I’m not doing another PR until we can get full consensus on issues. This has taken 3 months, and I’m frustrated that it’s still not mergable  
      - Nick: No strong feelings about distinction. But if we don’t feel that we will be able to come to some new consensus, we need to move forward with a decision, file an objection and move on  
      - Brian: Tim, I appreciate and understand your frustration. This feels more like wearing people down than consensus.  
        - Tim: This is documented in the TPAC meeting notes.  
      - Heather: Not hearing new information  
    - Lee: (left meeting)  
    - Nick (from chat): I'm not sure a liaison agreement (although I haven't seen any text for that yet) actually helps with us doing a privacy or security review, since we presumably couldn't discuss it publicly  
      - Simone (from chat): @Nick, ISO already told me that with a liaison they'll give us free (not only free as a beer) to review. I've already \_\_\_ the docs \[scribe: agreement?\] ready  
    - Rick: Are we opposed to browsers supporting ISO? What is the specific objection?  
      - Challenges of working with ISO? Privacy and Security requirements?  
      - Should we not?  
      - Brian: No, this spec should not endorse a paywalled specification; browsers can make their own decisions. It’s a false dichotomy that only custom schemes.  
      - Rick: No implementor is going to make a decision based on DC API.  
      - Brian: There are different points of leverage throughout the ecosystem.  
      - Rick: There are pragmatic ways around this: we could omit ISO from the spec, and then Chrome and Apple can add extensions to the spec somewhere else  
      - Brian: There is discussion to make the specs available.  
- Heather: We’re not going to further hash out the ISO discussion. Let’s finish out this queue  
- Wendy: As co-chairs, we’re going to need a more structured decision process so that we are sure that we have clear decision points, and submit notice of decisions if we have to make decisions without full consensus. Heather and I will work on this to make sure everyone has notice of what is being addressed and can reach closure..  
- Matt: In closing, not including ISO is not going to be helpful to developers who want to learn about digital credentials. If Apple has mention of ISO, but W3C ideologically doesn’t reference it, this hypothetical strawman developer is going to be lost. It is not good, as someone who has paid for the spec and wants their money back; it also does a disservice to these developers.  
- Heather: Closing discussion on this for today.

### [What protocols should a user agent implement? \#439](https://github.com/w3c-fedid/digital-credentials/issues/439)

* Group ran out of time; will discuss on a future call

### [Security Considerations PRs](https://github.com/w3c-fedid/digital-credentials/pulls?q=is%3Apr+is%3Aopen+label%3Asecurity-considerations) \#424

* Group ran out of time; will discuss on a future call

# AOB

* . 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Isaiah Inuwa (Bitwarden)  
* Nick Doty (CDT)  
* Luke Dary (Red Hat/IBM)  
* Matthew Miller (Cisco)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Wendy Seltzer  
* Mohamed Amir Yosef (Google Chrome)  
* Bjorn Hjelm (Yubico)  
* Christian Bormann (Sprind)  
* Michael Jones  
* Tim Cappalli (Okta)  
* Simone Onofri (W3C)a  
* Ryan Watkins (Mastercard)  
* Brian Campbell 