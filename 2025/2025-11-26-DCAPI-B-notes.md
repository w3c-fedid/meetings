# FedID WG Telecon — DC API Series B, 2025-11-26

* Moderators: Heather Flanagan

* Scribe: Nick Doty

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia (5 minutes)  
  * Scribe volunteer?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (30 minutes)  
  * [Make user mediation implicit and always required \#392](https://github.com/w3c-fedid/digital-credentials/pull/392)  
  * [Add terminology section, merge in Model \#387](https://github.com/w3c-fedid/digital-credentials/pull/387)  
  * [Define Digital Wallet \#386](https://github.com/w3c-fedid/digital-credentials/pull/386)  
* Any Other Business (AOB) (15 minutes)  
  * [Security Considerations](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.lgu8jgz2n99n)

# Notes 

## Administrivia

* Thanks to the group. Got lots of positive feedback from attendees about how our group ran and how we engage with each other.  
* Nick: can we have a non-member join the call?  
* Simone: can have observers present at the invitation of the chair, but active participants should become Invited Experts. issues and **but not substative (only editorial)** PRs can also come from non-members, with a form to complete IPR commitments.

## Ecosystem Updates

* 

## DC API PRs and Issues

### [Make user mediation implicit and always required \#392](https://github.com/w3c-fedid/digital-credentials/pull/392)

* Marcos: explaining the change here. what happened was, in Credential Manager, there’s a concept of mediation and whether it’s needed to request something, some like passwords could just be auto-filled. for Digital Credentials, we require mediation. So we had say that the developer should say explicitly that mediation is required. Credential Manager assumes that mediation is optional by default. but Chrome just ignores what the developer puts in the mediation parameter. WebKit will throw an error, but Chrome doesn’t, creating an interop issue.  
* Marcos: suggested that Credential Manager should have a mapping of when it defaults to required,  but Mohamed suggested we just put it explicitly in our spec. I preferred not to monkey patch the spec.  
* Nick: before, the developer had to write mediation required to make sure they realized that was necessary and was going to happen. We can change the spec to match what appears to be a buggy implementation on Chrome’s part, or we can ask Chrome to fix their implementation.   
* Marcos: we could also do that, but decided it would just be more developer friendly if the parameter wasn’t required.  
* Nick: I don’t feel strongly, but there was a reason, to make the developer know that mediation/prompting is going to happen.  
* Christian: doesn’t seem like a big impact, so might as well make it more developer friendly.  
* Marcos: prefer to make this change now and later improve Credential Manager spec.  
* Marcos: Related to "User mediation is \*credential type\* based":  [https://github.com/w3c/webappsec-credential-management/issues/248](https://github.com/w3c/webappsec-credential-management/issues/248)   
  And "Should mediation be defaulted at all?"  
  [https://github.com/w3c/webappsec-credential-management/issues/256](https://github.com/w3c/webappsec-credential-management/issues/256)  
* Heather: don’t have the meeting minutes handy, but based on experience, doesn’t sound like this is very contentious. has reviews with approval, should be okay to merge.

### [Add terminology section, merge in Model \#387](https://github.com/w3c-fedid/digital-credentials/pull/387)

* contention about how much to define here, versus what is defined elsewhere.  
* Marcos: Tim defined terms that might be useful: wallet, credential manager (is now exported though wasn’t previously). Marcos prefers to do one definition at a time, small PRs, because lots of potential discussion and implications throughout the spec. which terms to be defined, where are they used in the spec, communities that might also reference it from outside the spec like Manu from VCWG since we have a formal requirement to work closely with them. we currently depend on/use definitions from the Verifiable Credentials spec, like “verifier”.  
* Heather: good for us to re-use definitions from elsewhere wherever possible, to avoid confusion across the ecosystem.  
* Marcos: PR proposes referencing an IETF draft that I don’t recognize, which was surprising.  
* – scribe thinks this is the draft referenced: [https://datatracker.ietf.org/doc/draft-ietf-spice-vdcarch/](https://datatracker.ietf.org/doc/draft-ietf-spice-vdcarch/)   
  * Heather: SPICE is a group I’m co-chairing at IETF. That’s a very drafty spec, just presented to the IETF group at the most recent meeting.  
* Heather: IETF group is someone we liaise with.  
* Marcos: we should do it in coordination with the Verifiable Credentials Working Group. need further context.  
* Marcos: hope Tim will be sending separate pull requests for each definition and where they are used. figuring out who owns these definitions for the community.  
* Christian: we should be overly explicit in terminology, so many terms are being re-used with slightly different meanings, which causes confusion for others.

### [Define Digital Wallet \#386](https://github.com/w3c-fedid/digital-credentials/pull/386)

* Marcos: waiting on Tim to approve, but great if other folks can have a look. has some positive reviews. asked Johann to review for the privacy considerations section changes.  
* David: a thing that helps you pick credentials (credential manager), thing that holds credentials, interface for those things. in the hybrid case, a credential manager is talking to another credential manager. in webauthn, the lowest level thing that holds credentials is an authenticator. seems like we need 3 terms, because there are slightly different roles.  
* Marcos: we do have 3 terms: holder, digital wallet, credential manager. changing it throughout the spec requires more reviews, like will it have an effect on privacy text?  
* Nick: I think we have much bigger changes needed on privacy rather than terminology.

## AOB

### [Security Consideration](https://docs.google.com/document/d/1BpBBiv7GgkGi1_Y7NvyD3Mkalj0g857Qw-aan3NqYwU/edit?tab=t.lgu8jgz2n99n)

Simone: ask for permission if you want to edit this Google Doc.

Threat Model, largely from the Security Interest Group. maybe summarize the threat model as a separate Group Note.

Security Considerations  
List of documents that are sources of threats.  
Listing in a table all the threats we are going to take care of in the spec, and what the response is. For example, malicious extensions create threats, might be further considered by the Web Extensions Working Group.  
API flooding of calls, can be addressed by transient activation and user mediation.  
Credential manager leakage, can be addressed by secure contexts.  
Improper verifier authorization – open question how we can try to reduce. should the browser inspect metadata and block malicious requests, or is this just a risk to be addressed by the wallet?  
cross-origin issues: addressed through permission policy (set to self by default)  
presentation response tampering: transferred to the protocol level

Heather: this isn’t exactly what I expect to see in a Security Consideration section given how the IETF does it. RFC 3552: what threats you are trying to cover, which are out of scope, how these are mitigated.  
Simone: structure should be similar. just a balance, where the Threat Model document is longer, and the Security Considerations section can be shorter. don’t want to cut and paste everything between them.

Marcos: mitigations covering different scenarios and explaining why. generally prefer to describe mitigations in more detail in the security considerations, but not as much detail on the attack. if you catch something that’s going to be bad, what are you going to do about it? WebKit tries to parse and limit the information used to present the user-request, avoiding a bunch of user-facing attacks that way. don’t want us to do more work than we need to, but want to document things we’ve done for good reasons. where ISO doesn’t have security considerations, might need to define how to handle it safely.

Nick: These are reasonable headings for a security considerations section. Is that the idea, to have sections, or will it just be this table? 

Simone: references to the much longer Threat Model document. Security Considerations section would just be this table with references. Implementation Considerations separately?

Christian: fine to have a separate longer threat model, but this spec Security Considerations should describe specifically what limits are present in this spec.

Nick: I would prefer to see prose text explanation of what the threat is to the user, how to mitigate, what the implementer needs to do it safely.

Simone: just a proposal to start discussion.

Heather: this list just talks about 8 threats that are specific to this API, where as there are many more that apply ecosystem-wide. useful for people who are thinking about the ecosystem impacts broadly. but for the specific threats that we have identified do apply to this API, could go into more detail here.

Simone: Security Considerations should be self-consistent \[?\]. implementation requirements could explain how threats should be addressed by different parts of the ecosystem.

Simone: drawn threats from the TAG finding. we should consider each, either addressing the threat or delegating them to some other part of the ecosystem. should do the same with Formal Objection. TAG Finding requests that we should do threat modeling, which is what we are doing.

Simone: open for contributions and review.

Marcos: re: browser extensions, might possibly prevent extensions from tampering with the credential namespace, because extensions have done bad things there. should go through to see what impacts on implementations, or what we have missed in implementation.

Heather: started an agenda for Monday to follow-up on a lot of this. have some quiet time.

Heather: blog post: \< \[scribe missed the link \]\>

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Nick Doty (CDT)  
* Marcos Caceres (Apple)  
* Simone Onofri (W3C)  
* Christian Bormann (SPRIND)  
* David Waite (Ping Identity)  
* Bjorn Hjelm (Yubico)