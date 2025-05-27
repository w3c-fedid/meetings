# FedID WG/CG Telecon, 2025-05-27

* Moderators: Heather Flanagan

* Scribe: Johann because he is amazing

Call-in details: see [https://www.w3.org/groups/wg/fedid/calendar/](https://www.w3.org/groups/wg/fedid/calendar/) 

Charter: [https://www.w3.org/2025/02/wg-fedid.html](https://www.w3.org/2025/02/wg-fedid.html) 

# Agenda

* Administrivia  
  * Scribe volunteer(s)?  
  * Reminders:   
    * [Working Group Membership](https://www.w3.org/groups/wg/fedid/), [Community Group Membership](https://www.w3.org/community/fed-id/)  
    * [W3C Code of Conduct](https://www.w3.org/policies/code-of-conduct/)  
  * Upcoming meeting schedule  
    * summer meetings  
    * meeting during IETF 123  
* Ecosystem Updates (15 minutes)  
  * IdP/RP implementations  
    * Axel Springer's implementation of FedCM with MultiIDP based on Ory with IDPs netID and Google Sign-In  
* FedCM issues  
  * [globalObjects should be the top level window, rather than the cross site iframe when Permissions Policy is used \#729](https://github.com/w3c-fedid/FedCM/issues/729)  
  * [Add API to show error messages from failed token fetches \#498](https://github.com/w3c-fedid/FedCM/pull/498)  
  * [CR Blocker List](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\)) \- updated  
* Any Other Business (AOB)

# 

# Notes

## Administrivia

* Heather: Reminders given  
* Summer is coming \- meetings will be pulled from the calendar  
* F2F with IETF in Madrid? Having trouble finding a space.  
  * Anyone willing to host? Otherwise will have to go remote (EU timezone)

## Ecosystem Updates 

* Achim Schlosser: Colleagues from Axel Springer have made progress with Multi-IDP, have both RP and IdP to talk about their implementation here, will talk about challenges / feature requests  
* Robert Blanck: Have a good collaboration between Axel Springer / netID for RP / IdP, other 3P tech providers. I’m a business / product guy, will give an overview.  
  * We’re almost ready with this, some small fixes remaining. Hoping it will really increase our login / registration success with users, hoping for time / friction improvements  
  * We’re big fans of Multi-IdP, not a fan of all the custom login buttons  
  * One major thing to bring up: IdP prioritization support, if there are 2 or 3 IdPs can we assign a priority to them? This was filed a while ago but is still a major request. Would like to pass a table / prioritization mapping to the browser. If an IdP is signed in and available, we want to show *just* that IdP.  
  * Second issue: Dialog is on the right hand side. Widget should be able to show in the center, meet the user front and center, make it clear that now is the time to sign in.  
  * Third issue: Analytics, we need some capabilities for that. Understand the privacy issues. Login and registration is a major challenge for publishers across the industry, so we embrace FedCM. But we need some way to analyze it.  
* Daniel Dagehus: Agree with Robert. Got great support in our implementation from Google et al, but hearing the same things from other publishers. This affects not just Axel Springer.  
* Ben VanderSloot: Working on Firefox implementation of FedCM.  
  * Prioritization / drop others if specific IdP is present: Valid request, will need to talk about how to do this fairly with the ecosystem.  
  * Placement: Firefox generally wants to avoid placing browser UI in content, so hesitant to do this  
  * Analytics: Obviously we’re sensitive to user privacy, and you probably are too, being in Germany. Would be curious what you want to get out of this exactly, let’s talk more about it.  
  * Question: Are you just looking for any authentication or authentication with identifiers?  
* Robert: Mostly authentication, start off the relationship. Just getting them authenticated and maybe asking for more information later. Can ask about email address if necessary later on.  
* Ben: That’s good to hear, consider exploring Passkeys.  
* Robert: Passkeys are a few more steps, more complicated, FedCM is easy, almost just one step.  
* Ben: Can’t really say which is a better idea \- bringing that concern to passkeys or the ones you have to FedCM.  
* Robert: To respond to the prioritization concern: We can already do this selective placement in content land, we just want the same capability in FedCM as well. Re: dialog placement, if the prompt isn’t clearly visible we have to give in context hints. If they’re too far apart this won’t lead to a great user experience.  
* Sam Goto: Responding to your questions:  
  * Prioritization: Seems plausible, let’s discuss this more  
  * Dialog placement: This came up in the past, have you tried FedCM active mode? That shows in the center.  
  * Analytics: Absolutely, we should give insight to developers  
  * Question: Can you walk us through your identity providers / relying parties? Who’s involved in this flow, how does it work end to end? If you use multi-idp, who are your identity providers? What space do they operate in? How many users to you expect?  
* Robert: Sure. We’re a european publisher. Not super high login rates. Working with netID, IdP by German consortium. 12 Million users. So, netID and Google as IdP, could be others (Microsoft?). Could be specific IdPs from different countries, e.g. Nordic countries have those. The reason why there might be 3-5 IdPs, currently have a lot of buttons.  
* Sam: So we know it’s mostly large email providers in Germany, is that correct?  
* Robert: Yeah, that’s still mostly correct. Also, broadcasters in Germany.  
* Daniel: We’re a federated sign in service, based on OpenID connect and FedCM.  
* Robert: It’s a non-profit foundation\!  
* Nicolas: Very excited to see multi-idp being used\! Prioritization: Issue is that we have a privacy invariant in FedCM: Want to show accounts when they are fetched. We could offer a less performant mode where we are fetching accounts in the priority order, so that we fetch the most wanted first, so we wait for the first one to return and then fetch the others. Performance tradeoff is that we’d have to wait on that to fetch the others.  
  * Active Mode is single IdP only, don't' support placement for passive mode. Might be reasonable to support that, but maybe not center. Maybe left instead of right? Don’t want it to be too spammy.  
  * Analytics: Have been thinking about this for a while, hopefully will have a more concrete proposal in the future. How do we report users who have declined? Don’t want to identify them. Maybe some uncredentialed ping with limited information?  
* Robert: re: performance, don’t really get the privacy problem but don’t have to discuss here. For analytics, we’d be okay with delayed analytics, just need something, doesn’t have to be super specific. Need to be able to do modeling, when to show the prompt, etc.  
* Chris Needham: Huge \+1 to Robert, want to increase sign in numbers, anything we can do to provide a simpler experience is welcome, looking at how FedCM fits into that. Two use cases: We run our own IdP on our owned domains, want to use FedCM for that. Second, want to enable social sign-in. Not much to add but just \+1 to all the point from Robert.  
* Robert: Everyone I’m talking to across Europe, they’re all very interested in this topic, and feel like this can change the way publishers are doing authentication. As soon as some publishers start with this, there could be a lot of others jumping on the train.  
* Heather: Are you a member of \<not sure which organisation\>?  
* Robert: \<naming other organisations they’re in\>

## FedCM issues

### [globalObjects should be the top level window, rather than the cross site iframe when Permissions Policy is used \#729](https://github.com/w3c-fedid/FedCM/issues/729)

* Ben: When you’re in an iframe delegating the permission to use FedCM, who is making the FedCM request? Origin header is the iframe. This seems bad, we have a warning that the Origin header needs to be checked by the IdP, but they can’t distinguish between embedders. Should we use the top level global for the origin header or update the security guidance to recommend x-frame protections when being embedded?  
* Christian: We can’t use the top-level origin, it’s based on referrer checks, and if you want to support a 3P iframe that’s truly independent of the top-level, you want to distinguish that.  
* Yi: The iframe is actually getting the token, it doesn’t have to share it with the top-level embedder. From the IdP’s perspective they’re protecting it with the iframe not the top-level.  
* \<some back-and-forth clarification that the token is not moving out of the iframe unless it’s post-messaged\>  
* Ben: Not sure how those auth iframes work, but at least some of this is surprising to me and others. Some security guidance would be nice around using CSP / frame-ancestors.  
* George (from chat): In the context of this conversation, the IDP will still get some identification of which origin RP is requesting the authentication, correct?  
* Yi (from chat): Right now the IdP only knows about the iframe origin who actually makes the FedCM API call.  
* George (from chat): I think this could be an issue as some IDPs may change behavior based on the requesting RP  
* Note from chat: Should it be in OAuth profile?  
* Christian: Could also mention it but shouldn’t be the only place.  
* Ben: Taking the top-frame also solves a related spec issue: a tracking vulnerability where many top-level sites can track you with the same iframe embedded.  
* Nicolas: That’s just solves by double-keying the connected accounts set, no? It’s not in the spec yet, maybe? We have triple keying at this point, should be updated. We have this implemented as an \<embedder, caller pair\> in Chrome.  
* Ben: Any other issues like that?  
* Nicolas: Good reminder, sorry about that.  
* Johann: Let’s block on this for CR  
* Ben Kelly: Would having a WPT have caught this inconsistency?  
* Christian: We don’t have one right now, not sure if WPT supports that.  
* Nicolas: We should probably add a test. Have to figure out the test infrastructure stuff.

### [Add API to show error messages from failed token fetches \#498](https://github.com/w3c-fedid/FedCM/pull/498)

* Nicolas: Probably not enough time for this.  
* Heather: Let’s move this to next call.

### [CR Blocker List](https://github.com/w3c-fedid/FedCM/wiki/Status-of-FPWD%E2%80%90identified-Issues-\(Consensus-Blockers-for-CR\)) \- updated

* We updated and reordered this. Only about 12 items remaining to be addressed. Please take a look.

## Any Other Business (AOB)

* No FedCM call next week \- see you at Identiverse conference maybe?

	

# Queue 

*  \<please use Zoom hand-raise\>

# Attendees (sign yourself in)

* Heather Flanagan (co-chair, Spherical Cow Consulting)  
* Wendy Seltzer (co-chair)  
* Erica Kovac (Google Chrome)  
* Parth Bhatt (Independent, An Individual Contributor)  
* Zachary Tan (Google Chrome)  
* Christian Biesinger (Google Chrome)  
* Ben Kelly (Meta)  
* Yi Gu (Google Chrome)  
* Ben VanderSloot (Mozilla)  
* Robert Blanck (Axel Springer)  
* Daniel Dagehus (European netID Foundation)  
* Nicolás Peña Moreno (Google Chrome)  
* Emily Lauber (Microsoft Identity)  
* Chris Fredrickson (Google Chrome)  
* Mike Jones (Self-Issued Consulting)  
* Chris Needham (BBC)  
* George Fletcher (Practical Identity LLC)  
* Johann Hofmann (Google Chrome)

