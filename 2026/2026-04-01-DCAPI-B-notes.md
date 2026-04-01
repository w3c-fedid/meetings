# FedID WG Telecon — DC API Series B, 2026-04-01

* Moderators: Heather Flanagan

* Scribe: Helen Qin

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:  
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/participants/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/20240318/)  
  * Warning: DST Clock skew is still a thing\! 8 March – 5 April  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Transport-only model with delegated behavior... API \#489](https://github.com/w3c-fedid/digital-credentials/issues/489)  
  * [Proposal: Relax transient user activation requirement for all DC API requests \#478](https://github.com/w3c-fedid/digital-credentials/issues/478)  
  * [Add Unauthorized Cross-Origin Access and mitigation \#480](https://github.com/w3c-fedid/digital-credentials/pull/480)  
  * [privacy review for registry inclusion \#226](https://github.com/w3c-fedid/digital-credentials/issues/226)  
* Any Other Business (AOB)


# Notes 

## Administrivia

* 

## Ecosystem Updates

* Heather: The [Global Digital Collaboration](https://globaldigitalcollaboration.org/) event will be held in September and we will be having conversation about DC API there

## 

## DC API PRs and Issues

### [Transport-only model with delegated behavior... API \#489](https://github.com/w3c-fedid/digital-credentials/issues/489)

* Heather: We are no longer a dump pipe. There’s a new comment that pushes back on the registry decision. I will point them back to the meeting notes. Will collect for consensus and close this.  
* Lee: Is this just asking for clarification whether this is still a dumb pipe API and goes through the relevant security review? And we’ve already answered that this is no longer a dumb pipe (Marcus answered that on the issue). Should we confirm with Simone if he needs anything else or otherwise we can close?  
* Heather: SG  
* No objection from others on the call

### [Proposal: Relax transient user activation requirement for all DC API requests \#478](https://github.com/w3c-fedid/digital-credentials/issues/478)

* John: Why are we doing re-directs?  
* Lee: It's less about re-directs and more about embedded iframes. To save an extra click.   
* John: Seems reasonable? Unsure if I have enough context. Why would you give this freebie?  
* Lee: *gave payment or age verification examples*  
* John: Given that request signing and response encryption is supported, why can’t the caller make this call?  
* Lee: It’s more about easier deployment. Today the payment use case is already doing this. They already do iframes. If we only allow the caller to do this directly then everyone will have to change their deployment.  
* John: Seems like a very different use case I need to read about.  
* Lee: Yeah. Note that this API is allowing different types of Digital Credentials today.  
* John: Probably OK with this. Will comment on the bug after some more reading.

### [Add Unauthorized Cross-Origin Access and mitigation \#480](https://github.com/w3c-fedid/digital-credentials/pull/480)

* Heather: Just want to check whether there’s anything else to be discussed? I thought this was already OK to merge, but unsure after Marcos added comments. Will double check with Marcos.

### [privacy review for registry inclusion \#226](https://github.com/w3c-fedid/digital-credentials/issues/226)

* Heather: We’ve gone around multiple times about how the model should look. Concerned that we don’t have concrete writing. Suggestion is that we get Tara from W3C to come in and help.   
* Lee: Can we ask Nick to do it?  
* Heather: We have. But Nick seems to be stuck on.. I can’t tell if Nick was not sure what the group wants to say or he disagrees with what the group wants to say.   
* Wendy: Nick wrote things down when we were focusing on the registry direction. Maybe he’s not wanting to put the same amount of effort the second time without getting some engagement from others as well.   
* Heather: We’ve asked Johan to help but he’s waiting on Rick’s direction.  
* Lee: I can help follow up.  
* Heather: John, is there anyone from Mozilla that can help?  
* John: I can ask around.

## AOB

* Lee: We’re now starting to return results from multiple providers, e.g. age from one and name from another. Currently, we have a constraint that all credentials must come from the same wallet, but we’re changing from that. Need to change to returning an array of results. Native API we’re changing to return an array of DC API responses; thinking the web should change similarly. Want the group’s thinking, since it’s a non-trivial change. We have lots of use cases for this. For example, in the EU we’re demonstrating payment \+ age. In the US, we are doing boarding pass \+ mdl. We can already do this today just from one wallet. It’s just an OS constraint. Some other OS might already support this. The web API doesn’t support this today so we have to change the web API.  
*   
* 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Wendy Seltzer  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* John Schanck (Mozilla)  
* David Waite (Ping Identity)  
* René Léveillé (1Password)  
* Helen Qin (Google / Android)  
* Lee Campbell (Google / Android)  
* Tim Cappalli