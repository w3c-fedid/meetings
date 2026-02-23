# FedID WG Telecon — DC API Series A, 2026-02-23

* Moderators: Heather

* Scribe: 

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)? [Matthew Miller](mailto:mattmil3@cisco.com)  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Warning: DST Clock skew is coming up\! 8 March through 5 April 2026  
* Ecosystem Updates (5 minutes)  
* DC API Issues & PRs (35 minutes)  
  * [privacy review for registry inclusion \#226](https://github.com/w3c-fedid/digital-credentials/issues/226)  
  * [Mandate one presentation protocol MUST be supported \#454](https://github.com/w3c-fedid/digital-credentials/pull/454)  
* Any Other Business (AOB)

# Notes

Admin: usual reminders

### Ecosystem Updates (5 minutes)

* None

## DC API Issues & PRs

### [privacy review for registry inclusion \#226](https://github.com/w3c-fedid/digital-credentials/issues/226)

* Heather: Discussed on B call. How are we going to handle privacy issues with our move away from a registry? Privacy concerns don’t evaporate, but it changes their nature. Where do we document these considerations for the protocols that we’re expecting to support? Do they belong in the spec? As a WG note? We have options, but we need to decide. Nick Doty put a suggestion in the issue, but the floor is open to discuss.  
* Heather: We do have to handle it,   
* Matt: Reviewing Nick’s suggestion, one of the options here is that instead of the privacy review being a reactive thing. The referenced protocols are all being specified outside the W3C. Could we decide what the W3C-centric privacy considerations need to be? Define those, rely on the cross pollination to propagate those to the other groups?   
* Lee: The DC API is no longer purely a dumb pipe. We have hard coded in the protocols allowed, so now the action of the DC API is fully defined. This is no different from how WebAuthn defines CBOR. So now you can write all your security/privacy requirements against a fully defined specification. So, I'm struggling to understand what the block is. Can we write a privacy consideration like we would with any spec in the W3C? If we decide to take on a new protocol, it’s a new version of this spec and that will also result in changing the privacy consideration sections.  
* Matt: Yes, we got prescriptive about the protocols, but I thought we were still going to allow arbitrary protocols through.  
* Lee: A browser can always do something outside the spec. The spec just says you should support at least one of the two, and that’s all that we’ll write privacy considerations around. If you do something outside of this spec, it’s outside those privacy considerations.   
* Matt: WebAuthn as written supports extensions as written.   
* Lee: We don’t write special privacy considerations for those. We only write privacy considerations for what’s in the spec. Before Kobe, it was in scope to try and figure out the full properties.  
* Matt: So it’s not a dumb pipe any more.   
* Tim: Everything just said proves that privacy considerations in the spec should only cover protocols in the spec. It wouldn’t make sense to talk about privacy considerations for protocols not defined in the spec. The “how to pick a good protocol” conversation should be a separate document.  
* Heather: Is that a document that should happen in this WG?  
* Tim: At least in W3C. It’s through W3C’s lens of what makes a good protocol. If it’s going to be a bunch of back-and-forth with Privacy WG then it should happen there.  
* Lee: It’s non-normative and not blocking. It could be in the README of this spec. Guidance to ourselves. “These are the sort of things we should pay attention to.” I don’t think it’s blocking as it’s non-normative. If you’re going to add a new curve or scheme to WebAuthn, we don’t have a section in the spec describing the properties of the new algorithm.   
* Matt: To clarify, \#226 is trying to suggest that we need to have this privacy consideration for things in this spec?   
* Heather: If it’s referenced in the spec, then I think Nick’s concern is that we include privacy considerations for them.  
* Matt: So do we define them first and then see if the protocols satisfy those requirements?   
* Heather: A good question to add to the issue.   
* Tim: We need to make sure the requirements don’t conflict with the protocols we’ve supported.   
* Mohamed: Question for Tim: what would we expect to include in that section? Why would the guidance being in a document be better than it being in the spec?   
* Tim: A document that describes the considerations doesn’t make sense to be in the document subject to those considerations. E.g. selective disclosure is an ecosystem consideration, but not an API consideration.  
* Mohamed: This was holding true when the DC API was a dumb pipe.  
* Tim: The (file system) API would say, “here are things to consider when asking for a PDF,” vs “here are bad things that can happen inside the PDF file format.” We’re reaching beyond what the API needs to be concerned about.  
* Lee: I agree with Tim, it doesn’t matter if it’s a document or wherever it ends up. The spec can have privacy and security considerations, but we have to respect the layering. We link to privacy and security considerations that the protocols and doc formats have published. We can’t enumerate the entire space, we need some layering. “Here’s the DC API, it supports xyz ???"  
* Christian (from chat): I think we need to be clear what exactly we expect from privacy considerations. IMHO we are mixing these 2: \- privacy considerations of this specific API; \- privacy considerations or I guess rather expectations on an ecosystem level (including all protocols etc.)  
* Johann: People probably over-index on privacy considerations. They’re non-normative; they don’t really change anything. They’re supposed to show people who review them, from a privacy perspective, that the WG has given it thought. I want people to focus on what matters: normative requirements in the spec. Apparently there’s a proposal for an auxiliary document about how to get other protocols in the spec. If that is normative guidance, then it probably needs to be in the spec. Putting it in a separate markdown is not unheard of.  
* Tim: Question to Johann: Do you agree that this is somewhat of a different spec, there are two different considerations? One at the API layer, and another at the protocol layer?  
* Johann: Those sound somewhat different, probably different sections. I think it comes back to the “dumb pipe” model: “we don’t care about the protocols being used with it.” But that doesn’t align with the goals of the implementers so the considerations probably belong in the spec.  
* Tim: Trying to figure out how to split this to make progress. We might be talking over each other between the A and B calls.  
* Johann: I think if you say “privacy considerations,” it’s more of an editorial thing. “Requirements” are more consequential; there should be more notes about why these are normatively being defined.  
* Mike: Listening to this, this is pretty meta. I suggest we take a stab at the two pieces, let people beat on it, that’s how we make progress. If we don’t do this, we won’t make progress on this issue.  
* Johann: We put a lot of stuff in the privacy considerations. Nick probably wants something normative about protocol inclusion in the group. He probably wants consequences/issues logged, etc... when someone wants to add a protocol to the spec.  
* Lee: This is a nice-to-have, but we have enough expertise in the group and enough people defining the protocols are in this group that it’s not necessary right now. We’re not considering adding new protocols right now, so it’s not as important right now. We should draft privacy considerations for the protocols we’re currently planning to include. Then we can move on.  
* Johann: That’s the dumb pipe idea.  
* Lee: Not necessarily. We’re saying we’ve looked at the privacy considerations of the selected protocols and saying we think these protocols are fine. Then we tell the reader of the spec to look at the documents drafted from those protocol SDOs.  
* Johann: That sounds fine from a go-to-market perspective. It should be the job of the WG to draft guidance on how future protocols can get added.  
* George: If I understand correctly, there are two issues here. One is, are there any privacy considerations for implementers consuming the API; and two, what does privacy look like across all of these things? It makes sense to say the latter is out of scope for the working group. Provide a warning, “if you just implement this spec, you’ve not solved privacy issues in the ecosystem.”  
* Heather: Is that something you’d be willing to help draft?  
* George: Sure, I can put something together, speaking to ecosystems, and let people red-line it.  
* Matt: Johann, I agree with you that this spec needs to provide guidance on how future protocols can be included as a normatively to be included protocol. But to Lee’s point, we already know the protocols we want right now and with all the cross-polination right now, I haven’t heard of any new protocols waiting to get in (unless maybe the harmonized protocol under discussion between the OIDF DCP WG and ISO). Can we punt it? Arguably yes because the protocols exist and we know what they are. The bigger question is, if we’re going to write something in the doc sooner than later, will it be based on our analysis of the protocols?  
* Lee: If we wrote this down, it’s unlikely we’d end up with the protocols we’ve picked. So we’ve already effectively grandfathered these in. We can have a debate about the protocols we’re putting in. But aligning on a document declaring what considerations we want to see in future protocols that get added in is a long process.  
* Johann: If we have this sort of process where we pick protocols, we need to justify it somehow. We don’t have that right now. Writing that is a future work item for this group.  
* Lee: I think we can capture that briefly in the README or other document.  
* Johann: It’s up to the group if it’s blocking or not.   
* Heather: If nothing else we’re blocked because we don’t have anything written at all. We’ve got a couple of protocols selected, because they’re “industry standard,” but nothing beyond that. I do support the text staying focused on what the API does. Not for this spec but for a separate document, we should engage the Privacy WG.

### [Mandate one presentation protocol MUST be supported \#454](https://github.com/w3c-fedid/digital-credentials/pull/454)

* Heather: next topic is MUST vs. SHOULD, at least one, all, etc. Last week there was agreement that mandating both means no implementers will be spec-compliant.  
* Matt: From an eco-system perspective, we should mandate all to avoid fragmentation. However, since we rely on implementation to decide what to get included, we should say one.  
* Tim: What does " minimum support" mean? Locally vs cross-device. We should find a way to make that distinction. I can take a stab at this text.  
* Matt: ..  
* Tim: if you don’t support it on the platform (browser+OS), send it cross-device.   
* Lee: There is no notion of understanding the protocol in the spec. We should say you should be able to send all protocols over cross-device. In other words, you shouldn’t block them on the browser-level.  
* Matt: It is tricky to reason about it because it is a collaboration between the browser+OS. This implies that browsers that run on OS that don’t support that protocol, must have their own cross-device. Are we going to get enough implementation to support that?  
* George (from chat): I think we should be careful about how we use the word "ecosystem". I feel like this conversation is more about what's required to be interoperable. Ecosystems might constrain this in some way. Or we need to be really clear about what the word "ecosystem" means in this context.  
* Tim: …  
* Lee: if you send it off, and it goes nowhere, you can do nothing about it. There will always be a possibility to be not able to implement (e.g. no Bluetooth API). But still this is better than what we have now, which is blocking on the web layer.  
* Tim: confirmed he has enough input to draft a PR.

# AOB

* 

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (Spherical Cow Consulting, co-chair)  
* Isaiah Inuwa (Bitwarden)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Chrisitan Bormann (SPRIND)  
* Mohamed Amir Yosef (Google Chrome)  
* George Fletcher (Practical Identity LLC)  
* Matthew Miller (Cisco)  
* Ryan Watkins (Mastercard)  
* Helen Qin (Google Android)  
* Mike Jones  
* Johann Hofmann (Google Chrome)  
* David Waite (Ping Identity)  
* Bjorn Hjelm (Yubico)