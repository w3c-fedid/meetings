# FedID WG Telecon — DC API Series B, 2025-08-06

* Moderators: Heather Flanagan

* Scribe: 


Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer: Matthew Miller (Cisco)  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
  * Meeting @ IIW?  
* Ecosystem Updates (5 minutes)  
* DC API Issues, PRs  
  * [Integrate with web wallets? \#38](https://github.com/w3c-fedid/digital-credentials/issues/38)  
  * [Define Coordinator and Client \#306](https://github.com/w3c-fedid/digital-credentials/pull/306)  
  * [Add request validation \#156](https://github.com/w3c-fedid/digital-credentials/pull/156)  
* Any Other Business (AOB)


# Notes

## Administrivia

* Meeting @ IIW?  
  * IIW moved to two weeks after Authenticate 2025  
  * Drop Heather a note **within the next week** (by Aug 13\) to help her make a deadline  
  * CB: Option to have a meeting at IETF instead?  
    * Not easily. WG meetings aren’t “open meetings” so meeting spaces require funding  
    * LC (from chat): Maybe get DCP to do only a morning and we can do the afternoon. Say on Friday and we can re-use the room

## Ecosystem Updates

* LC: UK age verification laws came into effect. On Android you can do it with the DC API, OID4VP, and ZKPs.  
  * CB: Using DCQL query for age\_over\_18?  
    * LC: Yes, with a new credential format  
  * MM: Does legislation encourage adoption of these technologies?  
    * CB: Generally speaking, lots of interest in DC API but wide availability of all of the components above is not yet there  
    * LC: Not necessarily platforms, but wallets need to support ZKP and the new credential format(s) that ZKPs require  
    * CB: Ongoing discussion is which ZKP scheme is going to be the winner. Expecting to see at least two or three proposals floating around vying for adoption.  
  * HF: Feels like a catch-22 — if no one’s implementing because no one knows which ones to implement, no winners rise to the top.

## DC API PRs and Issues

### [Integrate with web wallets? \#38](https://github.com/w3c-fedid/digital-credentials/issues/38)

* LC: Didn’t we say it’s out of scope for this spec?  
* MM: Looks like Tim confirmed as such within the last week  
* HF: Does this suggest we propose a new item for this working group?  
* LC: Can we simply say it’s out of scope and close?  
* HF: That’s what I’m inclined to do, with a note that if we want to standardize web wallets we should discuss separately where that work goes.

### [Define Coordinator and Client \#306](https://github.com/w3c-fedid/digital-credentials/pull/306)

* MM: Feels like it might be a bit too much abstraction over the players involved in a DC API ceremony  
* LC: Agree with Tim’s comment. No idea how to progress it but would like to see things go more along the original lines of “Client” and “Client Platform”  
* HF: As chair I’d like to drive this to agreement. Will reach out to Marcos and Mohamed and get a better understanding why they think splitting it is a good idea.

### [Add request validation \#156](https://github.com/w3c-fedid/digital-credentials/pull/156)

* CB: One of the concerns with DC API is that it’s not just wallet and verifier interacting. It adds more gateways into the ecosystem. This has been the biggest criticism heard about the ecosystem. Can understand why Marcos says there should be more security checks. But at what layer in cross-device should which entities be involved in security checks? Getting all of them involved makes things inflexible.  
* LC: We should say that *something* should perform security checks, but not necessarily put it into the browser. Hybrid is why the expectation is not that the browser checks everything. The wallet and OS should probably verify things. Browsers should take a passive role.  
* BC: Not protocol and especially not credential level.  
* LC: Reasonable thing for spec to define that the browser mandates that response is JSON-serializable  
* HF: What will get confusing is that platforms will make different decisions about what the browser does, which are out of scope for the spec, but will make things confusing for users.  
* LC: Spec should set expectation, and if not followed, then it’s the implementations that will define success (or lack thereof)  
* LC: In the case of clientSupportsProtocol(), if we move to the browser taking a passive role, or when we think about hybrid and the client not being able to know what mobile device will get used, then the method’s utility will decrease.  
* CB: Currently fragmentation goes beyond protocol. “Is credential type supported” and “is doctype supported” would be needed to help make progress if we assume browsers remain active in the ceremony.  
* MM: The original vision of the DC API was for the browser to be a more passive participant, but the spec has since evolved to become more active. Do we need to talk more intently as a WG about the role of the browser?  
* LC: It’s probably fine with hybrid in the mix. What’s more important is that the platforms support hybrid. If Safari supported anything over hybrid, then things would get better.  
* CB: For cross-device flow, every entity checking the request…browser, platform, mobile platform, wallet…that sounds crazy.  
* LC: If this isn’t how   
* Matt: When prioritizing spec development, is it ok to give ground on some validation things if hybrid is too vague? If there is consistent availability for hybrid to support any protocol, does that shape the spec efforts? It seems like we’re making hybrid the de facto way to do presentations. If we lean on hybrid as the reason the browser is ok to validate, it seems like we’re saying it’s ok to deprioritize the local experience.  
* LC: The browser doesn’t do any validation. If the wallet ultimately does the validation, and the OS does some if there is credential selection, that’s where the responsibility lives. If you do hybrid, the responsibility lives on a remote device. Locally, it’s whatever the OS and wallet support. And the browser won’t know in advance, so all will be listed as fall. If you encompass that in the spec, the “is credential type supported?” makes no sense.  
* Matt: Makes sense, but it's concerning to think the spec is moving to make the browser more active when we talk among ourselves and say the browser should NOT be more active. We need to do more to steer the spec down the path we want it to go.  
* LC: Let’s use the spec to make that clear. What the browser does is JSON serialization; everything else happens at other layers.   
* Matt: That wouldn’t constrain browser combos that want to be more active?  
* LC: Even Apple’s implementation would be consistent if we did this. If they did everything over hybrid and everything down locally, but the OS may reject things, that would still be consistent with the spec. The only thing they’d be inconsistent with is if they dropped hybrid.  
* Matt: Is a requirement to pass through to hybrid something the spec could define as MUST behavior?  
* LC: Would like it if we can achieve consensus.   
* Matt: As co-chair, can the spec have that level of influence, in the MUST/SHALL way?  
* HF: Can’t see why not. The biggest challenge will be getting text into spec. Authors will be the ones who have to agree to add the text.  
* LC: Many within the group appear to agree on the desired browser behavior.  
* CB: We should get something in writing. I think there are many parties whose perception of DC API would change if we had something written down with a more explicit position on which participants should be actively verifying requests. This would address the biggest concerns people have about the API.

## AOB

* 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* Matthew Miller (Cisco)  
* Christian Bormann (SPRIND)  
* Brian Campbell \[on mobile device\] ([Ping](https://www.pingidentity.com))   
* Helen Qin (Google Android)  
* Lee Campbell (Google Android)  
* Ryan Watkins (Mastercard)  
* David Moore (IBM)




