# FedID WG Telecon — DC API Series A, 2026-05-04

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
* DC API Issues & PRs (45 minutes)  
  * [DC API CR Project Plan](https://github.com/orgs/w3c-fedid/projects/1/views/1)  
* Any Other Business (AOB)

# Notes

### Ecosystem Updates (5 minutes)

* No ecosystem updates

## DC API Issues & PRs

### [DC API CR Project Plan](https://github.com/orgs/w3c-fedid/projects/1/views/1)

* Heather: Is this useful? Marcos made this while I was out.  
* Tim: What’s the intent besides alternative view into issues?  
* Heather: I don’t know yet.  
* Tim: If we’re going to use this, we need more than the three statuses (Todo, In Progress, Done), since we might not address all issues.  
* Tim: Are these all of the open issues? I don’t see total counts… 81 here out of 89 issues in the repo.  
* Mohamed: It’d be interesting to know which are the missing 8 and why they’re not included.  
* Mohamed: We had a productive meeting on Wednesday’s call, but Marcos didn’t mention this yet. I know Marcos wants to discuss a plan for CR and decide which issues are V1 vs. V2, but I don’t have much other context.  
* Tim: We can do triaging.  
* Tim: Marcos replied to a couple… there’s automations on some issues that put them into the DC API CR Project Plan view  
* Tim: I don’t know if this is related to the pending issues tag.( I added that back in September.) I don’t think so.  
* Tim: Do we want to add a CR tag?  
* Heather: I think that would be helpful. Also, if there’s something that we’re not going to address in V1 and maybe will in V2, that’d be good too.  
* Heather: That discussion would be worthwhile.  
* Heather: In order to get to CR, we have to address all the open issues. Doesn’t mean “resolve,” may mean “we’re not going to do this (yet)”.  
* Heather: Let’s go ahead and triage, not use the project for now, while we figure this out.

# AOB

- Heather: Anything else?

\#\# Triage

- [\#35](https://github.com/w3c-fedid/digital-credentials/issues/35)  
  - Tim: Kyle responded and said OK, so we’ll close.  
  - Christian: I’m a bit concerned about that, as I don’t see how an allow list would ever work, but we can discuss the PR when it comes.  
  - Tim: Yeah, it’s out of scope.  
  - Heather: Do we want to leave it open until the PR so we can tie it back?  
  - Time: The issue is so broad, but we can.  
  - Heather: I think that makes sense.  
- [\#44](https://github.com/w3c-fedid/digital-credentials/issues/44)  
  - Heather: Nick added this.  
  - Christian: Similar issue as the one before. It seems that we’re repeating.  
  - Heather: We keep coming back to the issue of layering. It is apparent to some here, but it keeps coming up for people that do not think that this is a safe way to expose this API. Is there any way we can articulate this so it is more clear that we are committed to layering and explain what happens where?  
  - Tim: Seems repetitive. But I don’t think that would address the confusion with this ticket.  
  - Mohamed: He’s asking for a place to put the reason for the request in the API. It could be done in the HTML. It’s unclear how wallets should all interpret this.  
  - Heather: Is there a public discussion we can point back to?  
  - Christian: Maybe in the mailing lists.  
  - Christian: There’s not a global rule for this. We could link to the extension points. [https://openid.github.io/OpenID4VP/openid-4-verifiable-presentations-1\_0-wg-draft.html\#name-verifier-info](https://openid.github.io/OpenID4VP/openid-4-verifiable-presentations-1_0-wg-draft.html#name-verifier-info)  
  - Mohamed: [https://github.com/w3c-fedid/digital-credentials/issues/44\#issuecomment-2707480219](https://github.com/w3c-fedid/digital-credentials/issues/44#issuecomment-2707480219) Christian, which direction did we wind up with?  
  - Christian: We didn’t reach consensus at a global rule, so each implementation has to define their own rules.   
  - Tim: No decision for either CR or V2?  
  - Heather: What I’m hearing is, we think it should be closed, but closing without Nick’s input seems not good.  
  - Tim: So pending closure in 2 weeks?  
  - Heather: Yes, and I’ll add a link so he can follow up.  
- [\#66](https://github.com/w3c-fedid/digital-credentials/issues/66)  
  - Mohamed: This seems like a nice diagram to add?  
  - Tim: I think this is intended to convey browser internals.  
  - M: But looking at the comments, we see “user agent”, “mobile device”. There’s a sketch in the 4th comment.  
  - Tim: Where would this go in the spec?  
  - M: I don’t know, maybe intro?  
  - Heather: FWIW, this looks like what inspired the layering document that Tim created. So I don’t know if the layering diagrams on digitalcredentials.dev would make sense.  
  - Mohamed: Let’s ask Marcos if this is still relevant.  
  - H: Yes  
- [\#84](https://github.com/w3c-fedid/digital-credentials/issues/84)  
  - ?  
  - Tim: If anything has pending closure, then I think we can skip.  
  - Heather: Agreed.  
- [\#85](https://github.com/w3c-fedid/digital-credentials/issues/85)  
  - Registry of credential types  
  - Tim: We said we’re not doing this, right?  
  - Heather: Correct.  
  - H: Even without a registry, Nick still has privacy related questions and a lack of clarity on how we are going to explicitly answer those.  
  - Tim: A lot of those were before we removed the registry. So maybe pending closure in 2 weeks to give a chance to respond?  
  - H:   
  - H: A lot of these are privacy issues, but …  
  - H: I don’t see why we removed pending closure.  
  - Christian: Wasn’t this linked to a PR?  
  - T: There was pushback about closing all of the linked issues with the one PR.  
  - T: Adding a note to address.  
- [\#100](https://github.com/w3c-fedid/digital-credentials/issues/100)  
  - Tim: I think we addressed this. \[...\] The actual verification steps don’t require \[it\], besides JSON serialization?  
  - T: Comment is strange: “if required by the format” doesn’t make sense.  
  - Christian: Maybe guarantee predefined extension points remain as extension points. If it’s defined in the spec, the extension point is respected in the check.  
  - T: That’s implementation, not spec  
  - Mohamed: I think we can close. Data must be JSON parsed is the last thing, but now it’s a JSON object, so that’s not relevant any more.  
  - T: Close with comment?  
  - Agreed  
- [\#104](https://github.com/w3c-fedid/digital-credentials/issues/104)  
  - Christian: Pending closure from 9 months ago?  
  - Tim: Marcos says by May 14th  
  - Heather: Yes, let’s come back to it then  
- [\#117](https://github.com/w3c-fedid/digital-credentials/issues/117)  
  - Tim: Pending closure, since original requestor (Sam Goto) is not engaging?  
  - Tim: Sam said that it’s a duplicate of \#85  
  - Heather: There was some debate, but let’s add it as pending closure in 2 weeks  
- [\#122](https://github.com/w3c-fedid/digital-credentials/issues/122)  
  - Tim: We have to assume that requests are linkable.  
  - T: Maybe that has to be more explicit in the spec.  
  - Heather: Also referred to in [\#279](https://github.com/w3c-fedid/digital-credentials/issues/279).  
  - H: This is going to need more discussion.  
  - H: Also might want to make sure that John \[Schank?\] knows that this exists in case he wants to pick it up from Martin and Ben  
  - Mohamed: CR or V2?  
  - H: I think this is CR.  
  - T: Only things for V2 would be functionality changes, right?  
  - M: Or issues that are not critical. It seems that there should be no breaking changes in V2  
  - H: I’ll follow up with John on [\#122](https://github.com/w3c-fedid/digital-credentials/issues/122) and probably [\#123](https://github.com/w3c-fedid/digital-credentials/issues/123) (next)  
- [\#123](https://github.com/w3c-fedid/digital-credentials/issues/123)  
  - Heather: I’ll follow up with John on this  
- [\#133](https://github.com/w3c-fedid/digital-credentials/issues/133)  
  - Security considerations  
  - Heather: This was labeled “Future,” what does that mean?  
  - Christian: It’s being discussed in security considerations to be strongly recommended  
  - Heather: Shall we leave these security consideration tickets alone while we wait for Simone et al.?  
- [\#134](https://github.com/w3c-fedid/digital-credentials/issues/134)  
  - Privacy: signal of user intent  
  - Heather: Looks like a recommendation to point to something that we can’t normatively reference.  
  - Mohamed: Good to explore, but probably V2.  
  - H: OK. Added V2 label.  
- [\#139](https://github.com/w3c-fedid/digital-credentials/issues/139)  
  - Heather: Is this something that would happen in our layer?  
  - Tim: Most are not, right? But people are generally unsatisfied with that answer.  
  - H: How do we address that? Just like the registry, how to we put “what’s in which layer” to bed? I’ll give that further thought and will speak with TAG members  
  - H: Leaving open for now, until we figure out how to resolve consensus on the layering issue.  
- [\#160](https://github.com/w3c-fedid/digital-credentials/issues/160)  
  - Heather: This is just an open question from Marcos  
  - Mohamed: Pending closure to Marcos?  
  - Heather: Did Marcos reach out to any of you directly?  
  - Christian: This is out of scope since the origin matters to Credential Management, anyway  
  - Tim: I think this is already addressed since we push origin through  
  - Heather: OK, pending close.  
- [\#166](https://github.com/w3c-fedid/digital-credentials/issues/166)  
  - Layering  
  - Christian: More controversial: is the wallet certified? What does that mean? That is hard to answer. These are ecosystem decisions right now.  
  - Heather: Every ecosystem is potentially going to answer this differently.  
  - Tim: We tried to answer this by defining a second user agent, but we removed it.  
  - Heather: Tim added 2 potential changes in the spec  
  - Tim: The wallet doesn’t talk the \[DC\] API directly  
  - Christian: We don’t want the browser to receive the response; it should be encrypted.  
  - Tim: Pending closure without responses

Heather: Ending with that issue  
H: We’ll do this again after we close these and do another round of triage after those are addressed.  
H: In the meantime, please add any comments you have to the pending issues

# 

# Queue 

*  \<please use Google Meet hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair)  
* Isaiah Inuwa (Bitwarden)  
* [Ted Thibodeau Jr](https://github.com/TallTed/) (he/ him) ([OpenLink Software](https://openlinksw.com/))  
* George Fletcher (Practical Identity LLC)  
* Christian Bormann (SPRIND)  
* Tim Cappalli (Okta)  
* Mohamed Amir Yosef (Google Chrome)  
* David Waite  
* Ryan Watkins  
* Tejas Dhagawkar  
* Bjorn Hjelm  
* Brian Campbell  
* Rene Leveille