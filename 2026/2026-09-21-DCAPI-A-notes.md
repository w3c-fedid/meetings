# FedID WG Telecon — DC API Series A, 2026-09-21

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
    * Consensus call: PR 454  
* Ecosystem Updates (10 minutes)  
* DC API Issues & PRs (45 minutes)  
  * [Add security considerations on forged credential chooser requests \- \#506](https://github.com/w3c-fedid/digital-credentials/pull/506)  
  * [Platform-bound wallet attestation for issuance (\#382) \- \#586](https://github.com/w3c-fedid/digital-credentials/pull/586)  
  * [EU Commission’s DC API assessment](https://github.com/w3c-fedid/meetings/blob/main/2026/Assessments%20of%20W3C%20TSs%20%20-%20W3C%20Digital%20Credentials.docx)  
* Any Other Business (AOB)

# Notes

Heather: light attendance on the call, we’ll just discuss the EU Commission DC API Assessment. Simone, what are we looking for?

### [EU Commission’s DC API assessment](https://github.com/w3c-fedid/meetings/blob/main/2026/Assessments%20of%20W3C%20TSs%20%20-%20W3C%20Digital%20Credentials.docx)

* Simone: we received this document  
* Lee: I’m confused. They told us they can only reference final specs, not drafts, but then they published the law with reference to the draft. What are they looking for?  
* Heather: they’re referencing another spec that refers to our draft  
* Lee: A transitive reference. They reference HAIP, Annex C. I think ISO spec refers only to “a digital credentials” API. HAIP references us, informative references.   
* Lee: They’ve said multiple times they need a Recommendation to reference. The law is already passed. What’s likely to happen, an update to the law?   
* Simone: Re bullet 1, we can’t predict when standards process will get to Rec  
* Heather: (numbers the primary bullets)  
* Tim: we have answered their questions about structure, such as what is delegated to external components.   
* Simone: Should we give back a list of questions?  
* Tim: 4a, please give questions or concerns on privacy/security guidelines; 4c, please give specific questions or concerns given that this is internal to brower implementations; protocol registry, what’s the question? We should be clear that it’s not the spec, re prompts, but implementers may show additional prompts. This spec is of general applicability, not just EU  
* Nick: I agree with Tim, I don’t think this gives us enough detail to work with. If they are concerned that there’s not alignment with their security and privacy guidelines, please tell us where, maybe they could provide something very useful if they want to talk  
* Tim: offer them the opportunity to hold a workshop, say 3 hours in ET morning, “expert meeting”  
* Lee: maybe ask them to join a call or have a call with them. Ask what they mean  
* Tim: Invite them to TPAC?   
* Simone: I can ask for more detailed feedback on their concerns, and suggest a phone call  
* Heather: If they want a dedicated couple hours to review, we’re happy to make the time. 

## Any Other Business (AOB)

### [Platform-bound wallet attestation for issuance (\#382) \- \#586](https://github.com/w3c-fedid/digital-credentials/pull/586)

* Nick: re binding issuance, I seem to recall Lee had suggested there might be an alternate proposal.   
* Lee: We need to write up option 4\. I’ll try to do that, or Mohamed.   
* Nick: When there’s text, I’ll review with people who had raised coercion concerns to me. While we can’t control what issuers do, it would be good to have a way for people to make security choices that don’t involve static allow-lists or revealing the name of the wallet  
* Lee: In this model, a certifier certifies adherence to a standard, and issuers indicate they need that standard.   
* Tim: that sounds like a happy middle ground. (because there are also good user protections in having a basic level security certification)  
* 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Simone Onofri (W3C)  
* Wendy Seltzer (co-chair)  
* Tim Cappalli (Okta)  
* Lee Campbell (Google)  
* David Waite  
* Nick Doty (CDT)

### Regrets

* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
  


